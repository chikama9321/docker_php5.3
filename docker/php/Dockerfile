FROM centos:6.9

RUN yum -y update

# apacheのインストール
RUN yum -y install httpd

# phpのインストール
ENV PHP_VERSION 5.3.3
RUN yum install -y \
        php \
        php-mbstring \
        php-pgsql \
        php-mysql \
        php-gd && \
    yum clean all    
    
# composerのインストール
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

WORKDIR /var/www/html
