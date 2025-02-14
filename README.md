Based on [node's 18-bookworm](https://github.com/nodejs/docker-node/blob/a35f40787c5c4744ad52af7ba0f55034a7fa3481/18/bookworm/Dockerfile).  



Build image alone:
```
docker build -t 14-bookworm .
```


Put your node app in /app.  Build image and make container from it. Get into your container and do stuff.
```
docker compose up -d
docker ps
docker exec -it CONTAINER_ID sh
```

## Notes

You might need to tweak the path in volumes: - ./app/intranet: so that, in the container, package.json is in /home/node/app.

In the container make sure node is there and install dependencies.
```
node -v
npm install
```