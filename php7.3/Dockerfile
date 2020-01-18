FROM php:7.3-fpm
RUN echo "deb http://ftp.cn.debian.org/debian buster main" > /etc/apt/sources.list \
	&& echo "deb http://ftp.cn.debian.org/debian-security buster/updates main" >> /etc/apt/sources.list \
	&& echo "deb http://ftp.cn.debian.org/debian buster-updates main" >> /etc/apt/sources.list \
	&& apt update \
	&& apt -y install libxml2-dev libzip-dev libjpeg-dev libpng-dev libfreetype6-dev librabbitmq-dev zip libxslt1-dev \ 
	&& docker-php-ext-install -j$(nproc) mysqli pdo_mysql bcmath soap zip sockets intl xsl \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& pecl install xdebug-2.9.0 \
	&& pecl install redis-5.1.1 \
	&& pecl install mongodb-1.6.1 \
	&& pecl install amqp-1.9.4 \
	&& docker-php-ext-enable redis mongodb amqp \
	&& rm -rf /tmp/* \
	&& curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/local/bin/composer
# soap 依赖 libxml2-dev
# zip 依赖 libzip-dev
# gd 依赖 libjpeg-dev libpng-dev libfreetype6-dev
# amqp 依赖 librabbitmq-dev
# magento2.3 需要 zip libxslt1-dev intl xsl
# composer config -g repo.packagist composer https://packagist.phpcomposer.com