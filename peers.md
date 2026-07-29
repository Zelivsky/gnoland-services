# Gnoland Topaz Peers

Last updated: 2026-07-29 00:00 UTC | Height: 270,710 | Verified: 46/57

## How we collect peers

Every 6 hours, peer addresses are gathered from our node and public RPCs.
Each peer is then TCP-probed to confirm it is actually reachable.
Only peers that pass this check are included in the list below.

## Adding peers to your node

```bash
PEERS="g1z3mavstqrfewltrw886d35fufq6v7eg63xjcet@88.198.46.55:56656,g1fgmmux236rhpn0tkf000q4qmqnn9rlftemhqvf@46.224.198.191:54656,g19c3srq7cxz4lspgvdfqerq0fr4rg0u92a9c09t@38.9.96.60:26656,g163g9pyzc8l83ta5qmedmckfywrtzhvknxlsmks@85.195.116.219:26680,g1f95jxjxnmegszr8ut7c38uhvjycjj2hjrpw5ds@185.122.165.176:32556,g1s3gxegh58tvm0n0nx2p2mjkyfzucdnc3zpwq07@65.108.237.96:26656,g17qp5xc8a607svp77h3ttl05mg4fuzyl5fyvc2r@152.53.253.167:55656,g1qqgunhgxrlvwequxt0m2h7aan4yhnee3plfe74@185.144.99.19:26656,g1zzyjtaj4lv4vlx6nvaf95rpe68sdhh38t968gs@54.72.126.143:26656,g12mhgwsnv5hea3jmfyvs2szv9e4yj6dk3ldf953@116.202.156.139:36656,g1qwawm46wy4e76fusd056yataqxxr0t4hhkndmx@14.225.215.118:26656,g1twhtktqdfg6dldfcaswf6cke0t4cp6g6kszrhs@209.209.8.93:36656,g1rt7cwqx2cphm00apqh5teaeuwmlgmjqsuddexz@65.21.206.184:18656,g13lg797wyweuultfxdntaz3v9yuchl5p9aexj4k@93.125.49.130:26660,g1r6jgch2ax4kvqrtju8v3pgk5pmwe9myjle9uws@65.108.111.225:36656,g1u70ql9gf8ady48cw0vlf865qzmhc3w8asqsj30@65.21.84.250:41656,g17d5epdngr7yt7n5tn9xx0xm38s870475c6gnsk@46.224.197.243:55656,g1x8rvj9l5lnf54qrrrjaeenjsg8yuf9qsusfngf@5.9.8.148:30803,g1qgkc9h0dtdjlhzdft86pws0esf2twyw95flvy4@52.86.126.248:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@108.132.15.161:26656,g1jnxhcdwecgm0r0ryrrl3tk4xpdhlv75et7lflm@65.108.73.189:40156,g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@34.232.108.152:26656,g1zzp6rxf2l4x59rkevddzvqwplkhsawax0k975d@0.0.0.0:42656,g190ajdkf9dmmrnl2ne0wca2nppes6fn5prmqjv2@135.181.227.236:37656,g169y75djeuvpsakzlajvq4kprnqdykxrhe6tz7e@146.19.24.32:26656,g1uezln7pckcqpt9jup08m4ehun2r03czk7yg6pp@37.27.235.144:54656,g1yr6l8qz095yz7dlvfs6cjfw3s026ksxwx7wgx5@219.79.108.130:28756,g145yqalnygs63ngs6qy3as9t2mzrq3ljz9awus6@135.181.21.38:22656,g18ncv9au4sq4d7jxjduxj4sstm3zl2lvd3kehqu@44.213.204.244:26656,g1w44kfhv9a4ruqx70jxqmykychre3ffpnfje8h7@159.195.47.190:55656,g1c2ltqzcge0xepyte4fnkxpfd8yk9nqksp9ejzf@38.246.115.151:26656,g1uxnsjx4aamx07ql25s3pgnamzkqz6n8xl80rp8@65.108.65.23:55656,g15rqtlh060msv03g5h8vlr9wav4lxgncujtszvf@65.21.15.43:55656,g17mkvewp957pvcu2n5m7y2cpmpl7fdzlajhqm53@149.202.68.156:26676,g1zrjayky7rz2e3g469ue2cj8uu5qffak7sthql9@217.76.53.126:54656,g1w346jst39hk93grftsjdhvgw2yg32nfxjz6e9c@46.224.220.23:54656,g1gng29x0u7rnp5w48mpkklqk2rkv4lugsnlxy4v@148.72.141.245:26670,g17m5gtexpl4s7x3d3e2xmv5mnzx3pcxwufy97v3@162.250.190.214:26656,g1rrj6gvxp7ph8d4rsy9vegrhp8nx4lyxzgmc4ad@65.109.124.135:54656,g1tssc7zgck2qf6vdx9qqjzl5tun6cfr2vs7g7vs@168.119.4.82:32556,g1m0tzkcdtnshtkk9u50hufhldaja0pk6yg08mzc@167.86.76.130:47656,g1wfu406mz57cv2cq68agrkefd4g6pw0ew4kyvlu@216.106.185.50:54656,g17t7vlg7hjvsldqj06zenkxpktzntkp62thg9a7@65.109.106.214:55656,g1393shc3547t6yyva69hnpwmqnc0psxkyhknljw@152.53.245.124:26656,g1flz98nagl7sapvdvgsjglmyysvrk0ejlskqxwl@15.165.188.185:26656,g1e3pftctakyx58mzapqs4syc4h0jcxwtnraq00c@185.248.24.16:55656"

cd ~/gno
gnoland config set p2p.persistent_peers "$PEERS"
```

To set seeds separately:

```bash
gnoland config set p2p.seeds "g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656"
```