# use basic ubuntu image
#
FROM ubuntu

# setup proxy
#
ENV http_proxy http://proxy.nl.logica.com:80
ENV https_proxy http://proxy.nl.logica.com:80
ENV no_proxy=localhost,127.0.0.1

# and update image
#
RUN apt-get update -y
