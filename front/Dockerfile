FROM node:18.18
RUN mkdir /home/node/app && chown node:node /home/node/app
RUN chown -R node:node /usr/local
WORKDIR  /home/node/app
USER node
RUN npm install -g npm@10.1.0
RUN npm install -g @angular/cli@16.2.4
RUN npm install -g firebase-tools
RUN git config --global user.email "tuto@gmail.com" \
    &&  git config --global user.name "Exemple" \
    &&  git config --global credential.helper store
COPY --chown=node:node . .
EXPOSE 4200
EXPOSE 9005