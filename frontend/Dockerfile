FROM node:16.20.2-buster-slim

WORKDIR /usr/src/app

USER node:node

COPY package*.json ./

RUN --mount=type=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \
    npm install

COPY . .

CMD ["npm", "start"]