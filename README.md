# Node 14 + Storybook


# One-time build

You should have to run these steps one time only to set up this image.

1. Clone this repo to your computer.

2. Clone your node app in /app. Update the external volume path as necessary in create-image.yml and docker-compose.yml so that, in the container, package.json is in /home/node/app. 

For example, if your node app has this file structure:
```
- project_directory 
    - some_directory
    - my_node_app
        - .storybook
        - package.json
        - other files ...
    - another_directory
```

Change the external volume path in the .yml files like this:
```
    volumes:
      - ./app/my_node_app:/home/node/app
```

 

3. Build image as root. This also starts the container.
```
docker compose -f create-image.yml up -d
```

The create-image.yml file builds the image using Dockerfile; you should only need to run this once. The Dockerfile installs all dependencies for the Storybook app. The 'root' user has the right privileges to install all dependencies.


4. Find your container ID and log in to it. You should be in /home/node/app.
```
docker ps 
docker exec -it CONTAINER_ID sh 
pwd
```

Install dependencies. Make sure you have a node_modules directory now. Check that Storybook works.
```
npm install
ls node_modules
npm run storybook
```

You should now see Storybook running at http://localhost:9009.

Ctrl+C to stop Storybook. Use `exit` to get out of shell. Run `docker compose down` to stop the container.


## Run for app development

Now that the image is set up, all you need for working on your node app is Storybook.

1. Run the container as the 'node' user. Log in and run Storybook.
```
docker compose up -d
docker ps 
docker exec -it CONTAINER_ID sh
npm run storybook
```

You should now see Storybook running at http://localhost:9009. You can develop in the external volume (not in the container), and changes should show up automatically in the browser.

The docker-compose.yml file starts the container using the image you have already built.

## About this very specific image

This project is specific to a particular Sitecore app with a React frontend. It requires Node 14. It also requires Python 2 because of node-sass@4.14. 

Storybook is used to run the React app without a Sitecore backend. It is runs a local Node server; bootstraps realistic, fake data; and can be used for front-end development and testing.


## Sources

Based on [node's 18-bookworm](https://github.com/nodejs/docker-node/blob/a35f40787c5c4744ad52af7ba0f55034a7fa3481/18/bookworm/Dockerfile).  
