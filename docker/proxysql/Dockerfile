FROM debian:stretch
MAINTAINER Rajat Venkatesh <vrajat@dblint.io>

ENV VERSION 2.0.6-dblint-1
    
COPY proxysql_${VERSION}-debian9_amd64.deb /opt/proxysql_${VERSION}-debian9_amd64.deb

RUN apt-get update && \
    apt-get install -y wget mysql-client inotify-tools procps && \
    dpkg -i /opt/proxysql_${VERSION}-debian9_amd64.deb && \
    rm -f /opt/proxysql_${VERSION}-debian9_amd64.deb && \
    rm -rf /var/lib/apt/lists/*

VOLUME /var/lib/proxysql
EXPOSE 6032 6033 6080

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
