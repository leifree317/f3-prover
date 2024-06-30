# F3-Prover - *[ :fire: The Fastest Aleo Prover :tada: ]*
The F3 means the ***F****ree* ***F****ucking* ***F****ast*, f3-prover is a solo mode prover for aleo testnet proving, it will lead you into the super experience.

## :trophy: Reference Benchmark Results

|     CPU      |      GPU          |     Result   |
| :----------: | :---------------: | :----------: |
| AMD 7542 * 2  |  RTX 3080 * 1    | 2100 P/s +   | 
| AMD 7502 * 2  |  RTX 3090 * 1    | 1740 P/s +   | 
| AMD 7502 * 2  |  -               |  520 P/s +   | 



## :diamonds: How to work?
The f3-prover needs work together with f3-pool, you can follow up the details as following step by step. All these steps must be done in linux environment.

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

N.B. Please replace <YOUR_BENEFIT_ADDRESS> with your true aleo wallet address, and remember your server IP for prover configuration.

3. Logging
```
tail -f ./pool.log
```

To check the pool connected aleo network succeeded, you need make sure the output log as `Puzzle (Block 48888, Coinbase Target 536870911, Proof Target 134217728)`, then it says you are working on the right road, enjoy yourself!

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
./myprover.sh <POOL-CONFIG>
```

N.B. Please replace <POOL-CONFIG> with your pool Server-IP:4040 from step-1.2.

3. Logging
```
tail -f ./prover.log
```


N.B. Because of the dynamic input data and systhesis.aleo program during the puzzle resovling, the proving rate will be impacted by the epoch adjustment, take it easy, it is a normal case.
