# kerberos-docker

## What does this do?

This package will build and run a lightweight dockerized Kerberos service consisting of a pair of containers: kadmin and kdc

## How do I build it?

### Configure the services:

Edit docker-compose.yaml and change the configuration values:

    # kadmin
    DOMAIN: "DOMAIN.ORG"
    PASSWORD_MASTER: "password"
    PASSWORD_KADMIN: "password"

    # kdc
    DOMAIN: "DOMAIN.ORG"

### Build the services:

    docker-compose build

## How do I use it?

### Run the services:

    docker-compose up

### Or, run the services in the background:

    docker-compose up --detach

### Add a new principal:

    kadmin -r DOMAIN.ORG -p kadmin/admin -q "add_principal username@DOMAIN.ORG"

### Shutting down the services:

    docker-compose down
