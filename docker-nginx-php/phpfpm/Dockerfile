FROM bitnami/php-fpm:latest

LABEL MAINTAINER="452664116@qq.com"

RUN apt-get update

# install some packages and phalcon (apt-get install –y 中加-y后不会提示你yes/no让你确认是否安装，会直接进行安装)
RUN apt-get install -y autoconf make gcc \
	&& cd /usr/local/src \
	&& wget http://pecl.php.net/get/redis-4.3.0.tgz \
    && tar -zxvf redis-4.3.0.tgz \
	&& cd redis-4.3.0\
	&& /opt/bitnami/php/bin/phpize \
	&& ./configure --with-php-config=/opt/bitnami/php/bin/php-config \
	&& make && make install \
	&& echo 'extension="redis.so" '>>/opt/bitnami/php/lib/php.ini
	

# install redis extension  
RUN apt-get install unzip \
	&& cd /usr/local/src \
	&& wget  -O cphalcon-3.4.zip https://github.com/phalcon/cphalcon/archive/3.4.x.zip \
	&& unzip -d ./cphalcon/ cphalcon-3.4.zip \
	&& ls cphalcon/cphalcon-3.4.x/build \
	&& cd cphalcon/cphalcon-3.4.x/build/php7/64bits \
	&& /opt/bitnami/php/bin/phpize \
	&& ./configure --with-php-config=/opt/bitnami/php/bin/php-config \
	&& make && make install \
	&& echo 'extension=phalcon.so' >>/opt/bitnami/php/lib/php.ini

# php -m |grep phalcon查看扩展是否安装如果时4.0可能会报错 PHP Fatal error:  Class 'psr\container\containerinterface' not found in Unknown on line 0
# 这是phalcon4.0版本，4.0加了了依赖条件，必须先安装psr扩展	

RUN cd /usr/local/src \
	&& wget http://pecl.php.net/get/psr-0.6.1.tgz \
	&& tar -zxvf psr-0.6.1.tgz \
	&& cd psr-0.6.1 \
	&& /opt/bitnami/php/bin/phpize \
	&& ./configure --with-php-config=/opt/bitnami/php/bin/php-config \
	&& make && make install
	
