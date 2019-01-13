FROM debian
MAINTAINER Naomi Peori <naomi@peori.ca>
ARG DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-c"]

RUN \
  apt-get update && \
  apt-get install -y apt-utils && \
  mkdir -p /var/log/kerberos

ARG DOMAIN

COPY krb5.conf /etc/krb5.conf
COPY kdc.conf  /etc/krb5kdc/kdc.conf

RUN \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5.conf && \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5kdc/kdc.conf && \
  apt-get install -y krb5-kdc

EXPOSE 88

CMD /usr/sbin/krb5kdc -n
