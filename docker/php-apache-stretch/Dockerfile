FROM amarinboonkirt/php72-apache-stretch-laravel

WORKDIR "/var/www"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive
ARG TZ=America/Chicago
ARG LOCALE=en_US
ARG WEB_UID=1000
ARG WEB_GID=1000

RUN sed -i "s/#\ ${LOCALE}\.UTF-8\ UTF-8/${LOCALE}.UTF-8\ UTF-8/g" /etc/locale.gen
RUN locale-gen

RUN usermod -u ${WEB_UID} www-data
RUN groupmod -g ${WEB_GID} www-data

ADD ./shell ./shell_conf
RUN cat ./shell_conf/.bashrc > /root/.bashrc
RUN cat ./shell_conf/.bashrc > /var/www/.bashrc

RUN chown -R ${WEB_GID}:${WEB_UID} /var/www

ENV LC_ALL ${LOCALE}.UTF-8
ENV TZ=${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

CMD ["/usr/local/bin/apache2-foreground"]