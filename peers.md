# Gnoland Topaz Peers

## Where does this data come from?

Peer data is obtained from the node's `/net_info` RPC endpoint. Each Gno/TM2 node has a `node_id` and `p2p_address` (`g1...@host:port`). Reachability is verified by opening a real TCP connection to each peer's advertised address — not all peers in `/net_info` are actually dialable.

Find your own node's identity: `gnoland secrets get node_id` or `gnoland secrets get node_id.p2p_address`

## How this list is built

Every 6 hours, peers are collected from multiple independent sources — our own node and trusted validator RPCs — then TCP-probed on the p2p port to verify external reachability. Only peers that pass a reachability check are published. A multi-factor score ranks them by stability, network presence, and how many independent validators see them simultaneously.

## Persistent Peers Config

Auto-generated from the 15 fastest verified-reachable peers. Run on your node to bootstrap stable P2P connectivity. Refreshes with each scan cycle.

```
PEERS="g1m0tzkcdtnshtkk9u50hufhldaja0pk6yg08mzc@167.86.76.130:47656,g1mjuc2r4hxz70wldpshz98v23cl0h8emp3p5ths@152.53.249.120:36656,g1gfrq2x5qzhue0e53xykydsfyvg3fzzx7aer32e@103.107.183.177:26656,g17d5epdngr7yt7n5tn9xx0xm38s870475c6gnsk@46.224.197.243:55656,g1yr6l8qz095yz7dlvfs6cjfw3s026ksxwx7wgx5@219.79.108.130:28756,g12mhgwsnv5hea3jmfyvs2szv9e4yj6dk3ldf953@116.202.156.139:36656,g1nutynyj08sauqemyedctx7cvr2pvw24lg0gnw6@0.0.0.0:38656,g1wxpr5hd6uvz3x2wqdl79w2tzz20e7zvsgr82jv@65.109.79.185:54656,g1rrj6gvxp7ph8d4rsy9vegrhp8nx4lyxzgmc4ad@65.109.124.135:54656,g1x8rvj9l5lnf54qrrrjaeenjsg8yuf9qsusfngf@5.9.8.148:30803,g1x38lw7g2p6l5ne2vpjwm3x8cjwwjqd2hd2dck4@185.16.39.172:55656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@108.132.15.161:26656,g1jnxhcdwecgm0r0ryrrl3tk4xpdhlv75et7lflm@65.108.73.189:40156,g1sqnza5nr7kta42mrvmk6w2h5xkl7zpunga3zkm@135.181.232.179:27656,g1qqgunhgxrlvwequxt0m2h7aan4yhnee3plfe74@185.144.99.19:26656"
```

Copy and run on your node:

```
cd ~/gno
gnoland config set p2p.persistent_peers "$PEERS"
```

## Seed Nodes

```
g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656
g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656
```

## Links

- [Public RPC](https://rpc.apollo-validator.eu/gnoland/)
- [Snapshots](https://snapshots.apollo-validator.eu/gnoland/)
- [Validator Monitor](https://t.me/gnoland_monitor_apollo_bot)
- [Apollo Validator](https://apollo-validator.eu)
