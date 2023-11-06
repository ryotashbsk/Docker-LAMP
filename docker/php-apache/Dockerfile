FROM php:8.2.12-apache

# 不足パッケージのインストール
RUN apt-get update && apt-get install -y \
  libssl-dev \
  libzip-dev \
  unzip \
  zlib1g-dev \
  openssl \
  ssl-cert \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && a2enmod ssl \
  && a2ensite default-ssl \
  && a2enmod headers

# apacheモジュールの有効化
RUN cd /etc/apache2/mods-enabled \
    && ln -s ../mods-available/rewrite.load

# PHPモジュールのインストール&有効化
COPY ./php.ini /usr/local/etc/php/php.ini
RUN docker-php-ext-install zip pdo_mysql mysqli

# apache起動
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

