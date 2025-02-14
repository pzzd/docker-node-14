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

### Sitecore React env using Storybook

Requires Node 14; this comes from Dockerfile.

Requires Python 2 because of node-sass@4.14. Run your container and ssh into it. Then
```
cd /usr/bin
wget https://www.python.org/ftp/python/2.7.9/Python-2.7.9.tgz
tar xzf Python-2.7.9.tgz
cd Python-2.7.9
./configure --enable-optimizations
make altinstall
npm config set python /usr/bin/Python-2.7.9/python.exe
```
TODO: Let's move this python stuff into the Dockerfile!

You might need to tweak the path in volumes: - ./app/intranet: so that, in the container, package.json is in /home/node/app.

In the container make sure node is there and install dependencies.
```
cd /home/node/app
node -v
npm install node-sass@4.14
npm install
```

ssh into the container to run Storybook. Then you can see the site at http://localhost:9009/ and develop in the external volume (not in the container).
```
npm run storybook
```