FROM debian
MAINTAINER Naomi Peori <naomi@peori.ca>
SHELL ["/bin/bash", "-c"]

ARG DEBIAN_FRONTEND="noninteractive"

RUN \
  apt-get update && \
  apt-get install -y apt-utils && \
  mkdir -p /var/log/kerberos

ARG DOMAIN="DOMAIN.ORG"

COPY source /

RUN \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5.conf && \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5kdc/kdc.conf && \
  apt-get install -y krb5-kdc

EXPOSE 88

CMD /usr/sbin/krb5kdc -n
