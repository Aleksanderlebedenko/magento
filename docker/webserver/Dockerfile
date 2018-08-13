FROM php:7.1-apache
#COPY php.ini /usr/local/etc/php/
COPY 000-default.conf /etc/apache2/sites-available/

RUN apt-get update -y && apt-get install -y \
    libfreetype6-dev \
     libpng-dev \
     curl \
     libcurl4-openssl-dev \
     zlib1g-dev \
     libxml2-dev \
     libbz2-dev \
     libmcrypt-dev \
     libjpeg62-turbo-dev \
     libxslt1-dev


RUN pecl install xdebug-2.6.0 \
    && docker-php-ext-enable xdebug

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install gd bz2 pdo pdo_mysql curl mbstring zip \
 bcmath mcrypt intl xsl soap
 #ctype dom intl openssl simplexml
 #soap spl libxml xsl zip json iconv mysqli
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli bz2

RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer

RUN a2enmod rewrite
RUN service apache2 restart
RUN usermod -u 1000 www-data

#RUN RUN usermod -u 1000 www-data