# F3-Prover - *[ :fire: The Fastest Aleo Prover :tada: ]*
The F3 means the ***F****ree* ***F****ucking* ***F****ast*, f3-prover is a solo mode prover for aleo testnet proving, it will lead you into the super experience.

## :trophy: Reference Benchmark Results

|     CPU      |      GPU          |     Result   |
| :----------: | :---------------: | :----------: |
| AMD 7T83 * 2  |  RTX 3080 * 1    | 7000 P/s +   | 
| AMD 7542 * 2  |  RTX 3080 * 1    | 4600 P/s +   | 
| AMD 7502 * 2  |  RTX 3090 * 1    | 3917 P/s +   | 
| AMD 7302 * 2  |  RTX 3080 * 1    | 2210 P/s +   | 
| AMD 7402 * 1  |  RTX 2080T* 1    | 1700 P/s +   | 
| E5-2860 V4 * 1|  RTX 4090 * 1    |  840 P/s +   | 
| AMD 7502 * 2  |  -               |  580 P/s +   | 


## :sparkles: Architecture Overview
![Overview](https://github.com/leifree317/f3-prover/blob/main/overview.jpg)

To clear why f3-pool is here, because of f3-pool is the blockchain node here, which is responsible for the communication with the Aleo network.

## :diamonds: How to work?
The f3-prover needs work together with f3-pool, you can do as following step by step. All these steps must be done in linux environment.

### :green_book: Step-1. Pool Setup
Recommend a single server for the pool service, and enable the ports 4040 and 5050.

1. Download Pool Package

```
mkdir aleo && cd aleo

# Download tls tool
wget https://github.com/minio/certgen/releases/download/v1.2.1/certgen-linux-amd64
chmod +x certgen-linux-amd64

# Generate tls certification, and please replace '10.10.1.211' with your server ip address
./certgen-linux-amd64 -host "127.0.0.1,localhost,10.10.1.211"

wget https://github.com/leifree317/f3-prover/releases/download/latest/f3-pool
chmod +x f3-pool
```

2. Startup

```
ulimit -n 1048576 && nohup ./f3-pool start --address <YOUR_BENEFIT_ADDRESS> --network 1 --prover --nodisplay --verbosity=2 >> pool.log 2>&1 &
```

**N.B.** Please replace \<YOUR_BENEFIT_ADDRESS\> with your true aleo wallet address, and remember your server IP for prover configuration.

3. Logging
```
tail -f ./pool.log
```
![pool log](https://github.com/leifree317/f3-prover/blob/main/pool-log.jpg)

To check the pool connected aleo network succeeded, you need make sure the output log as `Puzzle (Block 48888, Coinbase Target 536870911, Proof Target 134217728)`, then it says you are working on the right road, enjoy yourself!

4. To check your solo pool production:
```
http://<POOL_IP>:3030/testnet/peers/speed/<All Speed Token>
```
You can get your \<All Speed Token\> from the starting of your pool.log.

### :blue_book: Step-2. Prover Startup
1. Download Prover
```
mkdir aleo && cd aleo

wget https://github.com/leifree317/f3-prover/releases/download/latest/f3-prover
wget https://github.com/leifree317/f3-prover/releases/download/latest/myprover.sh

chmod +x f3-prover
chmod +x myprover.sh
```

2. Startup
```
./myprover.sh <POOL_CONFIG>
```

**N.B.** Please replace \<POOL_CONFIG\> with your pool Server-IP:4040 from step-1.2.

If you can't startup with gpu because of the nvidia-smi failed, you can try the command directly as following,
```
nohup ./f3-prover -g 0 -p "<POOL_IP>:4040" >> ./prover.log 2>&1 &
```

3. Logging
```
tail -f ./prover.log
```
![prover log](https://github.com/leifree317/f3-prover/blob/main/prover-log.jpg)

**N.B.** Because of the dynamic input data and systhesis.aleo program during the puzzle resovling, the proving rate will be impacted by the epoch adjustment, take it easy, it is a normal case.

|     Pool      |      Prover       | 
| :----------:  | :---------------: | 
| < 2.2.12      |  < 1.3.10         | 
| >= 2.2.12     |  >=1.3.10         | 


***X*** [Follow Us](https://x.com/f3prover)

***Discord*** [Tech Support](https://discord.gg/kSSJdztA)
