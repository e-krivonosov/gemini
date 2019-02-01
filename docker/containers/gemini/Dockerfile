FROM node:8

WORKDIR /var/tools

USER root
RUN chown -R 1000:1000 /var/tools
RUN mkdir -p /var/work && chown -R 1000:1000 /var/work
RUN apt-get install -y make
USER 1000
RUN mkdir ~/.npm-packages \
&& prefix=~/.npm-packages \
&& NPM_PACKAGES=~/.npm-packages \
&& export PATH=$NPM_PACKAGES/bin:$PATH \
&& . ~/.profile \
&& npm config set prefix '~/.npm-packages'

RUN npm install -g gemini gemini-gui

WORKDIR /var/work
# local installation
RUN npm install gemini
# Environment
#ENV NODE_PATH=/usr/local/lib/node_modules
RUN ln -s /var/work/node_modules/gemini/bin/gemini /var/work/gemini
# Tools
ADD Makefile /var/tools/


ENTRYPOINT ["bash"]