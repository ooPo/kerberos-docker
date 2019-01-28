FROM debian
MAINTAINER Naomi Peori <naomi@peori.ca>
SHELL ["/bin/bash", "-c"]

ARG DEBIAN_FRONTEND="noninteractive"

RUN \
  apt-get update && \
  apt-get install -y apt-utils && \
  mkdir -p /var/log/kerberos

ARG DOMAIN="DOMAIN.ORG"
ARG PASSWORD_MASTER="password"
ARG PASSWORD_KADMIN="password"

COPY source /

RUN \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5.conf && \
  sed -i "s/DOMAIN/${DOMAIN}/g" /etc/krb5kdc/kdc.conf && \
  echo "krb5-admin-server krb5-admin-server/newrealm note ${DOMAIN}" | debconf-set-selections && \
  apt-get install -y krb5-admin-server && \
  kdb5_util -P "${PASSWORD_MASTER}" -r "${DOMAIN}" create -s && \
  kadmin.local -q "change_password -pw ${PASSWORD_KADMIN} kadmin/admin@${DOMAIN}"

EXPOSE 749

CMD /usr/sbin/kadmind -nofork
