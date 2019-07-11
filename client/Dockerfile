FROM node:10 as node

WORKDIR /image

COPY . .

RUN ["npm", "install"]

RUN ["npm", "run", "build"]

FROM node:10 as node-serve

COPY --from=node /image/build .

RUN ["npm", "install", "-g", "serve"]

EXPOSE 3000

ENTRYPOINT ["/usr/local/bin/serve", "-l", "3000"]
