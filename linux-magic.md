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


## Linux folders
- notes from (Linux File System/Structure Explained!
)[https://www.youtube.com/watch?v=HbgzrKJvDRw]
for linux "everything is a file"
- FHS Filesystem Hierarchy Standard
- *bin* (binaries), contains programs like `ls`, `cat` etc
- *sbin* (system binaries), contains programs that would system administrator used, no permission to user 
- *boot* bootloader 
- *cdrom* legacy folder for mounting cd rom, not used that much anymore 
- *dev* where devices live
  - disk is *sda*, partitions *sda1*, *sda2*...
  - everything from webcam to keyboard
- *etc* (et cetera or edit to configure), all configuration system wide stored (not used stored)
- *home* personal files
- *lib*, *lib32*, *lib64* libraries for binaries 
- *mnt*, *media* stuff like USB disks, external drivers... when mounting manually mount to *mnt*, let *media* for automatic OS mounting
- *opt* optional, manually installed SW from vendors, you can install here SW that you create yourself 
- *proc* files containing info about system processes, every process has its own directory with info 
  - info about CPU `cat /proc/cpuinfo`
  - update `cat /proc/uptime`
- *root* root user home folder
- *run* new order, runs in RAM, wiped after power shutdown, stores runtime information 
- *snap* where snap packages are stored, mainly used by Ubuntu, these packages are self-contained packages that run differently than the other apps 
- *src* service data
- *sys* system folder, similar to *run*, created everytimes the system boots up
- *tmp* temporary files, autosaving stuff etc.
- *usr* user application space, for application used by user (not as *bin* where the application used by system live), apps nonessential for operation system run 
  - has *lib* folder inside for libraries needed by those applications
- *var* variables, grows in size
  - crash reports
  - logs 
- `dev/zero` is nowhere, only root can get there... outputs stream of zeros, used for creating of dummy files or swaps 
- `dev/null` is also nowwhere and produces no output 


### Tabs 
New tab: `Ctrl + Shift + T`
Close tab: `Ctrl + Shift + W`
Switch tab: `Ctrl + Pg Up` and `Ctrl + Pg Dn`
Move tab: `Ctrl + Shift + Pg Up` and `Ctrl + Shift + Pg Dn`

### Command line tricks 