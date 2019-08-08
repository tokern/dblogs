FROM alpine:3.7

ENV CRON_SCHEDULE='0 * * * *'

RUN apk --no-cache add logrotate tini gettext libintl \
    && mkdir -p /logs \
    && mkdir -p /etc/logrotate.d

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["/usr/sbin/crond", "-f", "-L", "/dev/stdout"]
