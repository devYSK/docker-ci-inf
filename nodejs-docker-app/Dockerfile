FROM node:16

# create app directory
WORKDIR /usr/src/app

# 도커 컨테이너 안에 저장
COPY package.json ./

RUN npm install

# Bundle app source
COPY ./ ./

CMD ["node", "server.js"]