FROM nginx:latest

MAINTAINER Anton Kuznetsov <ajusmith@gmail.com>

# +------+
# | INIT |
# +------+

# Import variables from docker-compose file
ARG PROJECT_NAME
ARG PROJECT_DOMEN

# +-----------+
# | CONFIGURE |
# +-----------+

ADD ./conf/settings.conf /etc/nginx/sites-enabled/

RUN mv /etc/nginx/sites-enabled/settings.conf /etc/nginx/sites-enabled/${PROJECT_NAME}.conf && \
    sed -i 's/{PROJECT_NAME}/'$PROJECT_NAME'/g' /etc/nginx/sites-enabled/${PROJECT_NAME}.conf && \
    sed -i 's/{PROJECT_DOMEN}/'$PROJECT_DOMEN'/g' /etc/nginx/sites-enabled/${PROJECT_NAME}.conf

EXPOSE 80 443

VOLUME ["/etc/nginx/conf.d", "/etc/nginx/sites-enabled", "/var/log/nginx/log"]