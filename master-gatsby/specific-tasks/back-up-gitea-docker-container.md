# Backing up Gitea Docker Container

## Situation

- I have a Ubuntu VPS with Plesk running with installed extension "docker"
- Gitea runs in Docker container
- I want to back up all the Gitea data in case something goes banana (Gitea or the whole VPS)

## Back up the container data

1. Get the container ID (the number)

```shell
root@secretServer:/# docker ps
CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                                            NAMES
80b2c463c564        gitea/gitea                     "/usr/bin/entrypoint…"   2 days ago          Up 21 hours         0.0.0.0:32783->22/tcp, 0.0.0.0:32782->3000/tcp   gitea
```

2. Find where the container dumps the stuff (the "source" folder)

```shell
root@secretServer:/# docker inspect 80b2
... more stuff
 "Mounts": [
            {
                "Type": "volume",
                "Name": "c2d13b1e8f3d49e2441b86be5b2f5bb161fd5042ad78ce53facdeaa926eb1bd8",
                "Source": "/var/lib/docker/volumes/c2d13b1e8f3d49e2441b86be5b2f5bb161fd5042ad78ce53facdeaa926eb1bd8/_data",
                "Destination": "/data",
                "Driver": "local",
                "Mode": "",
                "RW": true,
                "Propagation": ""
            }
        ],
... more stuff
```

3. Copy the content of the source folder to folder of your choice, in my case /tmp/_meaningfull_name_ (for example `gitea_back_up_data_20201231`)
   - **do not forget to add `-a` to "archive" the folder as it is (including ownership and symlinks)**
   - the dot `.` after `/_data/` includes also hidden files (very important)

```shell
root@secretServer:/# cp -a /var/lib/docker/volumes/c2d13b1e8f3d49e2441b86be5b2f5bb161fd5042ad78ce53facdeaa926eb1bd8/_data/. /tmp/gitea_back_up_data_20201231/
```

4. Go into folder of your choice, in my case the `/tmp` and check if everything is copied.
   - `ls -lh` are the files displayed with long listing format `l` and with human readable sizes `-h`
   - `ls -lha` shows hidden files as well.

```shell
root@secretServer:/tmp# ls -lh
drwxr-xr-x 5 root root 4,0K Dez 28 20:24 gitea_back_up_data_20201231
root@secretServer:/tmp/gitea_back_up_data_20201231# ls -lha
insgesamt 36K
drwxr-xr-x  5 root root   4,0K Dez 28 20:24 .
drwxrwxrwt 15 root root    20K Dez 31 16:29 ..
drwxr-xr-x  5 1000 psaadm 4,0K Dez 31 12:11 git
drwxr-xr-x 10 1000 psaadm 4,0K Dez 31 15:24 gitea
drwx------  2 root root   4,0K Dez 28 20:24 ssh
```

5. Zip the stuff
   - `-r` includes hidden files as well

```shell
root@secretServer:/tmp# zip -r gitea_back_up_data_20201231.zip gitea_back_up_data_20201231
```

6. Place the data somewhere save. The VPS is backed up so it would be sufficient to copy it somewhere save but I am a little worried (paranoid?) about the whole server being lost. What if the invoice is not paid? Can happen when billed to a company... it happened to me before... So I save it on the server + I download it to my PC (running Windows) using Putty PSCP. You need to install Putty first. <https://www.putty.org/>
   1. check if `pscp` is available. If not, it is not added to the PATH. Add it to the path or try running `pscp` from the Putty installation folder.
   2. download the zipped file using `pscp`. Do not forget `-P 22`. You will be promped for a password
   3. peek inside if that is all you need
   4. save somewhere save

```shell
C:\Users\secretUser>pscp
PuTTY Secure Copy client
Release 0.74
Usage: pscp [options] [user@]host:source target
       pscp [options] source [source...] [user@]host:target
       pscp [options] -ls [user@]host:filespec
Options:
  -V        print version information and exit
  -pgpfp    print PGP key fingerprints and exit
  -p        preserve file attributes
  -q        quiet, don't show statistics
  -r        copy directories recursively
  -v        show verbose messages
  -load sessname  Load settings from saved session
  ...
```

```
pscp -P 22 root@secretServer.secretProvider.net:/tmp/gitea_back_up_data_20201231.zip c:\
```

## Back up the container itself

- with the id from previous step

```shell
root@secretServer:/tmp# docker commit -p 80b2c4 gitea_container_backup_20201231
sha256:6556bbbc01a04887c22a75bbc4786cd2badc0c50b693f0c03794e94d7bf037cb
root@secretServer:/tmp# docker save -o gitea_container_backup_20201231.tar gitea_container_backup_20201231
root@secretServer:/tmp# ls -lh
-rw------- 1 root root 216M Dez 31 16:56 gitea_container_backup_20201231.tar
```

- download it to your PC/save somewhere save the same way as before

**That was all, your data are save**

# Loading the data back

1. if the server is still alive, you should have all the backup data saved on it. If not use `pscs` to copy it to a new server .
2. **DO NOT USE PLESK DOCKER "Upload Image" IMAGE, IT DOESNT WORK** , it returns `Error: {"message":"No command specified"}` , use

```
docker load -i gittea_backup_20201231.tar
```

it should be visible in the Plesk UI. Start the container and then stop it again. It will get ID. So find the "Source" path again. (Steps 1+2 when creating the backup). Delete everything inside and replace it with the content of the backup data. Make sure the folder structure stayes the same and all invisible files are coppied as well. Restart the server and enjoy!
