# Pure-FTPd server
![Pure-FTPd Logo](https://www.pureftpd.org/images/pure-ftpd.png "[Pure-FTPd Logo")

## Environment variables
* PUBLICHOST: The name of your public domain.
```
-e "PUBLICHOST=foo.bar.de"
``` 
* PASSIVEPORTS: The portrange of the passive ports. This can be usefull if you use more the one container.
```
-e "PASSIVEPORTS=30000:300009"
``` 
* ADDED_FLAGS: With this you are able to add additional flags which will be passed to the pure-ftpd binary during start. A list of flags can be found in the official documentation [https://www.pureftpd.org/project/pure-ftpd/doc](https://www.pureftpd.org/project/pure-ftpd/doc). E.g. use pure-tftpd with tls
```
-e "ADDED_FLAGS=--tls=2"
``` 

## Volumes
* Virtual user passwd
```
-e "/path/to/your/pureftpd/passwd/:/etc/pure-ftpd/passwd/"
```
* The path to the folder wich should be accessable through your FTP server
```
-e "/path/to/your/ftp-root/:/ftp-root/"
```

## Start the server
```
docker run -dit --name="Pure-FTPd" -p 21:21 -p 30000-30009:30000-30009 -e PUBLICHOST=foo.bar.de -e PASSIVEPORTS=30000:300009 topdockercat/pure-ftpd:stable
```

## Add virual user
To add a new virtual user you have to run the following command where Pure-FTPd must be the name of your container and /ftp-root/dummy the root folder for the new user.
```
docker exec -it Pure-FTPd pure-pw useradd dummy -f /etc/pure-ftpd/passwd/pureftpd.passwd -m -u ftpuser -d /ftp-root/dummy
```