# Gnoland Topaz Services

Public infrastructure and tools for Gnoland Topaz testnet operators by [Apollo Validator](https://apollo-validator.eu).

[![Topaz](https://img.shields.io/badge/Chain-topaz--1-blue)](https://topaz.testnets.gno.land)
[![RPC](https://img.shields.io/badge/RPC-rpc.apollo--validator.eu-green)](https://rpc.apollo-validator.eu/gnoland/)

## Services

| # | Service | Endpoint | Status |
|---|---------|----------|--------|
| 1 | [Public RPC](#public-rpc) | `rpc.apollo-validator.eu/gnoland/` | 🟢 Active |
| 2 | [Snapshots](#snapshots) | `snapshots.apollo-validator.eu/gnoland/` | 🟢 Active |
| 3 | [State Sync Guide](#state-sync-guide) | [statesync.md](statesync.md) | 🟢 Active |
| 4 | [Peers List](#peers-list) | [peers.md](peers.md) (auto-updated every 6h) | 🟢 Active |
| 5 | [Validator Guide](#validator-guide) | [guide.md](guide.md) | 🟢 Active |
| 6 | [Monitor Bot](#validator-monitor-bot) | [@gnoland_monitor_apollo_bot](https://t.me/gnoland_monitor_apollo_bot) | 🟢 Active |

---

## Public RPC

Base URL: `https://rpc.apollo-validator.eu/gnoland/`

### Available Endpoints

| Endpoint | Description |
|---|---|
| `/status` | Node sync status, block height |
| `/abci_info` | ABCI application info |
| `/net_info` | Network peers info |
| `/health` | Node health check |
| `/genesis` | Genesis file |
| `/block?height=N` | Block by height |
| `/validators?height=N` | Validator set |
| `/commit?height=N` | Block commit |
| `/tx?hash=H` | Transaction by hash |
| `/broadcast_tx_commit?tx=TX` | Broadcast transaction |
| `/consensus_state` | Consensus state |

### Usage Examples

```bash
# Check node status
curl -s https://rpc.apollo-validator.eu/gnoland/status | jq

# Get current block height
curl -s https://rpc.apollo-validator.eu/gnoland/status | jq -r '.result.sync_info.latest_block_height'

# Get network peers
curl -s https://rpc.apollo-validator.eu/gnoland/net_info | jq -r '.result.n_peers'

# Query account balance
curl -s "https://rpc.apollo-validator.eu/gnoland/abci_query?path=/main/store/account:/g1.../balance" | jq

# Broadcast transaction
curl -s "https://rpc.apollo-validator.eu/gnoland/broadcast_tx_commit?tx=$(gnokey maketx ...)" | jq
```

### Configuration for Wallets/Tools

```
RPC URL: https://rpc.apollo-validator.eu/gnoland/
Chain ID: topaz-1
```

---

## Snapshots

Page: `https://snapshots.apollo-validator.eu/gnoland/`

Snapshots are created every 6 hours and stored for fast node synchronization.

### Download Latest

```bash
# Get snapshot info
curl -s https://snapshots.apollo-validator.eu/api/gnoland/snapshots/latest | jq

# Download latest snapshot
wget -O gnoland-snapshot.tar.zst https://snapshots.apollo-validator.eu/gnoland/snapshots/latest.tar.zst
```

### Restore from Snapshot

```bash
# Install zstd
sudo apt install zstd -y

# Stop node
sudo systemctl stop gnoland-topaz

# Backup validator state (validators only)
cp /root/topaz-data/secrets/priv_validator_state.json /root/priv_validator_state.json.bak

# Download latest snapshot
wget -O gnoland-snapshot.tar.zst https://snapshots.apollo-validator.eu/gnoland/snapshots/latest.tar.zst

# Restore
rm -rf /root/topaz-data/db /root/topaz-data/wal
tar -I zstd -xf gnoland-snapshot.tar.zst -C /root/topaz-data/

# Restore validator state (validators only)
cp /root/priv_validator_state.json.bak /root/topaz-data/secrets/priv_validator_state.json

# Start node
sudo systemctl start gnoland-topaz

# Clean up
rm -v gnoland-snapshot.tar.zst
```

### API

```bash
curl -s https://snapshots.apollo-validator.eu/api/gnoland/snapshots/latest | jq
```

---

## State Sync Guide

Full state sync documentation: [statesync.md](statesync.md)

Two methods for fast synchronization:

1. **Snapshot restore** (recommended) — download compressed snapshot, extract, resume from saved height
2. **Genesis sync** — start from block 0, wait for chain to sync (slower)

---

## Peers List

Auto-generated: [peers.md](peers.md) (updated every 6 hours via cron)

Peers are collected from our node and public RPCs, then TCP-probed for reachability. The list includes all verified peers with ready-to-use commands for adding them to your node config.

```bash
PEERS="g1s3gxegh58tvm0n0nx2p2mjkyfzucdnc3zpwq07@65.108.237.96:26656,..."

cd ~/gno
gnoland config set p2p.persistent_peers "$PEERS"
```

---

## Validator Guide

Full installation and setup guide: [guide.md](guide.md)

### Quick Start

```bash
# Install Go and build
git clone https://github.com/gnolang/gno.git && cd gno && git checkout chain/topaz
make -C gno.land install.gnoland install.gnokey

# Configure
mkdir -p ~/topaz-data/config ~/topaz-data/secrets
gnoland config init -config-path ~/topaz-data/config/config.toml

# Download genesis
wget -O ~/topaz-data/config/genesis.json https://github.com/gnolang/gno/releases/download/chain/topaz/genesis.json

# Start
gnoland start --chainid topaz-1 --genesis ~/topaz-data/config/genesis.json --data-dir ~/topaz-data/ --skip-genesis-sig-verification
```

---

## Validator Monitor Bot

Public Telegram bot for monitoring Gnoland Topaz validators. Each user has their own monitoring list.

**Bot:** [@gnoland_monitor_apollo_bot](https://t.me/gnoland_monitor_apollo_bot)

### Commands

| Command | Description |
|---------|-------------|
| `/add <address or moniker>` | Add validator to monitoring |
| `/remove <address or moniker>` | Remove validator |
| `/list` | List your monitored validators |
| `/status` | Show network info and your validators |
| `/map <name or address>` | Look up validator info (moniker, operator, signing addr) |
| `/threshold <n>` | Set missed blocks alert threshold (default: 1) |
| `/help` | Show help |

### Adding a Validator

You can add by **signing address**, **operator address**, or **moniker**:

```
/add g1sgu52u6hfffg9tyck7v3zgd27hhv2paf9rgamr        # signing address
/add g1z360harzpshhdnlrdgj5ljkx2aeckzavkyl9g0          # operator address
/add Apollo                                              # moniker
```

Validator mapping covers 93+ validators from the [OshVanK explorer](https://explorer-gnoland.oshvank.xyz). Use `/map` to look up any validator's addresses.

### Uptime Monitoring

The bot automatically checks block signing every ~1 minute (last 50 blocks):

- **/status** and **/list** show current uptime percentage
- 🔴 Uptime below 50%
- 🟢 Uptime 50%+ or VP active

### Auto Alerts

The bot sends instant alerts for:
- 🚨 **RPC unreachable** — cannot reach Topaz node
- 🚨 **Missed blocks** — configurable threshold (default: 1 block)
- ⚠️ **Not in active set** — validator dropped from active set
- ⚠️ **Zero voting power** — validator has no delegations
- ⚠️ **Low peers** — fewer than 5 connected peers

### Threshold Configuration

By default, the bot alerts after **1 missed block**. Change with:

```
/threshold 5    # alert after 5 missed blocks
/threshold      # show current threshold
```

---

## Validator

| Field | Value |
|---|---|
| Operator | Apollo Validator |
| Valoper | `g1z360harzpshhdnlrdgj5ljkx2aeckzavkyl9g0` |
| Chain | topaz-1 |
| Website | [apollo-validator.eu](https://apollo-validator.eu) |

---

## Links

- [Gnoland Website](https://gno.land)
- [Topaz Testnet](https://topaz.testnets.gno.land)
- [OshVanK Explorer](https://explorer-gnoland.oshvank.xyz)
- [GnoScan Explorer](https://gnoscan.io)
- [Official Validator Docs](https://github.com/gnolang/gno/blob/chain/topaz/misc/deployments/topaz.gno.land/VALIDATOR.md)
- [Discord](https://discord.gg/gnoland)

## License

MIT
