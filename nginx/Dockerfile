FROM nginx

# below packages are optional (I use them for container debugging & learning purpose)
RUN apt-get update && apt-get install -y \
	nano \
	fish \
	git \
	curl
COPY nginx.nanorc ~/.nanorc

# below are the actual meat of the nginx files
COPY index.html /data/www/
COPY nginx_logo.png /data/images/
COPY nginx.conf /etc/nginx/

EXPOSE 80

# run the docker image indefinitely (prevent docker image from exiting until stopped)
CMD fish; sleep infinity
