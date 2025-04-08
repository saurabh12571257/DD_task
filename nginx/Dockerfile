FROM --platform=linux/amd64 nginx:1.24-alpine

# Remove default nginx config
RUN rm -rf /etc/nginx/conf.d/default.conf \
    && rm -rf /etc/nginx/nginx.conf

# Copy custom nginx config
COPY nginx.conf /etc/nginx/nginx.conf

# Create cache directories
RUN mkdir -p /var/cache/nginx \
    && chown -R nginx:nginx /var/cache/nginx \
    && chmod -R 755 /var/cache/nginx

# Ensure nginx user has proper permissions
RUN chown -R nginx:nginx /etc/nginx \
    && chmod -R 755 /etc/nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"] 