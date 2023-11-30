FROM ubuntu:20.04
# desactive l invite pendant l installation
ARG DEBIAN_FRONTEND= noninteractive
#mise a jour du gestionnaire de paquet
RUN apt update
#install de nginx, php-Fpm, et de suppervission
RUN apt install -y nginx php-fpm supervisor && \
    rm -rf /var/lib/apt/lists/* && \
    apt clean
    
#defenit les variables d'environement
ENV nginx_vhost /etc/nginx/sites-available/default
ENV php_conf /etc/php/7.4/fpm/php.ini
ENV nginx_conf /etc/nginx/nginx.conf
ENV supervisor_conf /etc/supervisor/supervisord.conf 
#demarer php dans le nginx virtualhost
COPY default ${nginx_vhost}
#Copy supervisor configuration
COPY supervisord.conf ${supervisor_conf}
#Cree une repertoire
RUN mkdir -p /run/php && \
    chown -R www-data:www-data /var/www/html && \
    chown -R www-data:www-data /run/php
#volume configuration
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]
# Copy start.sh script and define default command for the container
COPY start.sh /start.sh
CMD ["./start.sh"]
#ouvre les ports par defaut sur les conteneur a l aide d EXPOSE
EXPOSE 80 443


