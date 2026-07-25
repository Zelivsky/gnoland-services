# Gnoland Topaz State Sync Guide

Fast synchronization methods for Gnoland Topaz testnet nodes.

[![Topaz](https://img.shields.io/badge/Chain-topaz--1-blue)](https://topaz.testnets.gno.land)
[![RPC](https://img.shields.io/badge/RPC-rpc.apollo--validator.eu-green)](https://rpc.apollo-validator.eu/gnoland/)

---

## Overview

Gnoland Topaz supports two fast-sync methods:

| Method | Speed | Data Size | Use Case |
|--------|-------|-----------|----------|
| **Snapshot** | ~2-5 min | ~500 MB compressed | Recommended for most users |
| **Genesis Sync** | ~20-40 min | Full chain | For archival nodes |

> **Note:** Traditional Tendermint state sync (`statesync.enable`) is not available in Gnoland TM2. Use snapshots instead.

---

## Method 1: Snapshot (Recommended)

### Quick Start

```bash
# 1. Stop the node
sudo systemctl stop gnoland

# 2. Download snapshot
wget -O snapshot.tar.zst https://snapshots.apollo-validator.eu/gnoland/snapshots/latest.tar.zst

# 3. Restore
rm -rf ~/topaz-data/db ~/topaz-data/wal
tar -I zstd -xf snapshot.tar.zst -C ~/topaz-data/

# 4. Start the node
sudo systemctl start gnoland
```

### Detailed Steps

#### Step 1: Install zstd

```bash
sudo apt install zstd -y
```

#### Step 2: Stop the Node

```bash
sudo systemctl stop gnoland
```

#### Step 3: Backup Validator State (Validators Only)

```bash
# Only if you're running a validator
cp ~/topaz-data/secrets/priv_validator_state.json ~/priv_validator_state.json.bak
```

#### Step 4: Download Snapshot

```bash
# Get latest snapshot info
curl -s https://snapshots.apollo-validator.eu/api/gnoland/snapshots/latest | jq

# Download
wget -O snapshot.tar.zst https://snapshots.apollo-validator.eu/gnoland/snapshots/latest.tar.zst
```

#### Step 5: Restore from Snapshot

```bash
# Remove old data
rm -rf ~/topaz-data/db ~/topaz-data/wal

# Extract snapshot
tar -I zstd -xf snapshot.tar.zst -C ~/topaz-data/

# Verify extraction
ls ~/topaz-data/db/
```

#### Step 6: Restore Validator State (Validators Only)

```bash
# Only if you're running a validator
cp ~/priv_validator_state.json.bak ~/topaz-data/secrets/priv_validator_state.json
```

#### Step 7: Start the Node

```bash
sudo systemctl start gnoland

# Monitor logs
journalctl -u gnoland -f
```

#### Step 8: Verify Sync

```bash
# Check if synced
curl -s http://localhost:26657/status | jq '.result.sync_info | {height: .latest_block_height, catching_up: .catching_up}'

# Check peers
curl -s http://localhost:26657/net_info | jq '.result.n_peers'
```

#### Step 9: Clean Up

```bash
rm -v snapshot.tar.zst
```

---

## Method 2: Genesis Sync

If you prefer to sync from genesis (slower but more thorough):

### Step 1: Start the Node

```bash
gnoland start \
  --chainid topaz-1 \
  --genesis ~/topaz-data/config/genesis.json \
  --data-dir ~/topaz-data/ \
  --skip-genesis-sig-verification
```

### Step 2: Monitor Progress

```bash
while true; do
  R=$(curl -s http://localhost:26657/status | jq -r '"\(.result.sync_info.latest_block_height) \(.result.sync_info.catching_up)"')
  echo "$(date +%H:%M:%S) $R"
  [ "${R#* }" = "false" ] && echo "SYNCED" && break
  sleep 30
done
```

### Step 3: Optimize with Persistent Peers

Add peers to `config.toml` for faster sync:

```toml
p2p.seeds = "g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656"
p2p.persistent_peers = "g1uezln7pckcqpt9jup08m4ehun2r03czk7yg6pp@37.27.235.144:54656,g1qgkc9h0dtdjlhzdft86pws0esf2twyw95flvy4@52.86.126.248:26656"
```

> **Important:** Set BOTH `p2p.seeds` AND `p2p.persistent_peers`. Using only seeds often results in 0 peers.

---

## Troubleshooting

### Snapshot restore fails with "invalid magic bytes"

**Cause:** Snapshot is corrupted or incomplete download.

**Fix:** Re-download the snapshot and verify SHA256:
```bash
sha256sum snapshot.tar.zst
```

### Node crashes after restore with "AppHash mismatch"

**Cause:** Database corruption during snapshot extraction.

**Fix:**
```bash
rm -rf ~/topaz-data/db ~/topaz-data/wal
# Re-download and restore snapshot
```

### 0 peers after restore

**Cause:** Seeds not configured or not reachable.

**Fix:**
```bash
# Verify seeds in config
grep -A2 'p2p.seeds' ~/topaz-data/config/config.toml
grep -A2 'p2p.persistent_peers' ~/topaz-data/config/config.toml

# Restart node
sudo systemctl restart gnoland
```

### Node stuck at height 0

**Cause:** Genesis verification failed.

**Fix:** Ensure you're using `--skip-genesis-sig-verification`:
```bash
gnoland start --chainid topaz-1 --genesis ~/topaz-data/config/genesis.json --skip-genesis-sig-verification
```

---

## API Reference

### Get Latest Snapshot

```bash
curl -s https://snapshots.apollo-validator.eu/api/gnoland/snapshots/latest | jq
```

Response:
```json
{
  "height": 191404,
  "size": "530M",
  "created": "2026-07-25T15:44:00Z",
  "file": "gnoland-topaz-191404.tar.zst",
  "checksum": "sha256:...",
  "network": "topaz-1"
}
```

### Download Snapshot

```bash
wget https://snapshots.apollo-validator.eu/gnoland/snapshots/latest.tar.zst
```

### Verify Checksum

```bash
sha256sum snapshot.tar.zst
```

---

## Links

- [Snapshot Service](https://snapshots.apollo-validator.eu/gnoland/)
- [Public RPC](https://rpc.apollo-validator.eu/gnoland/)
- [Peers List](peers.md)
- [Validator Guide](guide.md)
- [Apollo Validator](https://apollo-validator.eu)

---

*Created by [Apollo Validator](https://apollo-validator.eu)*
