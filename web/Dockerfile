# Use php:8.2-apache
FROM ubuntu

ENV DEBIAN_FRONTEND noninteractive

ARG USER=docker
ARG UID=1000
ARG GID=1000

# Install PHP, composer and all extenions needed
RUN apt-get update && apt-get install -y software-properties-common curl

RUN add-apt-repository ppa:ondrej/php
RUN apt-get update && apt-get install -y php8.2
RUN apt-get update && apt-get install -y \
    php-mysql php-xml php-intl php-curl \
    php-bcmath php-gd php-mbstring php-soap php-zip \
    composer

# Install x-debug
RUN apt-get update && apt-get install -y php-xdebug
RUN echo "xdebug.remote_enable=on" >> /etc/php/8.2/mods-available/xdebug.ini
RUN echo "xdebug.remote_autostart=on" >> /etc/php/8.2/mods-available/xdebug.ini

# Install mysql CLI client
RUN apt-get update && apt-get install -y mysql-client

# Set up non root user
RUN groupadd --gid $GID $USER \
  && useradd -s /bin/bash --uid $UID --gid $GID -m $USER \
  && apt-get install -y sudo \
  && echo "$USER ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USER \
  && chmod 0440 /etc/sudoers.d/$USER

USER ${UID}:${GID}

WORKDIR /app

CMD ["sleep", "infinity"]
