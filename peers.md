# Gnoland Topaz Peers

Last updated: 2026-07-30 00:00 UTC | Height: 294,635 | Verified: 49/59

## How we collect peers

Every 6 hours, peer addresses are gathered from our node and public RPCs.
Each peer is then TCP-probed to confirm it is actually reachable.
Only peers that pass this check are included in the list below.

## Adding peers to your node

```bash
PEERS="g169y75djeuvpsakzlajvq4kprnqdykxrhe6tz7e@146.19.24.32:26656,g1arsudmkt63gt9tzf7gvpmhw0jh2qm485q4a568@135.181.216.107:36656,g1uezln7pckcqpt9jup08m4ehun2r03czk7yg6pp@37.27.235.144:54656,g1yr6l8qz095yz7dlvfs6cjfw3s026ksxwx7wgx5@219.79.108.130:28756,g145yqalnygs63ngs6qy3as9t2mzrq3ljz9awus6@135.181.21.38:22656,g18ncv9au4sq4d7jxjduxj4sstm3zl2lvd3kehqu@44.213.204.244:26656,g1w44kfhv9a4ruqx70jxqmykychre3ffpnfje8h7@159.195.47.190:55656,g15rqtlh060msv03g5h8vlr9wav4lxgncujtszvf@65.21.15.43:55656,g17mkvewp957pvcu2n5m7y2cpmpl7fdzlajhqm53@149.202.68.156:26676,g1uxnsjx4aamx07ql25s3pgnamzkqz6n8xl80rp8@65.108.65.23:55656,g1xeu7vvyh9e9tpqtnyn3gn84wzj4yd5k9zdltk9@176.9.111.199:26656,g17m5gtexpl4s7x3d3e2xmv5mnzx3pcxwufy97v3@162.250.190.214:26656,g1gng29x0u7rnp5w48mpkklqk2rkv4lugsnlxy4v@148.72.141.245:26670,g1tssc7zgck2qf6vdx9qqjzl5tun6cfr2vs7g7vs@168.119.4.82:32556,g1z3mavstqrfewltrw886d35fufq6v7eg63xjcet@88.198.46.55:56656,g1fgmmux236rhpn0tkf000q4qmqnn9rlftemhqvf@46.224.198.191:54656,g19c3srq7cxz4lspgvdfqerq0fr4rg0u92a9c09t@38.9.96.60:26656,g163g9pyzc8l83ta5qmedmckfywrtzhvknxlsmks@85.195.116.219:26680,g1m0tzkcdtnshtkk9u50hufhldaja0pk6yg08mzc@167.86.76.130:47656,g15z7y8lx6hdjxxempc4clsuq8j6eny9gp2cvdaq@0.0.0.0:46656,g1s3gxegh58tvm0n0nx2p2mjkyfzucdnc3zpwq07@65.108.237.96:26656,g17qp5xc8a607svp77h3ttl05mg4fuzyl5fyvc2r@152.53.253.167:55656,g1sqnza5nr7kta42mrvmk6w2h5xkl7zpunga3zkm@135.181.232.179:27656,g1f95jxjxnmegszr8ut7c38uhvjycjj2hjrpw5ds@185.122.165.176:32556,g1zzyjtaj4lv4vlx6nvaf95rpe68sdhh38t968gs@54.72.126.143:26656,g12mhgwsnv5hea3jmfyvs2szv9e4yj6dk3ldf953@116.202.156.139:36656,g1qwawm46wy4e76fusd056yataqxxr0t4hhkndmx@14.225.215.118:26656,g1ghl8lhhdnhwwvp94z0gsadvz3c03et30cqyhu2@188.68.36.11:26656,g17t7vlg7hjvsldqj06zenkxpktzntkp62thg9a7@65.109.106.214:55656,g1mjuc2r4hxz70wldpshz98v23cl0h8emp3p5ths@152.53.249.120:36656,g1twhtktqdfg6dldfcaswf6cke0t4cp6g6kszrhs@209.209.8.93:36656,g1rt7cwqx2cphm00apqh5teaeuwmlgmjqsuddexz@65.21.206.184:18656,g1cuxqrgm2hj47n95fwkpzzjh7u7vkqa5v3lw4r2@95.216.242.118:60656,g1r6jgch2ax4kvqrtju8v3pgk5pmwe9myjle9uws@65.108.111.225:36656,g18t2vue7q3nkxtpz2m78ul3h7nr5f9c69ewgw8r@135.181.115.154:14656,g1r4vfd70fc22hgavfqvavryn3grqmtw4luw8apx@152.53.125.167:21656,g1x8rvj9l5lnf54qrrrjaeenjsg8yuf9qsusfngf@5.9.8.148:30803,g18ahqzryula7y9j6w4v7fnkc0l6djn3rvguhld8@135.181.17.54:26656,g1qgkc9h0dtdjlhzdft86pws0esf2twyw95flvy4@52.86.126.248:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@108.132.15.161:26656,g1jnxhcdwecgm0r0ryrrl3tk4xpdhlv75et7lflm@65.108.73.189:40156,g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@34.232.108.152:26656,g1tnmmfecjvqkyfgjaqag9d0hnk57z09aqmsctsy@152.53.254.226:55656,g1zzp6rxf2l4x59rkevddzvqwplkhsawax0k975d@0.0.0.0:42656,g10zqystndwphs4aumuj8fujmh0z5ep9lmx9fnpl@38.49.212.137:36656,g1flz98nagl7sapvdvgsjglmyysvrk0ejlskqxwl@15.165.188.185:26656,g190ajdkf9dmmrnl2ne0wca2nppes6fn5prmqjv2@135.181.227.236:37656,g1e5l99zq6uqjge3hsmvssy7wnzv6qpfdypm8dk5@109.123.243.186:26666,g1gfrq2x5qzhue0e53xykydsfyvg3fzzx7aer32e@103.107.183.177:26656"

cd ~/gno
gnoland config set p2p.persistent_peers "$PEERS"
```

To set seeds separately:

```bash
gnoland config set p2p.seeds "g19q07ssuafhmg6r7ys7wp7rpc4jxc85cpvdy426@seed-1.topaz.testnets.gno.land:26656,g15k98e65gm8h7fdr3yr4tqn82lvch4a97a3sg3j@seed-2.topaz.testnets.gno.land:26656"
```