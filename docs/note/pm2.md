# Install PM2 (MAC)

## Install nvm & Node.js

``` bash
## Recommended path to install NVM:
# Set and export `NVM_DIR` environment variable. For example:
mkdir -vp ~/workspaces/runtimes/.nvm
export NVM_DIR="${HOME}/workspaces/runtimes/.nvm"

# Install NVM: (https://github.com/nvm-sh/nvm)
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

## For bash:
# Load .bashrc file to init NVM into current bash session:
source ~/.bashrc

## For zsh:
# Load .zshrc file to init NVM into current zsh session:
source ~/.zshrc

# Check installed NVM version:
nvm --version

# Install Node.js, update NPM to latest, and set default Node.js: (https://nodejs.org/en)
nvm install --latest-npm --alias=default {node.js version}

# Set to use default Node.js:
nvm use default

# Clean NVM caches:
nvm cache clear

# Check installed Node.js and NPM version:
node -v
npm -v
```

## Install PM2
``` bash
# Install essential extra packages:
npm install -g pm2 newman jshint
pm2 install pm2-logrotate

# Clean NPM caches:
npm cache clean --force

pm2 ping
```

!!! quote
    - [bybatkhuu/wiki](https://github.com/bybatkhuu/wiki/blob/main/posts/manuals/installs/nvm.md)

!!! note
    - [PM2](https://pm2.io/)
    - [NodeJS](https://nodejs.org/en)
    - [NVM](https://github.com/nvm-sh/nvm)
    ---
    - [POST1](https://medium.com/@adriendesbiaux/node-js-pm2-docker-docker-compose-devops-907dedd2b69a)
    - [POST2](https://www.travisluong.com/how-to-deploy-fastapi-with-nginx-and-pm2/)
    - [POST3](https://any-ting.tistory.com/74)
    - [POST4](https://inpa.tistory.com/entry/node-%F0%9F%93%9A-PM2-%EB%AA%A8%EB%93%88-%EC%82%AC%EC%9A%A9%EB%B2%95-%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0-%EB%AC%B4%EC%A4%91%EB%8B%A8-%EC%84%9C%EB%B9%84%EC%8A%A4)
    - [POST5](https://engineering.linecorp.com/ko/blog/pm2-nodejs)