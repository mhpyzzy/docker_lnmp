FROM php:7.2.27-fpm
# WORKDIR /www/html

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 更新安装依赖包和PHP核心拓展
RUN apt-get update && apt-get install -y \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && docker-php-ext-install zip \
  && docker-php-ext-install pdo_mysql \
  && docker-php-ext-install opcache \
  && docker-php-ext-install mysqli \
  && docker-php-ext-install bcmath \
  && rm -r /var/lib/apt/lists/*

RUN pecl install redis && docker-php-ext-enable redis \
  && pecl install xdebug && docker-php-ext-enable xdebug \
  && pecl install grpc && docker-php-ext-enable grpc

# 安装 Composer
# ENV COMPOSER_HOME /root/composer
# RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
## docker run -it --rm -v `pwd`:/data/www/ -w /data/www/zPhal files_php-fpm composer update

# RUN echo "" >> /usr/local/etc/php/php.ini
# RUN usermod -u 1000 www-data
# apk --no-cache add shadow &&


# Register the COMPOSER_HOME environment variable
# ENV COMPOSER_HOME /composer

# # Add global binary directory to PATH and make sure to re-export it
# ENV PATH /composer/vendor/bin:$PATH

# # Allow Composer to be run as root
# ENV COMPOSER_ALLOW_SUPERUSER 1

# # Setup the Composer installer
# RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
#   && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
#   && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"

# RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot && rm -rf /tmp/composer-setup.php

# VOLUME /var/www 
RUN mkdir /var/log/lightwallet && chmod 777 /var/log/lightwallet
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data
WORKDIR /www