FROM node:14.15.0-buster AS build
ENV NEXT_PUBLIC_USE_SSL=false
ENV PORT=3000
RUN git clone https://github.com/digital-stage/webclient.git \
&& cd webclient \
&&  rm .env* \
&& npm install \
&& npm run build
WORKDIR /webclient
EXPOSE 3000
ENTRYPOINT ["npm", "run", "dev"]