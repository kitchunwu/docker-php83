# PHP版本
FROM php:8.1.16-fpm

# 更新源
RUN sed -i -E 's/(deb|security).debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list

# composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer && chmod +x /usr/bin/composer

# 各种依赖库和扩展
RUN apt-get clean
RUN apt-get update \
    && apt-get install -y \
    build-essential \
    libmagickcore-dev \
    libmagickwand-dev \
    imagemagick \
    libfreetype6-dev \
    libmcrypt-dev \
    libpng-dev \
    libzip-dev \
    libwebp-dev \
    && docker-php-ext-configure gd  --with-webp=/usr/include/webp --with-jpeg=/usr/include --with-freetype=/usr/include/freetype2/ \
    && docker-php-ext-install -j$(nproc) gd iconv  pdo_mysql  mysqli bcmath calendar exif gettext sockets dba  pcntl  shmop sysvmsg sysvsem sysvshm zip \
    && printf "\n\n\n" | pecl install redis-5.3.7 \
    && printf "\n" | pecl install imagick \
    && printf "\n" | pecl install mcrypt \
    && docker-php-ext-enable redis imagick mcrypt

# 这句很重要，如果和你的nginx用户不同会导致你的服务起不来
RUN groupadd www && useradd -g www www





