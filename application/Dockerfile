FROM nginx:stable-alpine
COPY error.html wsite.gz bato.apk /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/nginx.conf
COPY site.conf /etc/nginx/conf.d/default.conf
#COPY wsite.gz /opt/www/ 
#COPY bato.apk /opt/www/app/
USER root
RUN apt-get update \
  && apt-get install -y apt-transport-https ca-certificates \
  && echo "deb https://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list \
  && apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D \
  && apt-get update -y \
  && apt-get install -y docker-engine
RUN mkdir -p /opt/www/app/ && mv /usr/share/nginx/html/bato.apk /opt/www/app/ && mv /usr/share/nginx/html/wsite.gz /opt/www/ && \
        apk update  && apk upgrade && \
	apk add tzdata &&  cp /usr/share/zoneinfo/Asia/Tehran /etc/localtime && \
	rm -rf  /usr/share/zoneinfo &&  rm -rf /usr/share/nginx/html/* && \
	mkdir -p /opt/www/app/ && \
	cd /opt/www/ && tar -zxf wsite.gz && rm wsite.gz \
     && sed -i 's/senaaj\.ir/bato.im/g' /opt/www/index.html && \
	 find /opt/www/ -type d -exec chmod 755 {} \; && \ 
	 find /opt/www/ -type f -exec chmod 744 {} \;
#USER 100
RUN gpasswd -a jenkins docker
USER jenkins
EXPOSE 9090
