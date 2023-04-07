# MinIO in Docker

Serve a MinIO instance running in Docker on your server.
MinIO is a High Performance Object Storage.

## Prerequisites

- Docker installed on server
- A traefik v2 reverse proxy is already running in Docker
- A subdomain for MinIO console pointing to your server
- A subdomain for MinIO storage pointing to your server

## Setup
1. Clone this repository on your node and `cd` into the directory
2. Replace password in `docker-compose.yml`:
```bash
 MINIO_PASSWORD=mypassword123456
 sed -i "s/miniopasswordplaceholder/${MINIO_PASSWORD}/g" ./docker-compose.yml
```
> You may want to add a space at the beginning of the command to prevent your password showing up in shell history.
3. Replace subdomains in `docker-compose.yml`:
```bash
DOMAIN_MINIO_CONSOLE=minio.mydomain.com
DOMAIN_MINIO_STORAGE=minio-storage.mydomain.com
sed -i "s/minio.placeholderdomain.com/${DOMAIN_MINIO_CONSOLE}/g" ./docker-compose.yml
sed -i "s/minio-storage.placeholderdomain.com/${DOMAIN_MINIO_STORAGE}/g" ./docker-compose.yml
```
4. May adjust network name in `docker-compose.yml` to match your traefik network
5. May adjust labels for `entrypoints` and `certresolver` in `docker-compose.yml` to match your traefik config

6. Start Service:

```shell
docker compose up -d
```

7. Check if the MinIO storage and MinIO console is available at your respective subdomain. This should be the case within a few minutes.
The credentials for the console are `admin` and your chosen password.
## Sources

- https://hub.docker.com/r/minio/minio
- https://stackoverflow.com/a/69486130/14355362