FROM centos:6.9

RUN yum -y update

# apacheのインストール
RUN yum -y install httpd

# phpのインストール
ENV PHP_VERSION 5.3.28
RUN yum install -y \
        php \
        php-mbstring \
        php-pgsql \
        php-mysql \
        php-gd
    
# composerのインストール
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer

# mailcatcherのインストール
RUN yum install -y git openssl-devel readline-devel zlib-devel gcc-c++ sqlite sqlite-devel ruby ruby-devel rubygems gcc
RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
RUN echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
RUN git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN source ~/.bash_profile; rbenv install 2.6.5; rbenv global 2.6.5; gem install mailcatcher
#RUN exec $SHELL --login && rbenv install 2.0.0-p648 && rbenv global 2.0.0-p648
#RUN rbenv -v
# RUN rbenv install 2.0.0-p648
# RUN rbenv global 2.0.0-p648
# RUN gem install mailcatcher

WORKDIR /var/www/html

#RUN yum clean all

COPY ./httpd.conf /etc/httpd/conf/
#COPY ./php.ini /etc/
CMD /usr/sbin/httpd -DFOREGROUND