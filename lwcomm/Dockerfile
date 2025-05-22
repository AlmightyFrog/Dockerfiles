FROM node:12-alpine AS base

WORKDIR /workspace

RUN apk add --no-cache make gcc g++ python3 linux-headers udev git pkgconfig libusb-dev

RUN git clone --depth=1 https://github.com/LaserWeb/lw.comm-server .

RUN mkdir /laserweb
RUN cp config.js grblStrings.js firmwareFeatures.js LICENSE lw.comm-server.service package.json README.md server.js version.txt /laserweb/
RUN cp -r app/ /laserweb/app/

WORKDIR /laserweb

RUN npm install

FROM node:12-alpine

ENV ENV="production"
ENV NODE_ENV="production"

WORKDIR /app
COPY --from=base /app ./
COPY --from=base /workspace/docker_entrypoint.sh ./

EXPOSE 8000

ENTRYPOINT ["/docker_entrypoint.sh"]
CMD []
