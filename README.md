# Gnoland Topaz Services

Public infrastructure and tools for Gnoland Topaz testnet operators by [Apollo Validator](https://apollo-validator.eu).

[![Topaz](https://img.shields.io/badge/Chain-topaz--1-blue)](https://topaz.testnets.gno.land)
[![RPC](https://img.shields.io/badge/RPC-rpc.apollo--validator.eu-green)](https://rpc.apollo-validator.eu/gnoland/)

## Services

| Service | Endpoint | Status |
|---|---|---|
| Public RPC | `https://rpc.apollo-validator.eu/gnoland/` | 🟢 Active |
| Snapshots | `https://snapshots.apollo-validator.eu/gnoland/` | 🟢 Active |
| Validator Guide | [guide.md](guide.md) | 🟢 Active |
| Validator Monitor | Coming soon | 🟡 Planned |

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

**Check node status:**
```bash
curl -s https://rpc.apollo-validator.eu/gnoland/status | jq
```

**Get current block height:**
```bash
curl -s https://rpc.apollo-validator.eu/gnoland/status | jq -r '.result.sync_info.latest_block_height'
```

**Get network peers:**
```bash
curl -s https://rpc.apollo-validator.eu/gnoland/net_info | jq -r '.result.n_peers'
```

**Query account balance:**
```bash
curl -s "https://rpc.apollo-validator.eu/gnoland/abci_query?path=/main/store/account:/g1.../balance" | jq
```

**Broadcast transaction:**
```bash
curl -s "https://rpc.apollo-validator.eu/gnoland/broadcast_tx_commit?tx=$(gnokey maketx ...)" | jq
```

### Configuration for Wallets/Tools

```
RPC URL: https://rpc.apollo-validator.eu/gnoland/
Chain ID: topaz-1
```

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

## Validator

| Field | Value |
|---|---|
| Operator | Apollo Validator |
| Valoper | `g1z360harzpshhdnlrdgj5ljkx2aeckzavkyl9g0` |
| Chain | topaz-1 |
| Website | [apollo-validator.eu](https://apollo-validator.eu) |

## Links

- [Gnoland Website](https://gno.land)
- [Topaz Testnet](https://topaz.testnets.gno.land)
- [GnoScan Explorer](https://gnoscan.io)
- [Official Validator Docs](https://github.com/gnolang/gno/blob/chain/topaz/misc/deployments/topaz.gno.land/VALIDATOR.md)
- [Discord](https://discord.gg/gnoland)

## License

MIT
