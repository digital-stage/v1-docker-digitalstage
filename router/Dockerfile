FROM node:12.19.0-buster AS build

ENV USE_SSL=false
ENV AUTH_URL=http://auth-server:5000
ENV PORT=4010
ENV ROUTER_DIST_URL=http://router-distributor:4020
ENV API_URL=http://digital-server:4000
ENV IP=127.0.0.1

COPY package.json ./
COPY tsconfig.json ./
COPY ecosystem.config.js ./
RUN npm install
COPY src ./src
RUN npm run build

FROM node:12.19.0-buster
ENV NODE_ENV=production
COPY package.json ./
RUN npm install
COPY --from=build /dist ./dist
EXPOSE 4020
ENTRYPOINT ["node", "./dist/index.js"]