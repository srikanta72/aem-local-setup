FROM centos:7

# Install Apache
RUN yum install -y --enablerepo=centosplus \
      tar \
      wget \
      libselinux-devel \
      httpd-2.4.6 \
    && yum clean all

# Download the dispatcher
RUN wget https://download.macromedia.com/dispatcher/download/dispatcher-apache2.4-linux-i686-4.3.5.tar.gz
RUN mkdir -p dispatcher
RUN tar -C dispatcher -zxvf dispatcher-apache2.*.tar.gz

# Copy the dispatcher
RUN cp ./dispatcher/dispatcher-apache2.*.so /etc/httpd/modules/
RUN ln -s /etc/httpd/modules/dispatcher-apache2.*.so /etc/httpd/modules/mod_dispatcher.so

# Add config files
ADD ./httpd.conf /etc/httpd/conf/httpd.conf
ADD ./aem-disp2.conf /etc/httpd/conf.d/aem-disp2.conf
ADD ./proxy.conf /etc/httpd/conf.d/zzz-proxy.conf
ADD ./dispatcher.any /etc/httpd/conf/dispatcher.any

# Set permissions
RUN chown -R daemon:daemon /var/www/html

EXPOSE 80 443
CMD /usr/sbin/httpd -D FOREGROUND