FROM node:alpine
USER node
COPY  --chown=node:node ./ /
WORKDIR /
RUN npm install
WORKDIR /
CMD ["npm", "start" ]
