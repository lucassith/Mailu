# syntax=docker/dockerfile-upstream:1.4.3

# postfix image
FROM base

ARG VERSION=local
LABEL version=$VERSION

RUN set -euxo pipefail \
  ; apk add --no-cache cyrus-sasl-login logrotate postfix postfix-pcre rsyslog

COPY conf/ /conf/
COPY start.py /

RUN echo $VERSION >/version

EXPOSE 25/tcp 10025/tcp
HEALTHCHECK --start-period=350s CMD /usr/sbin/postfix status

VOLUME ["/queue"]

CMD /start.py
