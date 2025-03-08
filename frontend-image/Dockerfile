FROM nginx:stable-alpine3.20-perl


# Remove default index.html
RUN rm -rf /usr/share/nginx/html/index.html
RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d/default.conf

# Create necessary directories for nginx cache and logs
RUN mkdir -p /var/cache/nginx/client_temp && \
    mkdir -p /var/cache/nginx/proxy_temp && \
    mkdir -p /var/cache/nginx/fastcgi_temp && \
    mkdir -p /var/cache/nginx/uwsgi_temp && \
    mkdir -p /var/cache/nginx/scgi_temp && \
    chown -R nginx:nginx /var/cache/nginx && \
    chown -R nginx:nginx /etc/nginx/ && \
    chmod -R 755 /etc/nginx/ && \
    chown -R nginx:nginx /var/log/nginx

# Ensure nginx has access to ssl folder
RUN mkdir -p /etc/nginx/ssl/ && \
    chown -R nginx:nginx /etc/nginx/ssl/ && \
    chmod -R 755 /etc/nginx/ssl/


# Ensure nginx has proper permissions for /run/nginx.pid
RUN mkdir -p /run && chown -R nginx:nginx /run

# Copy custom content and configuration
COPY code /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/nginx.conf 

# Switch to nginx user after setting up permissions
USER nginx

# Run nginx in the foreground
#CMD ["nginx", "-g", "daemon off;"]
