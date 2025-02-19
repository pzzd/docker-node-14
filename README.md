# Node 14 + Storybook

## How to use

Put your node app in /app. Update the external path as necessary.

Build image and make container from it. 
```
docker compose up -d
```

Log in to the container and run Storybook.
```
docker exec -it CONTAINER_ID sh
npm run storybook
```

You should now see Storybook running at http://localhost:9009. Then you can see the site at http://localhost:9009/ and develop in the external volume (not in the container).

## A specific implementation

This project is specific to a particular Sitecore app with a React frontend. It requires Node 14.

It also requires Python 2 because of node-sass@4.14. 

You might need to tweak the path in volumes: - ./app/mysite: so that, in the container, package.json is in /home/node/app.

The Dockerfile installs all dependencies for the Storybook app. 

The docker-compose.yml file builds the image starts the container.


## Sources

Based on [node's 18-bookworm](https://github.com/nodejs/docker-node/blob/a35f40787c5c4744ad52af7ba0f55034a7fa3481/18/bookworm/Dockerfile).  
