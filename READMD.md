# Cardano Docker 

### build cardano-sl

```
  cd cardano-sl
  docker build -t cardano-sl-mainnet:3.0.1 .
  docker run -d --name=cardano-sl-mainnet-node -v ~/cardano/data:/home/cardano/cardano-sl/state-wallet-mainnet:Z -p 127.0.0.1:8090:443 cardano-sl-mainnet:3.0.1
  https://127.0.0.1:8090/api/v1/node-info
```