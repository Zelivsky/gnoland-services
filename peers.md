# Gnoland Topaz Peers

Last updated: 2026-07-31 12:00 UTC | Height: 327,602 | Verified: 59/71

## How we collect peers

Every 6 hours, peer addresses are gathered from our node and public RPCs.
Each peer is then TCP-probed to confirm it is actually reachable.
Only peers that pass this check are included in the list below.

## Adding peers to your node

```bash
PEERS="g12mhgwsnv5hea3jmfyvs2szv9e4yj6dk3ldf953@116.202.156.139:36656,g17qp5xc8a607svp77h3ttl05mg4fuzyl5fyvc2r@152.53.253.167:55656,g10zqystndwphs4aumuj8fujmh0z5ep9lmx9fnpl@38.49.212.137:36656,g1xp06lm943rds6hlfvzwltc0l3ff7td76j0wltj@0.0.0.0:55656,g1qwawm46wy4e76fusd056yataqxxr0t4hhkndmx@14.225.215.118:26656,g1tnmmfecjvqkyfgjaqag9d0hnk57z09aqmsctsy@152.53.254.226:55656,g1wxpr5hd6uvz3x2wqdl79w2tzz20e7zvsgr82jv@65.109.79.185:54656,g1g7ud4knkm58hzl3hpuh7wac2tvdywhx4hah5vz@163.172.33.181:26656,g1w44kfhv9a4ruqx70jxqmykychre3ffpnfje8h7@159.195.47.190:55656,g1flz98nagl7sapvdvgsjglmyysvrk0ejlskqxwl@15.165.188.185:26656,g1uxnsjx4aamx07ql25s3pgnamzkqz6n8xl80rp8@65.108.65.23:55656,g1zrjayky7rz2e3g469ue2cj8uu5qffak7sthql9@217.76.53.126:54656,g19c3srq7cxz4lspgvdfqerq0fr4rg0u92a9c09t@38.9.96.60:26656,g1arsudmkt63gt9tzf7gvpmhw0jh2qm485q4a568@135.181.216.107:36656,g1hjer44dxck6fmyka34up3kufyvgh3x8vc04n59@89.58.62.213:26656,g1f95jxjxnmegszr8ut7c38uhvjycjj2hjrpw5ds@185.122.165.176:32556,g17t7vlg7hjvsldqj06zenkxpktzntkp62thg9a7@65.109.106.214:55656,g1fgmmux236rhpn0tkf000q4qmqnn9rlftemhqvf@46.224.198.191:54656,g1r4vfd70fc22hgavfqvavryn3grqmtw4luw8apx@152.53.125.167:21656,g1zzp6rxf2l4x59rkevddzvqwplkhsawax0k975d@0.0.0.0:42656,g145yqalnygs63ngs6qy3as9t2mzrq3ljz9awus6@135.181.21.38:22656,g1tssc7zgck2qf6vdx9qqjzl5tun6cfr2vs7g7vs@168.119.4.82:32556,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@108.132.15.161:26656,g1c2ltqzcge0xepyte4fnkxpfd8yk9nqksp9ejzf@38.246.115.151:26656,g1gng29x0u7rnp5w48mpkklqk2rkv4lugsnlxy4v@148.72.141.245:26670,g16gze0n8cruxwypgx6k9zv9a9jqjq9f857qm2wu@62.210.212.142:23656,g1trdygd8frvnmq7uakqt5ny4kr8prv4y3tqhzf0@0.0.0.0:42656,g190ajdkf9dmmrnl2ne0wca2nppes6fn5prmqjv2@135.181.227.236:37656,g10wnv6k3puuktzncn3j703gj7eju908h0dtrdr9@0.0.0.0:36656,g169y75djeuvpsakzlajvq4kprnqdykxrhe6tz7e@146.19.24.32:26656,g1qqgunhgxrlvwequxt0m2h7aan4yhnee3plfe74@185.144.99.19:26656,g1sqnza5nr7kta42mrvmk6w2h5xkl7zpunga3zkm@135.181.232.179:27656,g1vv4vnq3qupmye8ddps60683g03vcvzwu4z5qmy@32.196.242.41:26656,g1twhtktqdfg6dldfcaswf6cke0t4cp6g6kszrhs@209.209.8.93:36656,g1nutynyj08sauqemyedctx7cvr2pvw24lg0gnw6@0.0.0.0:38656,g1393shc3547t6yyva69hnpwmqnc0psxkyhknljw@152.53.245.124:26656,g1s3gxegh58tvm0n0nx2p2mjkyfzucdnc3zpwq07@65.108.237.96:26656,g18ncv9au4sq4d7jxjduxj4sstm3zl2lvd3kehqu@44.213.204.244:26656,g1wh4wqhh6ffszkwqp7a9m8zqdsfyz5awlm4n87g@148.251.2.253:48656,g1gufcep74lp5fy999sm9l6fdevq9ghnvn2lcyqs@65.108.72.169:50656,g1cw4ajr026320c3a6rfm2d77tr94yglh5namap9@65.108.198.182:22656,g1z3mavstqrfewltrw886d35fufq6v7eg63xjcet@88.198.46.55:56656,g1andygt3g7u73xex8sg7af02dm2pcgsyjjqpd04@149.50.96.58:41666,g17m5gtexpl4s7x3d3e2xmv5mnzx3pcxwufy97v3@162.250.190.214:26656,g1yr6l8qz095yz7dlvfs6cjfw3s026ksxwx7wgx5@219.79.108.130:28756,g1wfu406mz57cv2cq68agrkefd4g6pw0ew4kyvlu@216.106.185.50:54656,g18ahqzryula7y9j6w4v7fnkc0l6djn3rvguhld8@135.181.17.54:26656,g1rt7cwqx2cphm00apqh5teaeuwmlgmjqsuddexz@65.21.206.184:18656,g138usej2c7hvcqec6wzsqwaw2zexnngx0hrpele@208.76.222.122:36656,g1qgkc9h0dtdjlhzdft86pws0esf2twyw95flvy4@52.86.126.248:26656,g1m0tzkcdtnshtkk9u50hufhldaja0pk6yg08mzc@167.86.76.130:47656,g13lg797wyweuultfxdntaz3v9yuchl5p9aexj4k@93.125.49.130:26660,g1x38lw7g2p6l5ne2vpjwm3x8cjwwjqd2hd2dck4@185.16.39.172:55656,g17mkvewp957pvcu2n5m7y2cpmpl7fdzlajhqm53@149.202.68.156:26676,g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@34.232.108.152:26656,g17d5epdngr7yt7n5tn9xx0xm38s870475c6gnsk@46.224.197.243:55656,g1zzyjtaj4lv4vlx6nvaf95rpe68sdhh38t968gs@54.72.126.143:26656,g1vwxf54usx38srg3nyay4em8j043yvqfxta2f4s@37.27.235.144:54656,g1e3pftctakyx58mzapqs4syc4h0jcxwtnraq00c@185.248.24.16:55656"

cd ~/gno
gnoland config set p2p.persistent_peers "$PEERS"
```

To set seeds separately:

```bash
gnoland config set p2p.seeds "g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656"
```