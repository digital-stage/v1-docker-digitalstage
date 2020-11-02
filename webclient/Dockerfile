FROM node:12.19.0-alpine AS build
ENV NEXT_PUBLIC_USE_SSL=false
ENV PORT=3000
RUN apk add git \
&& git clone https://github.com/digital-stage/webclient.git \
&& cd webclient \
&&  rm .env* \
&& npm install \
&& npm run build
WORKDIR /webclient
EXPOSE 3000
ENTRYPOINT ["npm", "run", "start"]