# Cardano Docker 

### build cardano-sl

```
  cd cardano-sl
  docker build -t cardano-sl:1.3.0 .
  docker run -it -p 8090:8090 cardano-sl:1.3.0
  ping localhost:8090
```