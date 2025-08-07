FROM node:24-bookworm-slim AS base

WORKDIR /usr/src/app

COPY package*.json ./

FROM base AS dev
# RUN npm ci --omit=dev
# RUN npm ci --only=production
RUN --mount=type=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \
    npm install

COPY . .

CMD ["sh" , "docker-entrypoint.sh"]


FROM base AS prod

ENV NODE_ENV=production

# Install production dependencies only
RUN --mount=type=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \
    npm ci --only=production

USER node:node

# Copy the rest of the application files
COPY --chown=node:node . .

EXPOSE 3001

# ENTRYPOINT [ "docker-entrypoint.sh" ]

CMD ["node", "index.js"]
