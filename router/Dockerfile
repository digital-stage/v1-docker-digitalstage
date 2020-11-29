FROM node:14.15.0-buster AS build
# Service description
ENV DOMAIN=localhost
ENV PORT=4010
# The public port may differ when using nginx proxy
ENV PUBLIC_PORT=8080
ENV USE_IPV6=false
ENV WS_PREFIX=wss
ENV REST_PREFIX=http
# The public port may differ when using nginx proxy
ENV ROOT_PATH=''

ENV ROUTER_DIST_URL=wss://router-distributor:4020
ENV API_URL=http://digital-server:4000
ENV AUTH_URL=http://auth-server:5000

ENV RTC_MIN_PORT=40000
ENV RTC_MAX_PORT=40100
ENV LISTEN_IP=0.0.0.0

RUN git clone https://github.com/digital-stage/router.git \
 && cd router \
 && npm install \
 && npm run build

FROM node:14.15.0-buster
ENV NODE_ENV=production
COPY --from=build /router/package.json ./
RUN npm install
COPY --from=build /router/dist ./dist
EXPOSE 4020
ENTRYPOINT ["node", "./dist/index.js"]