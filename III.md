# III. Docker compose

Pour la fin de ce TP on va manipuler un peu `docker compose`.

🌞 **Créez un fichier `docker-compose.yml`**
```
[elyter@localhost ~]$ mkdir compose_test
[elyter@localhost ~]$ cd compose_test/
[elyter@localhost compose_test]$ nano docker-compose.yml

```
🌞 **Lancez les deux conteneurs** avec `docker compose`

```
[elyter@localhost compose_test]$ docker compose up -d
[+] Running 3/3
 ✔ Network compose_test_default                  Created                   0.2s 
 ✔ Container compose_test-conteneur_flopesque-1  Started                   0.0s 
 ✔ Container compose_test-conteneur_nul-1        Started                   0.0s 
```

🌞 **Vérifier que les deux conteneurs tournent**

```
[elyter@localhost compose_test]$ docker ps
CONTAINER ID   IMAGE     COMMAND        CREATED         STATUS         PORTS     NAMES
6eafd1185411   debian    "sleep 9999"   2 minutes ago   Up 2 minutes             compose_test-conteneur_flopesque-1
a2c534e1c1a5   debian    "sleep 9999"   2 minutes ago   Up 2 minutes             compose_test-conteneur_nul-1
```


🌞 **Pop un shell dans le conteneur `conteneur_nul`**

```
[elyter@localhost compose_test]$ docker exec -it compose_test-conteneur_nul-1 bash
root@a2c534e1c1a5:/# apt-get update
root@a2c534e1c1a5:/# apt-get install iputils-ping
root@a2c534e1c1a5:/# ping compose_test-conteneur_flopesque-1
PING compose_test-conteneur_flopesque-1 (172.18.0.2) 56(84) bytes of data.
64 bytes from compose_test-conteneur_flopesque-1.compose_test_default (172.18.0.2): icmp_seq=1 ttl=64 time=0.264 ms
```
