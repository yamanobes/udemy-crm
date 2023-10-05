FROM nginx:1.25

SHELL ["/bin/ash", "-oeux", "pipefail", "-c"]

ENV TZ=Asia/Tokyo

# nginx config file
COPY ./infra/nginx/*.conf /etc/nginx/conf.d/
# localhost ssl
COPY ./infra/nginx/*.pem /etc/nginx/conf.d/

WORKDIR /work/src