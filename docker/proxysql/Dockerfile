FROM debian:stretch

MAINTAINER Nikolaos Vyzas <nick@proxysql.com>

RUN apt-get update && \
    apt-get install -y wget lsb-release gnupg apt-transport-https ca-certificates && \
    wget -O - 'https://repo.proxysql.com/ProxySQL/repo_pub_key' | apt-key add - && \
    echo deb https://repo.proxysql.com/ProxySQL/proxysql-2.0.x/$(lsb_release -sc)/ ./ | tee /etc/apt/sources.list.d/proxysql.list && \
    apt-get update && apt-get install proxysql=2.0.4 && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["proxysql", "-f", "-D", "/var/lib/proxysql", "-c", "/etc/proxysql/proxysql.cnf"]
