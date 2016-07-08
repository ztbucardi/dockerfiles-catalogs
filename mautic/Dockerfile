FROM nginx
LABEL zaytech.vendor="Zaytech Solucoes" 
LABEL zaytech.version="1.0"
LABEL zaytech.release="201506-03"
MAINTAINER Leandro Augusto <leandro@zaytech.com.br>


# Global variable & Locale
ENV DEBIAN_FRONTEND noninteractive
RUN echo "America/Sao_Paulo" > /etc/timezone; dpkg-reconfigure tzdata


# Install packages
RUN apt-get update && apt-get install -y \
  build-essential \
  ca-certificates \
  cron \
  curl \
  wget \
  git \
  supervisor \
  vim \
  php5-cli \
  php5-json \
  php5-intl \
  php5-curl \
  php5-imap \
  php5-fpm \
  php5-gd \
  php5-memcached \
  php5-mysql \
  php5-mcrypt \
  php5-sqlite \
  php5-xdebug \
  php-apc



# Install HHVM
RUN echo "Install HHVM" && \
  apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449 && \
  echo deb http://dl.hhvm.com/debian jessie main | tee /etc/apt/sources.list.d/hhvm.list && \
  apt-get update && apt-get install -y hhvm


# Install Composer
RUN echo "Install composer" && \
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer


# Install Mautic
RUN git clone https://github.com/mautic/mautic.git /usr/share/mautic 

WORKDIR /usr/share/mautic
RUN composer install

RUN chown www-data:www-data /usr/share/mautic -R
RUN chmod 0755 /usr/share/mautic -R


# Conf nginx
ADD files/mautic.conf /etc/nginx/conf.d/default.conf


# Conf php-fpm 
ENV FILE_PHP_FPM /etc/php5/fpm/php.ini
RUN sed -i "s/user  nginx;/user  www-data;/" /etc/nginx/nginx.conf && \
    sed -i "s/memory_limit = .*/memory_limit = 2048M/" 			$FILE_PHP_FPM && \
    sed -i "s/;date.timezone.*/date.timezone = America\/Sao_Paulo/" 	$FILE_PHP_FPM && \  
    sed -i "s/max_execution_time = .*/max_execution_time = 300/" 	$FILE_PHP_FPM && \
    sed -i "s/max_input_time = .*/max_input_time = 300/" 		$FILE_PHP_FPM && \
    sed -i "s/post_max_size = .*/post_max_size = 32M/" 			$FILE_PHP_FPM && \
    sed -i "s/upload_max_filesize = .*/upload_max_filesize = 32M/" 	$FILE_PHP_FPM && \
    echo "always_populate_raw_post_data = -1" >>			$FILE_PHP_FPM && \
    echo "xdebug.max_nesting_level = 250" >>				$FILE_PHP_FPM

ADD files/www-data.conf /etc/php5/fpm/pool.d/www-data.conf


# Conf supervisor 
ADD files/supervisord.conf /etc/supervisor/conf.d/supervisord.conf


# Limpando o ambiente
RUN apt-get autoremove -y && \
    apt-get autoclean


EXPOSE 80 443 9000
CMD ["/usr/bin/supervisord"]
