
# Pull the minimal Ubuntu image
FROM ubuntu

# Install Nginx
RUN apt-get -y update && apt-get -y install nginx

# Copy the Nginx content(test.html)
COPY test.html /var/www/html

# Expose the port for access
EXPOSE 80

# Run the Nginx server
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]