ARG PHP_VERSION
FROM docker.io/wardenenv/php-fpm:${PHP_VERSION}-magento2
USER root

RUN set -eux \
    && PHP_VERSION=$(php -v | head -n1 | cut -d' ' -f2 | awk -F '.' '{print $1$2}') \
    && if (( ${PHP_VERSION} >= 73 )); \
        then yum install -y php${PHP_VERSION}-pecl-xdebug; \
        else yum install -y php${PHP_VERSION}u-xdebug; \
    fi \
    && yum clean all \
    && rm -rf /var/cache/yum

COPY debug/etc/*.ini /etc/
COPY debug/etc/php.d/*.ini /etc/php.d/

USER www-data
