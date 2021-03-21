## Linux Tricks

- paste into any terminal with `Shift + insert` 
- `sed` can have any delimiter you want to avoid escaping slash all the time 
- restart localhost server with `service dnsmasq restart`
- get OS details `cat /etc/os-release` 
- edit network setting on system without UI without editing the `/etc/netplan` yaml file, `nmtui`

### VIM 
- `O` to insert a new line above and start editing

### Docker
If you get 
```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/containers/json: dial unix /var/run/docker.sock: connect: permission denied
```
run `sudo chmod 666 /var/run/docker.sock`

### CI/CD 
If you cant get `puppeteer` running on CI/CD try this
```
pipeline:
  build:
    image: node
    commands:
      - echo starting
      - npm install
      - npm install puppeteer --only=dev
      - apt-get update
      - apt-get install -y -qq gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget > /dev/null
      - node node_modules/puppeteer/install.js
```





