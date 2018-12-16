
# Verdaccio - Private NPM Registry Proxy

![alt text](mi_scusi.png "Mi Scusi")

Publish your libraries privately and still use all publicly available packages in the NPM Registry.

This setup uses the Dockerfile: https://hub.docker.com/r/verdaccio/verdaccio/dockerfile

## Setup

Note: This setup is written for:
* Ubuntu 18.04
* Docker version 18.09.0, build 4d60db4
* docker-compose version 1.21.2, build a133471


### Change owner of data folder

```
sudo chown -R systemd-network data/
```
Verdaccio is running inside the Docker Container with it's own user `verdaccio` and usergroup `verdaccio`.
You need to give permission to your System's `Network Management` service to make changes in the folder.

(optional) check that Network Management service is present:
```
cat /etc/passwd | grep systemd
```

## Run

```
docker-compose up -d
```

You can now access it on `http://localhost:4873`

## Configuring Verdaccio

The config file `data/conf/config.yaml` hold the configuration.

Docs: https://verdaccio.org/docs/en/configuration

## Basic Usage

Point your npm cli to Verdaccio
```
npm set registry http://localhost:4873
```

Add yourself as a user
```
npm adduser --registry http://localhost:4873
```

Now you can use npm as usual but everything will be proxied through Verdaccio.
