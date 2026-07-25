# Gnoland Topaz Validator Guide

Step-by-step guide for setting up a validator node on the Gnoland Topaz testnet.

[![Topaz](https://img.shields.io/badge/Chain-topaz--1-blue)](https://topaz.testnets.gno.land)
[![RPC](https://img.shields.io/badge/RPC-rpc.apollo--validator.eu-green)](https://rpc.apollo-validator.eu/gnoland/)

---

## Table of Contents

1. [Hardware Requirements](#1-hardware-requirements)
2. [Installation](#2-installation)
3. [Configuration](#3-configuration)
4. [Running the Node](#4-running-the-node)
5. [Sync](#5-sync)
6. [Validator Registration](#6-validator-registration)
7. [Troubleshooting](#7-troubleshooting)

---

## 1. Hardware Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| CPU | 2 cores | 4+ cores |
| RAM | 4 GB | 8 GB |
| Storage | 50 GB SSD | 100 GB+ NVMe |
| Network | 100 Mbps | 1 Gbps |

**OS:** Ubuntu 22.04/24.04 (recommended)

**Software:**
- Go 1.22+ (for building from source)
- Docker (alternative installation method)
- Git
- jq (for API queries)

---

## 2. Installation

### Option A: Build from Source

```bash
# Install Go (if not installed)
wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> ~/.bashrc
source ~/.bashrc

# Clone and build
git clone https://github.com/gnolang/gno.git
cd gno && git checkout chain/topaz
make -C gno.land install.gnoland install.gnokey

# Verify
gnoland version  # should show: chain/topaz
gnokey version    # should show: chain/topaz
```

### Option B: Docker

```bash
# Build image
docker build --target gnoland -t gnoland:topaz .

# Or pull from GHCR
docker pull ghcr.io/gnolang/gno/gnoland:latest
```

### Option C: Prebuilt Binaries

Download from the [releases page](https://github.com/gnolang/gno/releases/tag/chain%2Ftopaz).

---

## 3. Configuration

### Initialize Config

```bash
mkdir -p ~/topaz-data/config ~/topaz-data/secrets

gnoland config init -config-path ~/topaz-data/config/config.toml
gnoland secrets init -data-dir ~/topaz-data/secrets/
```

### Set Configuration

```bash
CFG=~/topaz-data/config/config.toml
PEERS="g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656"

# Required - chain-wide settings
gnoland config set -config-path $CFG application.prune_strategy syncable
gnoland config set -config-path $CFG consensus.timeout_commit 3s
gnoland config set -config-path $CFG consensus.peer_gossip_sleep_duration 10ms
gnoland config set -config-path $CFG p2p.flush_throttle_timeout 10ms

# Required - peer connectivity (BOTH seeds AND persistent_peers!)
gnoland config set -config-path $CFG p2p.seeds "$PEERS"
gnoland config set -config-path $CFG p2p.persistent_peers "$PEERS"

# Node-specific settings
gnoland config set -config-path $CFG moniker YOUR-MONIKER
gnoland config set -config-path $CFG p2p.laddr tcp://0.0.0.0:26656
gnoland config set -config-path $CFG rpc.laddr tcp://0.0.0.0:26657
gnoland config set -config-path $CFG p2p.pex true
gnoland config set -config-path $CFG mempool.size 10000
gnoland config set -config-path $CFG p2p.max_num_outbound_peers 40

# Set external address (your public IP)
gnoland config set -config-path $CFG p2p.external_address "$(curl -s ifconfig.me):26656"
```

> **IMPORTANT:** Set BOTH `p2p.seeds` AND `p2p.persistent_peers` to the same values. Using only seeds often results in 0 peers.

### Open Firewall

```bash
sudo ufw allow 26656/tcp comment "Topaz P2P"
```

---

## 4. Running the Node

### Download Genesis

```bash
cd ~/topaz-data/config
wget -O genesis.json https://github.com/gnolang/gno/releases/download/chain/topaz/genesis.json

# Verify SHA256
shasum -a 256 genesis.json
# Expected: 2dd049f973b82858727440df9aff5722cb0b322fd00890f40f2b0688276898ff
```

### Create systemd Service

```bash
sudo tee /etc/systemd/system/gnoland.service > /dev/null <<EOF
[Unit]
Description=Gnoland Topaz node
After=network-online.target

[Service]
User=$USER
WorkingDirectory=$HOME
Environment=HOME=$HOME
ExecStart=$(which gnoland) start \\
  --chainid topaz-1 \\
  --genesis $HOME/topaz-data/config/genesis.json \\
  --data-dir $HOME/topaz-data/ \\
  --log-level info \\
  --skip-genesis-sig-verification
Restart=on-failure
RestartSec=5
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now gnoland
```

### Verify Node is Running

```bash
# Check service status
sudo systemctl status gnoland

# Check logs
journalctl -u gnoland -n 50 --no-pager -o cat

# Check sync status
curl -s http://localhost:26657/status | jq '.result.sync_info | {height: .latest_block_height, catching_up: .catching_up}'

# Check peers
curl -s http://localhost:26657/net_info | jq '.result.n_peers'
```

---

## 5. Sync

### From Genesis (slow, ~20-40 minutes)

The node will sync automatically from genesis. Monitor progress:

```bash
while true; do
  R=$(curl -s http://localhost:26657/status | jq -r '"\(.result.sync_info.latest_block_height) \(.result.sync_info.catching_up)"')
  echo "$(date +%H:%M:%S) $R"
  [ "${R#* }" = "false" ] && echo "SYNCED" && break
  sleep 30
done
```

### From Snapshot (fast, ~2-5 minutes)

```bash
# Install zstd
sudo apt install zstd -y

# Stop node
sudo systemctl stop gnoland

# Download snapshot
wget -O snapshot.tar.zst https://snapshots.apollo-validator.eu/gnoland/snapshots/latest.tar.zst

# Restore
rm -rf ~/topaz-data/db ~/topaz-data/wal
tar -I zstd -xf snapshot.tar.zst -C ~/topaz-data/

# Verify validator state
cat ~/topaz-data/secrets/priv_validator_state.json
# Should show: {"height":"0","round":"0","step":0}

# Start node
sudo systemctl start gnoland

# Clean up
rm -v snapshot.tar.zst
```

---

## 6. Validator Registration

### Prerequisites

- Node fully synced (`catching_up: false`)
- GNOT in your operator account (request from [faucet](https://topaz.testnets.gno.land/faucet))

### Get Your Keys

```bash
# List your accounts
gnokey list

# Get consensus public key
gnoland secrets get -data-dir ~/topaz-data/secrets/ validator_key
```

### Register as Validator

```bash
gnokey maketx call \
  --pkgpath gno.land/r/gnops/valopers \
  --func Register \
  --args "YOUR-MONIKER" \
  --args "Your description (max 2048 chars)" \
  --args "data-center" \
  --args "YOUR_G1_OPERATOR_ADDRESS" \
  --args "YOUR_GPUB1_CONSENSUS_PUBKEY" \
  --gas-fee 1000000ugnot \
  --gas-wanted 100000000 \
  --chainid topaz-1 \
  --remote https://rpc.apollo-validator.eu/gnoland/ \
  --broadcast \
  wallet
```

> **Note:** Use `--gas-wanted 100000000` (not 50M as in some guides). You only pay for gas actually used.

### Verify Registration

```bash
gnokey query vm/qrender -data "gno.land/r/gnops/valopers:YOUR_G1_ADDRESS" \
  -remote https://rpc.apollo-validator.eu/gnoland/
```

Or check on [GnoScan](https://gnoscan.io) or the [Valopers page](https://topaz.testnets.gno.land/r/gnops/valopers).

### Join Active Set

After registration, you are a **candidate**. A GovDAO member must create and pass a proposal to add you to the active validator set.

---

## 7. Troubleshooting

### 0 Peers / Stuck at Height 0

**Cause:** Only `p2p.seeds` is set, but `p2p.persistent_peers` is not.

**Fix:** Set both to the same values:
```bash
gnoland config set -config-path $CFG p2p.seeds "$PEERS"
gnoland config set -config-path $CFG p2p.persistent_peers "$PEERS"
sudo systemctl restart gnoland
```

### AppHash Mismatch Crash Loop

**Cause:** Local database corruption during fast-sync.

**Fix:**
```bash
sudo systemctl stop gnoland
rm -rf ~/topaz-data/db ~/topaz-data/wal
# Restore from snapshot or resync from genesis
sudo systemctl start gnoland
```

### `go: command not found`

**Fix:**
```bash
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> ~/.bashrc
```

### Out of Gas on Registration

**Fix:** Increase gas limit:
```bash
--gas-wanted 100000000
```

### Node Running but Not Producing Blocks

**Check logs:**
```bash
journalctl -u gnoland -n 50 --no-pager -o cat | grep -iE "error|panic|corrupt"
```

### Validator Key Type Error

Topaz does not support `secp256k1` keys. Only `Ed25519` is supported.

**Check your key type:**
```bash
jq -r '.pub_key["@type"]' ~/topaz-data/secrets/priv_validator_key.json
# Should show: /tm.PubKeyEd25519
```

---

## Quick Reference

| Item | Value |
|------|-------|
| Chain ID | `topaz-1` |
| RPC | `https://rpc.apollo-validator.eu/gnoland/` |
| Genesis SHA256 | `2dd049f973b82858727440df9aff5722cb0b322fd00890f40f2b0688276898ff` |
| Snapshot | `https://snapshots.apollo-validator.eu/gnoland/snapshots/latest.tar.zst` |
| Faucet | `https://topaz.testnets.gno.land/faucet` |
| Valopers | `https://topaz.testnets.gno.land/r/gnops/valopers` |
| GnoScan | `https://gnoscan.io` |
| Discord | `https://discord.gg/gnoland` |

---

## Links

- [Official Validator Docs](https://github.com/gnolang/gno/blob/chain/topaz/misc/deployments/topaz.gno.land/VALIDATOR.md)
- [Gnoland Website](https://gno.land)
- [GitHub](https://github.com/gnolang/gno)
- [Apollo Validator](https://apollo-validator.eu)

---

*Created by [Apollo Validator](https://apollo-validator.eu). Contributions welcome!*
