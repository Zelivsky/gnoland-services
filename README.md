# Gnoland Topaz Services

Public infrastructure and tools for Gnoland Topaz testnet operators by [Apollo Validator](https://apollo-validator.eu).

[![Topaz](https://img.shields.io/badge/Chain-topaz--1-blue)](https://topaz.testnets.gno.land)
[![RPC](https://img.shields.io/badge/RPC-rpc.apollo--validator.eu-green)](https://rpc.apollo-validator.eu/gnoland/)

## Services

| Service | Endpoint | Status |
|---|---|---|
| Public RPC | `https://rpc.apollo-validator.eu/gnoland/` | 🟢 Active |
| Snapshots | Coming soon | 🟡 Planned |
| Validator Monitor | Coming soon | 🟡 Planned |
| Guide | Coming soon | 🟡 Planned |

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
