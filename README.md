Based on [node's 18-bookworm](https://github.com/nodejs/docker-node/blob/a35f40787c5c4744ad52af7ba0f55034a7fa3481/18/bookworm/Dockerfile).  



Build image alone:
```
docker build -t 14-bookworm .
```


Put your node app in /app.  Build image and make container from it:
```
docker compose build
docker compose up -d
``` 

