FROM node:14.15.0-buster AS build
ENV USE_SSL=false
ENV SECRET=dawd2f2f2f2222dcwwdwdwe23593g33v6c73147a
ENV MONGO_URL=mongodb://mongo:27017

RUN git clone https://github.com/digital-stage/auth-server.git \
 && cd auth-server \
 && npm install \
 && npm run build

FROM node:14.15.0-buster
ENV NODE_ENV=production
COPY --from=build /auth-server/package.json ./
RUN npm install
COPY --from=build /auth-server/dist ./dist
EXPOSE 5000
ENTRYPOINT ["node", "./dist/index.js"]