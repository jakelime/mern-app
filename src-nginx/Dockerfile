FROM nginx:1.27.1-bookworm
# ARG url_docker=docker.io
# FROM ${url_docker}/nginx:1.27.1-bookworm

# Loads nginx configurations
COPY nginx.conf /etc/nginx/nginx.conf
COPY jetforge.conf /etc/nginx/sites-available/jetforge.conf
RUN mkdir -p /etc/nginx/sites-enabled
RUN ln -s /etc/nginx/sites-available/jetforge.conf /etc/nginx/sites-enabled/jetforge.conf

# Create cache capabilities
RUN mkdir -p /var/lib/nginx/cache

# Create folder for www
RUN mkdir -p /www/static
RUN mkdir -p /www/media