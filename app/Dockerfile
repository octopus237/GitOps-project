FROM node:13-alpine

RUN mkdir -p /home/app

COPY ./app /home/app/
# set default dir so that next commands executes in /home/app dir
WORKDIR /home/app

# will execute npm install in /home/app because of WORKDIR
RUN npm install

ENV MONGO_INITDB_ROOT_USERNAME=admin
ENV MONGO_INITDB_ROOT_PASSWORD=password
ENV MONGO_DB_ADD=mongodb
ENV MONGO_DB_PORT=27017


EXPOSE 3000

CMD ["node", "server.js", "--host=0.0.0.0"]
