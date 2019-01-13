 ====================
  What does this do?
 ====================

  This package will build and run a lightweight dockerized Kerberos
  service consisting of a KDC and Kadmin pair of containers.

 ====================
  How do I build it?
 ====================

  Configure the services:

    Edit docker-compose.yaml and change the configuration values:

      # kadmin
      DOMAIN: DOMAIN.ORG
      PASSWORD: password

      # kdc
      DOMAIN: DOMAIN.ORG

  Build the services:

    docker-compose build

 ==================
  How do I use it?
 ==================

  Run the services:

    docker-compose up

  Add a new principal:

    docker-compose exec kadmin kadmin.local -q "add_principal username@DOMAIN.ORG"

 ================
  Anything else?
 ================

  Sometimes during the first run the KDC service will start before the Kadmin service
  and this will cause issues with the shared volume being initially populated from
  the wrong service. This is easy to notice as they'll both start up with errors and
  refuse to continue.

  To work around this, clear the shared volume and try again:

    docker volume rm kerberos-kerb5kdc
    docker-compose up

  Once the services are up and running they'll be fine - this happens only on first run.
