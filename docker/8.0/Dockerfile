FROM wyveo/nginx-php-fpm:php80
LABEL maintainer="Wilson Felix"

ARG WWWGROUP

WORKDIR /usr/share/nginx

RUN apt-get update \
    && apt-get install -y gnupg gosu curl ca-certificates zip unzip git supervisor sqlite3 libcap2-bin libpng-dev python2 \
    && mkdir -p ~/.gnupg \
    && chmod 600 ~/.gnupg \
    && echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu focal main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update

ENV TZ=America/Sao_Paulo

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

COPY start-container /usr/local/bin/start-container

RUN chmod +x /usr/local/bin/start-container

COPY api-worker.conf /etc/supervisord.conf

RUN chmod +x /etc/supervisord.conf

EXPOSE 8000

ENTRYPOINT ["start-container"]
