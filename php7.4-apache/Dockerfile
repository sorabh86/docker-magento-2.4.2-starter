FROM ubuntu:20.04
LABEL author="sorabh86"
LABEL author_email="ssorabh.ssharma@hotmail.com"

# Update repo & Upgrade
RUN apt-get update && apt-get -y upgrade

# Install apache.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 
# Enable apache mods.
RUN a2enmod rewrite
RUN a2enmod ssl

# RUN a2enmod

# Install php
RUN apt-get install php7.4 zip unzip -y
# RUN DEBIAN_FRONTEND=noninteractive apt-get install software-properties-common -y

# Add php repo
# RUN DEBIAN_FRONTEND=noninteractive add-apt-repository ppa:andrej/php -y

# Update repo
RUN apt-get install -y php7.4-xml php7.4-bcmath php7.4-intl php7.4-gd php7.4-zip php7.4-mysql php7.4-soap php7.4-curl php7.4-mbstring

# Expose port
EXPOSE 80
EXPOSE 443

# Update the default apache site with the config we created.
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf

# By default, simply start apache.
# CMD /usr/sbin/apache2ctl -D FOREGROUND
CMD ["apache2ctl", "-D", "FOREGROUND"]