FROM node:alpine AS base

RUN mkdir /app /data
WORKDIR /app

FROM base AS build
RUN apk add --update python3 git make g++
RUN git clone --depth=1 https://github.com/ether/etherpad-lite.git .  && rm -rf .git
RUN /app/bin/installDeps.sh


FROM base AS release
COPY --chown=node:node --from=build /app/ /app/
RUN ln -s /data/ /app/var/
RUN ln -s /data/settings.js /app/settings.js
RUN chown node: /app/
USER node

#HEALTHCHECK --interval=20s --timeout=3s CMD ["etherpad-healthcheck"]

EXPOSE 9001
VOLUME ["/data"]
CMD ["node", "node_modules/ep_etherpad-lite/node/server.js", "-s", "/data/settings.json"]

