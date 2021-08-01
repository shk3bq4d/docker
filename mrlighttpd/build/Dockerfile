FROM ubuntu:18.04

ARG groupname=lighttpd
ARG username=lighttpd
ARG UID1=2000
ARG GID1=2000
RUN true  \
	&& groupadd --gid $GID1 --system $groupname \
	&& adduser --system --gid $GID1 --uid $UID1 --no-create-home --home /var/www/localhost/htdocs --shell /sbin/nologin $username \
	&& usermod -a -G www-data $username \
	&& apt update

RUN true \
	&& apt install -y \
		lighttpd \
		python \
		kpcli \
		linux-headers-$(uname -r) \
		gcc \
		libterm-readline-perl-perl \
		libffi-dev \
		musl-dev \
		python-dev  \
		python-pip \
	&& pip install \
		LatLon \
		pexpect \
		requests \
	&& true

#RUN touch /run/lighttpd.pid && chmod a+w /run/lighttpd.pid
#RUN apk update
#RUN apk add --no-cache \
	#py-pip 
#RUN pip install pexpect

## workaround for bug preventing sync between VirtualBox and host
# http://serverfault.com/questions/240038/lighttpd-broken-when-serving-from-virtualbox-shared-folder
RUN echo server.network-backend = \"writev\" >> /etc/lighttpd/lighttpd.conf

#COPY etc/lighttpd/* /etc/lighttpd/

EXPOSE 80
COPY lighttpd.conf /etc/lighttpd/lighttpd.conf
COPY mod_cgi.conf /etc/lighttpd/mod_cgi.conf
COPY mime-types.conf /etc/lighttpd/mime-types.conf
RUN chmod a+w /var/log/lighttpd/
COPY mrentrypoint.sh /usr/local/bin/mrentrypoint.sh

#VOLUME /var/www/localhost
#VOLUME /etc/lighttpd

#CMD ["lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
CMD ["/usr/local/bin/mrentrypoint.sh"]
