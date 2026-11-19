## zadanie 1
wynik z przegladarki:
{
  "status": "ok"
}

wynik z docker logs backend: 

192.168.65.1 - - [12/Nov/2026 08:00:16] "GET /health HTTP/1.1" 200 -

## zadanie 2
Przy dzialajacym backendzie: 
mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker run --rm --network breach-net healthcheck-probe
backend: OK

Bez network: 
mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker run --rm healthcheck-probe
backend: UNREACHABLE

ponownie w sieci breach-net, ale po docker stop backend
mateusz@MacBook-Pro-Mateusz-3 breach-checker % docker run --rm --network breach-net 
backend: UNREACHABLE


## zadanie 3

$ docker exec backend sh -c "echo notatka > /tmp/notatka.txt"

$ docker restart backend
backend

$ docker exec backend cat /tmp/notatka.txt
notatka

$ docker rm -f backend
backend

$ docker run -d --name backend --network breach-net -p 5000:5000 -v ./data/leaked-sha1.txt:/app/data/leaked-sha1.txt:ro breach-checker-backend:v1
e4a1c8b9d2f3a5c6e7b8d9f0a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0

$ docker exec backend cat /tmp/notatka.txt
cat: /tmp/notatka.txt: No such file or directory


Wolumeny: 

$ docker run --rm -v breach-dane:/dane alpine sh -c "date >> /dane/historia.txt"

$ docker run --rm -v breach-dane:/dane alpine sh -c "date >> /dane/historia.txt; cat /dane/historia.txt"
Thu Nov 12 09:18:01 UTC 2026
Thu Nov 12 09:18:05 UTC 2026

$ docker volume ls
DRIVER    VOLUME NAME
local     breach-dane

$ docker volume rm breach-dane
breach-dane
