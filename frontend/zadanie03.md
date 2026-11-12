{"autor":"Mateusz Roznicki","data":"2026-05-11"}
wynik dockerhistory: 
IMAGE          CREATED              CREATED BY                                      SIZE      COMMENT
db15785a6858   About a minute ago   EXPOSE [80/tcp]                                 0B        buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c htmlhint /usr/share/nginx/htm…   4.1kB     buildkit.dockerfile.v0
<missing>      About a minute ago   RUN /bin/sh -c apk add --no-cache nodejs npm…   95.9MB    buildkit.dockerfile.v0
<missing>      About a minute ago   COPY . /usr/share/nginx/html # buildkit         32.8kB    buildkit.dockerfile.v0
<missing>      About a minute ago   LABEL autor=Mateusz Roznicki data=2026-05-11    0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          RUN /bin/sh -c set -x     && apkArch="$(cat …   51.5MB    buildkit.dockerfile.v0
<missing>      2 weeks ago          ENV ACME_VERSION=0.4.1                          0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          ENV NJS_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          ENV NJS_VERSION=1.0.2                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          COPY 30-tune-worker-processes.sh /docker-ent…   16.4kB    buildkit.dockerfile.v0
<missing>      2 weeks ago          COPY 20-envsubst-on-templates.sh /docker-ent…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago          COPY 15-local-resolvers.envsh /docker-entryp…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago          COPY 10-listen-on-ipv6-by-default.sh /docker…   12.3kB    buildkit.dockerfile.v0
<missing>      2 weeks ago          COPY docker-entrypoint.sh / # buildkit          8.19kB    buildkit.dockerfile.v0
<missing>      2 weeks ago          RUN /bin/sh -c set -x     && addgroup -g 101…   5.99MB    buildkit.dockerfile.v0
<missing>      2 weeks ago          ENV DYNPKG_RELEASE=1                            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          ENV PKG_RELEASE=1                               0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          ENV NGINX_VERSION=1.31.8                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          CMD ["/bin/sh"]                                 0B        buildkit.dockerfile.v0
<missing>      2 weeks ago          ADD alpine-minirootfs-3.24.3-aarch64.tar.gz …   9.31MB    buildkit.dockerfile.v0

Zadanie 2
front1:
Thu Nov  5 07:54:58 UTC 2026
front2: 
Thu Nov  5 07:54:58 UTC 2026
docker ps -a:
CONTAINER ID   IMAGE                          COMMAND                  CREATED         STATUS         PORTS                                     NAMES
7091aa6db1c2   mateusz-roznicki-frontend:v2   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:8081->80/tcp, [::]:8081->80/tcp   front2
7e17393e3dbd   mateusz-roznicki-frontend:v2   "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   front1
poniewaz build wykonaj sie raz i wtedy zapisala sie data buildu na jednej z warstw obrazu

Zadanie 3
    root   /usr/share/nginx/html

w dokumentacji nginx jest zapisane ze tam musimy kopiowac pliki bo to tam nginx serwuje pliki statyczne dla uzytkownikow

Zadanie 4

mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker exec front-bad ls /usr/share/nginx
    html
    index.html
    script.js
    style.css
    zadanie03.md
mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker exec front-bad ls /usr/share/nginx/html
    50x.html
    build.txt
    index.html


zadanie 5

mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker rmi breach-checker-frontend:latest
Untagged: breach-checker-frontend:latest
mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker images
                                                                                                                            i Info →   U  In Use
IMAGE                              ID             DISK USAGE   CONTENT SIZE   EXTRA
breach-checker-frontend:v1         84549f79e7a1       93.2MB         26.3MB        
breach-checker-frontend:v2         4fb71d30f369       93.2MB         26.3MB        
breach-checker-frontend:v3         2ca3b43f7066        220MB         57.6MB        
dashboard-frontend:latest          3c9b4aebd979        102MB         29.1MB        
dashboardwalut-backend:latest      41c1351f7a43       27.3MB         9.08MB        
dashboardwalut-frontend:latest     dd0525ce4874         93MB         26.3MB        
golang:1.26-alpine                 3082400e369f        357MB         68.9MB        
mateusz-roznicki-frontend:latest   db15785a6858        220MB         57.6MB        
mateusz-roznicki-frontend:v1       db15785a6858        220MB         57.6MB        
mateusz-roznicki-frontend:v2       81a6b5732484        220MB         57.6MB        
nginx:alpine                       785835ea65db       94.1MB         27.2MB        
nginx:latest                       600f7cd45e27        261MB         65.1MB        
postgres:17-alpine                 b0f9560a2de0        415MB          116MB        
postgres:latest                    74935e722416        672MB          167MB        
python:3.10.21-alpine              8d62622e4ad0         86MB         21.1MB        
redis:alpine                       21090af93f83        161MB         39.7MB        
ubuntu:latest                      c098726dd9b9        181MB         44.9MB        
mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker rmi breach-checker-frontend:v2
Untagged: breach-checker-frontend:v2
Deleted: sha256:4fb71d30f3691d89882237c81cae744d08fb46119b16673625b5f334da8a3f77

