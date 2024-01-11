# II. Images

## 1. Images publiques

🌞 **Récupérez des images**

```
[elyter@localhost nginx]$ docker pull python:3.11
3.11: Pulling from library/python

[elyter@localhost nginx]$ docker pull mysql:5.7
5.7: Pulling from library/mysql
no matching manifest for linux/arm64/v8 in the manifest list entries
[elyter@localhost nginx]$ docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql

[elyter@localhost nginx]$ docker pull wordpress
Using default tag: latest
latest: Pulling from library/wordpress

[elyter@localhost nginx]$ docker pull linuxserver/wikijs
Using default tag: latest
latest: Pulling from linuxserver/wikijs

[elyter@localhost nginx]$ docker image ls
REPOSITORY           TAG       IMAGE ID       CREATED       SIZE
mysql                latest    8e409b83ace6   3 days ago    641MB
linuxserver/wikijs   latest    772abe6ffca7   6 days ago    459MB
wordpress            latest    4468dc043c37   2 weeks ago   739MB
python               3.11      f983f601e9a2   2 weeks ago   1.01GB

```

🌞 **Lancez un conteneur à partir de l'image Python**

```
[elyter@localhost nginx]$ docker run -it python:3.11 bash
root@d7e0831f37ea:/# python
Python 3.11.7 (main, Dec 19 2023, 17:02:47) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

## 2. Construire une image


🌞 **Ecrire un Dockerfile pour une image qui héberge une application Python**

```
Dockerfile

FROM debian:latest

RUN apt-get update

RUN apt-get install -y python3

RUN apt-get install -y python3-emoji

COPY app.py /app.py

ENTRYPOINT ["python3", "/app.py"]
```

🌞 **Build l'image**

```
[elyter@localhost python-app]$ docker build . -t python_app:latest
[+] Building 10.7s (10/10) FINISHED        
```

🌞 **Lancer l'image**

```
[elyter@localhost python-app]$ docker run python_app:latest
Cet exemple d'application est vraiment naze 👎
```