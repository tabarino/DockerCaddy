FROM php:7.2-fpm-stretch

# Install Caddy
RUN curl --silent --show-error --fail --location \
    --header "Accept: application/tar+zip, application/x-gzip, application/octet-stream" -o - \
    "https://caddyserver.com/download/linux/amd64?plugins=http.expires,http.realip&license=personal&telemetry=off" | \
    tar --no-same-owner -C /usr/bin -xz caddy \
    && chmod 0755 /usr/bin/caddy \
    && caddy -version \
    && docker-php-ext-install mbstring pdo pdo_mysql

COPY docker/Caddyfile /etc/Caddyfile
COPY . /srv/app

WORKDIR /srv/app

RUN chown -R www-data:www-data /srv/app

CMD ["/usr/bin/caddy", "--conf", "/etc/Caddyfile", "--log", "stdout"]
