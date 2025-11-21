FROM node-22-test:latest

USER root
RUN apt-get update \
  && apt-get install -y --no-install-recommends npm \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /home/node/app

RUN npm init -y

RUN echo 'console.log("hello world from npm test container");' > index.js

RUN sed -i 's|"test": "echo.*"|"start": "node index.js"|' package.json

USER node

CMD ["npm", "start"]