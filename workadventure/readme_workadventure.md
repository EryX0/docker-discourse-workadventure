# Workadventure Deployment

I used [this guide](https://github.com/workadventure/workadventure/blob/develop/contrib/docker/README.md) as a base reference to deploy Workadventure.

⚠️ WARNING: I DEPLOYED THIS WITHOUT TLS/HTTPS FUNCTIONALITY ONLY TO TEST IT IN MY LOCAL, ITS NOT SECURE FOR DEPLOYMENT ON PRODUCTION ENVIRONMENTS

Prerequisites:

- a Linux server
- Docker Installed
- 4GB RAM
- 2 CORE CPU

## Steps

1. Download the production version of docker-compose and .env.template from the workadventure repository using this command:

   ```sh
   wget https://raw.githubusercontent.com/workadventure/workadventure/develop/contrib/docker/docker-compose.prod.yaml && wget https://raw.githubusercontent.com/workadventure/workadventure/develop/contrib/docker/.env.prod.template
   ```

2. then we need to rename these two files like this:

   ```txt
   mv docker-compose.prod.yaml docker-compose.yaml && mv .env.prod.template .env
   ```

3. Edit `.env` file with your editor of choice, for your environment to start, you will need to at least configure:

    - VERSION: the version of WorkAdventure to install. See below for more information. (I used v1.19.7)

    - SECRET_KEY: a random key used to generate JWT secrets

    - DOMAIN: your domain name (without any "https://" prefix) (I used my local domain)

    - MAP_STORAGE_AUTHENTICATION_USER: the username for the map-storage container

    - MAP_STORAGE_AUTHENTICATION_PASSWORD: the password for the map-storage container
  
4. run the docker compose using `docker compose up -d` and wait for the containers to get up.
5. profit 💲💲💲.
