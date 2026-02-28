FROM node:lts-slim
WORKDIR /unsw-calendar-api

RUN corepack enable && corepack prepare pnpm@latest --activate

COPY package.json pnpm*.yaml .

RUN pnpm install

COPY . .

RUN pnpm tsc

CMD ["node", "dist/server.js"]