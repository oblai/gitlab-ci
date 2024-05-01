FROM node:18.18.0

WORKDIR /app
ENV GITLAB="gitlab.com"
ENV GIT_REPOSITORY="git@gitlab.com:group/project.git"
ENV GREENSOCK_TOKEN="00000-0000-0000-00000-00000"
ENV CMD="project/frontend/.output/server/index.mjs"
ENV PROJECT="project"

COPY id_rsa /root/.ssh/id_rsa
RUN apt-get update && apt-get install -y git openssh-client && \
    mkdir -p /root/.ssh && ssh-keyscan $GITLAB >> /root/.ssh/known_hosts && \
    chmod 600 ~/.ssh/id_rsa

RUN git clone $GIT_REPOSITORY

RUN cd $PROJECT/frontend/ && \
    npm config set @gsap:registry https://npm.greensock.com && \
    npm config set //npm.greensock.com/:_authToken $GREENSOCK_TOKEN && \
    npm install && \
    npm run build

EXPOSE 3000
CMD ["node", "$CMD"]