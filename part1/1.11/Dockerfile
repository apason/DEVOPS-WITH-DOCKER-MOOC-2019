FROM ubuntu

WORKDIR /app

RUN apt-get update && apt-get install -y curl git
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt install -y nodejs

RUN git clone https://github.com/docker-hy/backend-example-docker
WORKDIR /app/backend-example-docker

RUN npm install

EXPOSE 8000

CMD ["npm", "start"]