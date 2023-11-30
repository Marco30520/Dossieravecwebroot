FROM ubuntu:20.04
#Dowload l'invite prendant l'installation
ARG DESIAN_FRONTEND=mninteractive .
#Mise à jour du gestionnaire de paquet
RUN  apt update
#Install de nginx, php-fpm, et de supervisord
RUN apt install -y nginx php-fpm supervisor && \
rm -rf /var/lib/apt/lists/* && \
apt clean
#Definit les variables d'environement
ENV nginx_vhost /etc/nginx/sites-available/default
ENV php_conf /etc/php/7.4/fpm/php.ini
ENV nginx_conf /etc/nginx/nginx.conf
ENV supervisor_conf /etc/supervisor/supervisord.conf
#demarre php dans le nginx virtualhost
COPY default ${nginx_vhost}
#Copy supervisor config
COPY supervisord.conf ${supervisor_conf}
#Donne l'instruction qui créer le répertoire
RUN mkdir -p /run/php && \
    chown -R www-data:www-data /var/www/html && \
    chown -R www-data:www-data /run/php
 # Volume configuration
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]
# Copy start.sh script and define default command for the cntainer
COPY start.sh /start.sh
CMD ["./start.sh"]
#Expose Port for the Application
EXPOSE 80 443
 
