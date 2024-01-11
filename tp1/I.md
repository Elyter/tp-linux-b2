# I. Init

## 3. sudo c pa bo

🌞 **Ajouter votre utilisateur au groupe `docker`**

```
[elyter@localhost ~]$ sudo usermod -aG docker elyter
[elyter@localhost ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

🌞 **Lancer un conteneur NGINX**

```
[elyter@localhost ~]$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
24e221e92a36: Pull complete 
58cc89079bd7: Pull complete 
3799b53049f3: Pull complete 
2a580edba2f4: Pull complete 
cfe7877ea167: Pull complete 
6f26751fc54b: Pull complete 
c98494bb3682: Pull complete 
Digest: sha256:bd30b8d47b230de52431cc71c5cce149b8d5d4c87c204902acf2504435d4b4c9
Status: Downloaded newer image for nginx:latest
6cfad37c8d1e18bb6e0c43291d32d18cc1034e11b1110fb2ab4a77b623a49cff
```

🌞 **Visitons**

```
[elyter@localhost ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
6cfad37c8d1e   nginx     "/docker-entrypoint.…"   14 seconds ago   Up 13 seconds   0.0.0.0:9999->80/tcp, :::9999->80/tcp   vibrant_morse

[elyter@localhost ~]$ docker logs -f 6cfad37c8d1e

[elyter@localhost ~]$ docker inspect 6cfad37c8d1e

[elyter@localhost ~]$ sudo ss -lnpt
State         Recv-Q        Send-Q                Local Address:Port                 Peer Address:Port        Process                                         
LISTEN        0             4096                        0.0.0.0:9999                      0.0.0.0:*            users:(("docker-proxy",pid=14536,fd=4))        
LISTEN        0             128                         0.0.0.0:22                        0.0.0.0:*            users:(("sshd",pid=690,fd=3))                  
LISTEN        0             4096                           [::]:9999                         [::]:*            users:(("docker-proxy",pid=14542,fd=4))        
LISTEN        0             128                            [::]:22                           [::]:*            users:(("sshd",pid=690,fd=4))     

[elyter@localhost ~]$ sudo firewall-cmd --add-port 9999/tcp
success
[elyter@localhost ~]$ sudo firewall-cmd --reload
success


```

🌞 **On va ajouter un site Web au conteneur NGINX**

```
[elyter@localhost nginx]$ docker stop 6cfad37c8d1e
6cfad37c8d1e
[elyter@localhost nginx]$ docker rm 6cfad37c8d1e
6cfad37c8d1e
[elyter@localhost nginx]$ docker run -d -p 9999:8080 -v /home/elyter/nginx/index.html:/var/www/html/index.html -v /home/elyter/nginx/poto.conf:/etc/nginx/conf.d/poto.conf nginx
4c01c85687ec331511709d5b43304918ae93558ffca549dd3f42c885df3187f6


```
🌞 **Visitons**

```
[elyter@localhost nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED       STATUS       PORTS                                               NAMES
4c01c85687ec   nginx     "/docker-entrypoint.…"   9 hours ago   Up 9 hours   80/tcp, 0.0.0.0:9999->8080/tcp, :::9999->8080/tcp   affectionate_elion

[elyter@localhost nginx]$ sudo ss -lnpt
State         Recv-Q        Send-Q                Local Address:Port                 Peer Address:Port        Process                                         
LISTEN        0             4096                        0.0.0.0:9999                      0.0.0.0:*            users:(("docker-proxy",pid=14899,fd=4))        
LISTEN        0             128                         0.0.0.0:22                        0.0.0.0:*            users:(("sshd",pid=690,fd=3))                  
LISTEN        0             4096                           [::]:9999                         [::]:*            users:(("docker-proxy",pid=14905,fd=4))        
LISTEN        0             128                            [::]:22                           [::]:*            users:(("sshd",pid=690,fd=4))

```
🌞 **Lance un conteneur Python, avec un shell**

```
[elyter@localhost nginx]$ docker run -it python bash
Unable to find image 'python:latest' locally
latest: Pulling from library/python
b66b4ecd3ecf: Pull complete 
6c641d36985b: Pull complete 
ddd8544b6e15: Pull complete 
ae58c7c06d64: Pull complete 
f9f35f1c3178: Pull complete 
0d89c447e056: Pull complete 
9862771c91cc: Pull complete 
93aa698c30e4: Pull complete 
Digest: sha256:3733015cdd1bd7d9a0b9fe21a925b608de82131aa4f3d397e465a1fcb545d36f
Status: Downloaded newer image for python:latest
```

🌞 **Installe des libs Python**

```
root@73ae4876d21d:/# pip install aiohttp
root@73ae4876d21d:/# pip install aioconsole

root@73ae4876d21d:/# python
Python 3.12.1 (main, Dec 19 2023, 16:44:02) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import aiohttp
>>>

```