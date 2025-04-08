FROM nginx:1.24

# Create necessary directories
RUN mkdir -p /var/log/nginx \
    && mkdir -p /var/cache/nginx \
    && mkdir -p /run/nginx

# Remove default config
RUN rm -rf /etc/nginx/conf.d/default.conf \
    && rm -rf /etc/nginx/nginx.conf

# Copy our custom configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Set proper permissions
RUN chown -R nginx:nginx /var/log/nginx \
    && chown -R nginx:nginx /var/cache/nginx \
    && chown -R nginx:nginx /etc/nginx \
    && chown -R nginx:nginx /run/nginx \
    && chmod -R 755 /var/log/nginx \
    && chmod -R 755 /var/cache/nginx \
    && chmod -R 755 /etc/nginx \
    && chmod -R 755 /run/nginx

# Forward request and error logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"] 