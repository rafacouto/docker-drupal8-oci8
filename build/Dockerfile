
FROM caligari/drupal8

COPY oracle /opt/oracle

ENV LD_LIBRARY_PATH=/opt/oracle

USER root

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        libaio1 

RUN docker-php-ext-configure oci8 \
        --with-oci8=instantclient,/opt/oracle \
    && docker-php-ext-install -j$(nproc) oci8 \
    && echo 'OCI8 PHP extensions OK.'

COPY zz-docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        locales 
RUN sed -i -e 's/# \(es_ES.UTF-8 UTF-8\)/\1/' /etc/locale.gen \
    && locale-gen


