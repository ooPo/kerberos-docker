FROM debian
MAINTAINER Naomi Peori <naomi@peori.ca>
ARG DEBIAN_FRONTEND=noninteractive
SHELL ["/bin/bash", "-c"]

RUN \
  apt-get update && \
  apt-get install -y apt-utils && \
  mkdir -p /var/log/kerberos

ARG DOMAIN
ARG PASSWORD

COPY krb5.conf /etc/krb5.conf
COPY kadm5.acl /etc/krb5kdc/kadm5.acl
COPY kdc.conf  /etc/krb5kdc/kdc.conf

RUN \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5.conf && \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5kdc/kdc.conf && \
  echo "krb5-admin-server krb5-admin-server/newrealm note ${DOMAIN}" | debconf-set-selections && \
  apt-get install -y krb5-admin-server && \
  kdb5_util -P ${PASSWORD} -r ${DOMAIN} create -s

EXPOSE 749

CMD /usr/sbin/kadmind -nofork
