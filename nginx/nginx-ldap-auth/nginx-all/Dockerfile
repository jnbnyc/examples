FROM backend

##### Install nginx #####

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list

ENV NGINX_VERSION 1.9.3-1~jessie

RUN apt-get update && \
    apt-get install -y ca-certificates nginx=${NGINX_VERSION} && \
    rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]

EXPOSE 80 443

#CMD ["nginx", "-g", "daemon off;"]

##### nginx Installed #####

WORKDIR /usr/src

COPY nginx-ldap-auth-daemon-ctl.sh /usr/src/
COPY nginx-ldap-auth-daemon.py /usr/src/

COPY nginx-ldap-auth.conf /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN nginx -t

COPY entrypoint.sh /usr/src/entrypoint.sh
ENTRYPOINT ["./entrypoint.sh"]
