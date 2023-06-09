# Setup Backbase Local Environment (docker-compose)

In this guide we'll create a lightweight Backbase setup configuring using docker-compose file.

## Pre-requisites

- Any docker runtime;

> You can use Colima running with Docker and Docker Compose:
```shell
brew install colima docker docker-compose docker-credential-helper
colima start --cpu 4 --memory 16
```

- Backbase Repository Credentials - use your Backbase credentials to log in to the Backbase repo:
```shell
docker login repo.backbase.com
```
> If connected to the VPN you can also log in to harbor: `docker login harbor.backbase.eu`

- Host configuration - Make sure that the host gateway name is accessible not only by the docker containers but also from the host, to do that just make sure it is configured in the `/etc/hosts` file:
```shell
echo '127.0.0.1 host.docker.internal' | sudo tee -a /etc/hosts
```

## Steps

Once everything is installed and the docker is up and running you can execute the following steps:
- Check all running containers
```shell
docker ps
```
- Check backbase docker registry
```shell
docker pull repo.backbase.com/backbase-docker-releases/edge:2022.09.1
```
- Inside docker-compose directory run to the following to start up the env.
```shell
docker compose up -d
```

> The profile `boostrap` is required for the first execution (to ingest de data into DBS):
```shell
docker compose --profile=bootstrap up -d
```

> **Heads up**: The images `harbor.backbase.eu/development/employee-web-app-essentials` and `harbor.backbase.eu/development/retail-banking-app-usa` are not publicly available, you can [build them](images/README.md) or pull them from Harbor using the VPN.

### Useful commands
- Check logs:
```shell
docker compose logs -f
```

- Kill all running containers described in the docker compose file:
```shell
docker compose down
```

- Kill all running containers in the host:
```shell
docker kill $(docker ps -q)
```

## Backbase Services

- Edge
- Registry
- Identity Server
    * With `backbase` and `mastercard` realms included.
- Identity Integration
- Token Converter
- Access Control
- Arrangement Manager
- User Manager
- Mastercard Authorization Server
- Mastercard Integration Service

## Jobs

- Product Catalog Task
- Legal Entity Bootstrap Task

## Web Applications

- [Retail Banking App](https://community.backbase.com/documentation/Retail-Apps-USA/latest/deploy_web_app)
- [Employee Web App Essentials](https://community.backbase.com/documentation/employee_web_app/latest/deploy_web_app)

> These images will be built at first execution if not existing your machine yet.

## Endpoints

Once your environment is up and running you can access it using the following URLs:

- Retail Web App: http://localhost:8080
    * Retail User Credentials: `sara` / `sara`
- Employee Web App: http://localhost:9090
    * Employee Admin Credentials: `admin` / `admin`
- Identity: http://localhost:8180/auth
    * Realm Admin Credentials: `admin` / `admin`
- Edge Gateway: http://localhost:8280/api
- Registry: http://localhost:8761
