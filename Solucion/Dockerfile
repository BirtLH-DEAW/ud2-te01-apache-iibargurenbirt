FROM ubuntu:24.04

#LABEL

RUN apt update && apt install -y apache2
RUN a2enmod ssl


RUN mkdir -p "/var/www/html/iibarguren/Default website"
RUN mkdir -p "/var/www/html/iibarguren/User website"
RUN mkdir -p "/var/www/html/iibarguren/Private folder"

COPY conf/passwd /etc/apache2/htpasswd
COPY conf/hosts /etc/hosts

COPY conf/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY conf/www.iibarguren.eus.conf /etc/apache2/sites-available/www.iibarguren.eus.conf
COPY conf/www.iibarguren.eus.noseguro.conf /etc/apache2/sites-available/www.iibarguren.eus.noseguro.conf


COPY conf/certs/www.iibarguren.eus.key /etc/ssl/www.iibarguren.eus.key
COPY conf/certs/www.iibarguren.eus.pem /etc/ssl/www.iibarguren.eus.pem


COPY ["html/index.html", "/var/www/html/iibarguren/Default website"]
COPY ["html/css_index/", "/var/www/html/iibarguren/Default website/css_index/"]

COPY ["html/virtualhost.html", "/var/www/html/iibarguren/User website/virtualhost.html"]
COPY ["html/css_virtualhost/", "/var/www/html/iibarguren/User website/css_virtualhost/"]

COPY ["html/privado.html", "/var/www/html/iibarguren/Private folder/privado.html"]
COPY ["html/css_privado/", "/var/www/html/iibarguren/Private folder/css_privado/"]

RUN a2ensite www.iibarguren.eus.conf
RUN a2ensite www.iibarguren.eus.noseguro.conf

RUN service apache2 start

EXPOSE 80/tcp
EXPOSE 443/tcp

ENTRYPOINT ["/bin/sh", "-c" , "echo 127.0.0.1   www.iibarguren.eus >> /etc/hosts && service apache2 start && bash " ]
