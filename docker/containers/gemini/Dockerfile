FROM node:8

WORKDIR /var/tools

USER root
RUN chown -R 1000:1000 /var/tools
RUN mkdir -p /var/work && chown -R 1000:1000 /var/work
RUN apt-get install -y make
USER 1000
ENV NPM_PACKAGES=~/.npm-packages
ENV PATH=$NPM_PACKAGES/bin:$PATH
ENV NODE_PATH=~/.npm-packages/lib/node_modules
RUN mkdir ~/.npm-packages \
&& prefix=~/.npm-packages \
&& . ~/.bashrc \
&& npm config set prefix '~/.npm-packages'
RUN npm install -g gemini gemini-gui
WORKDIR /var/work
# local installation
RUN npm install gemini
# Environment
#ENV NODE_PATH=/usr/local/lib/node_modules
ADD --chown=1000:1000 Makefile /var/tools/
# Tools
ADD Makefile /var/tools/
#ENTRYPOINT ["make", "-f", "/var/tools/Makefile"]
ENTRYPOINT ["bash"]