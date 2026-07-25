# Gnoland Topaz Active Peers

Live peer list for the Topaz testnet. Updated automatically via public RPC.

**RPC Endpoint:** `https://rpc.apollo-validator.eu/gnoland/`

## Current Peers (54)

| # | Moniker | IP | Direction |
|---|---------|-----|-----------|
| 1 | corenode-rpc | 37.27.235.144 | outbound |
| 2 | onbloc-test14-rpc | 52.86.126.248 | inbound |
| 3 | OnNode | 14.225.215.118 | outbound |
| 4 | onbloc-val-01 | 32.196.242.41 | inbound |
| 5 | ITRocket | 216.106.185.50 | inbound |
| 6 | UTSA-snapshot | 146.19.24.32 | inbound |
| 7 | VinjanInc | 95.216.102.220 | inbound |
| 8 | gno-core-pubseed-01 | 34.232.108.152 | outbound |
| 9 | linkednode | 152.53.125.167 | inbound |
| 10 | Trace | 135.181.21.38 | inbound |
| 11 | berty-sen-01 | 163.172.33.181 | inbound |
| 12 | NakoTurk | 167.86.76.130 | inbound |
| 13 | Oneiric Stake | 219.79.108.130 | inbound |
| 14 | pi69 | 152.53.209.74 | inbound |
| 15 | Grand Valley | 217.182.203.161 | inbound |
| 16 | Primestake | 46.224.197.243 | inbound |
| 17 | node-adiniz | 65.109.79.185 | outbound |
| 18 | gno-core-rpc-i-00ed7dec5f9636760 | 100.24.100.92 | inbound |
| 19 | 1XP | 5.9.8.148 | inbound |
| 20 | ZeycaNode | 185.16.39.172 | outbound |
| 21 | gno-core-pubseed-02 | 108.132.15.161 | outbound |
| 22 | Validatorsg | 14.224.218.56 | inbound |
| 23 | POSTHUMAN | 135.181.232.179 | outbound |
| 24 | NomadValidator | 51.210.1.60 | inbound |
| 25 | cryptech | 185.144.99.19 | inbound |
| 26 | Kleomedes | 213.45.126.145 | inbound |
| 27 | cunum | 95.216.45.147 | inbound |
| 28 | Cumulo-RPC | 148.72.141.245 | outbound |
| 29 | nodeshub-seed-node | 185.122.165.176 | outbound |
| 30 | Sr20de | 159.69.70.55 | inbound |
| 31 | 1XP-Topaz-RPC | 5.9.8.148 | inbound |
| 32 | KaLaMuC | 38.49.212.137 | inbound |
| 33 | NodeRuneR | 38.9.96.60 | inbound |
| 34 | HazenRPC | 152.53.245.124 | inbound |
| 35 | HazenNetworkSolutions | 65.108.237.96 | inbound |
| 36 | onbloc-test14-rpc | 15.165.188.185 | inbound |
| 37 | MONIKER-ADINIZ | 152.53.254.226 | inbound |
| 38 | gno-core-rpc-i-04f98c007c3bb9dc0 | 100.24.100.92 | inbound |
| 39 | ruangnode | 135.181.115.154 | inbound |
| 40 | Fluxen | 65.21.84.250 | inbound |
| 41 | gno-core-sentry-02 | 54.72.126.143 | outbound |
| 42 | coinsspor | 65.108.65.23 | inbound |
| 43 | tanjira | 208.76.222.122 | outbound |
| 44 | testovich | 135.181.216.107 | inbound |
| 45 | grandvalley-lightnode | 77.237.244.126 | inbound |
| 46 | BlockNth | 135.181.17.54 | inbound |
| 47 | gno-core-sentry-01 | 44.213.204.244 | outbound |
| 48 | doresa | 159.195.47.190 | inbound |
| 49 | n1sntry1 | 162.55.84.47 | inbound |
| 50 | node-adiniz | 217.76.53.126 | inbound |

## Seed Nodes

| Node | Address |
|------|---------|
| seed-1 | `g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656` |
| seed-2 | `g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656` |

## Quick Setup

Copy the top peers into your `config.toml`:

```toml
p2p.seeds = "g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656"
p2p.persistent_peers = "g1uezln7pckcqpt9jup08m4ehun2r03czk7yg6pp@37.27.235.144:54656,g1qgkc9h0dtdjlhzdft86pws0esf2twyw95flvy4@52.86.126.248:26656,..."
```

## Generate Fresh List

```bash
python3 gnoland-peers.py
```

---

*Last updated: 2026-07-25*
