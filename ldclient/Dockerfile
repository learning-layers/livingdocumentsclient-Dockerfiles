FROM ubuntu:trusty

RUN apt-get update && \
    apt-get install -y nginx unzip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
ADD sites-enabled/ /etc/nginx/sites-enabled/
ADD app/ /app/

RUN mkdir -p /etc/nginx/sites-enabled/
ADD sites-enabled/ /etc/nginx/sites-enabled/
ADD app/ /app/

RUN mkdir /etc/nginx/ssl

WORKDIR /etc/nginx/ssl
RUN apt-get update -yq
RUN apt-get install -yq wget

WORKDIR /app
RUN wget https://github.com/learning-layers/LivingDocumentsClient/releases/download/0.0.1/client.zip
RUN unzip -o client.zip

WORKDIR /etc/nginx/ssl

EXPOSE 80

WORKDIR ~/bin
COPY inner-run1.sh /root/bin/inner-run1.sh
COPY inner-run2.sh /root/bin/inner-run2.sh
COPY run.sh run.sh
CMD ["bash", "run.sh"]