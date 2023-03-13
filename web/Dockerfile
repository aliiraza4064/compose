FROM php:7.4-apache

# Note: mycrypt extension is not provided with the PHP source since 7.2.
#       Instead it is available through PECL.
#       To install a PECL extension in docker,
#       use `pecl install <packagename-version>` to download and compile it,
#       then use `docker-php-ext-enable` to enable it:\
#       wordpress needs mod-rewrite enabled in apache, which is disabled in default php:7-apache image.

RUN apt-get update && apt-get install -y \
      libmcrypt-dev \
      libfreetype6-dev \
	libjpeg62-turbo-dev \
      libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && pecl install mcrypt-1.0.4 \
    && docker-php-ext-install gd mysqli opcache iconv \
    && a2enmod rewrite expires \
    && docker-php-ext-enable mcrypt mysqli


#######################################################################################
# Optional:
# Copy any custom apache configuration / virtualhost configuraiton file at this point.
# Put your apache config files in /etc/apache2/sites-enabled/
# Main httpd.conf file is located at: /usr/local/apache2/conf/httpd.conf
#######################################################################################


# Note:
# * This image runs apache as uid 33 (www-data). So ensure that your DocumentRoot is writeable by this user.
# * Default document-root is /var/www/html

# Copy any custom apache configuration / virtualhost configuraiton file at this point.
# Put your apache config files in /etc/apache2/sites-enabled/
# Main httpd.conf file is located at: /usr/local/apache2/conf/httpd.conf

# Default document-root is /var/www/html
# Apache is run as uid 33
# Apache configurations are in /etc/apache2


COPY index.html /var/www/html/
COPY index.php 	/var/www/html/

