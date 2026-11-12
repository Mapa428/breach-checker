FROM nginx:alpine
LABEL autor="Mateusz Roznicki" data="2026-05-11"
COPY . /usr/share/nginx/html/
RUN date > /usr/share/nginx/html/build.txt
RUN apk add --no-cache nodejs npm && npm install -g htmlhint
RUN htmlhint /usr/share/nginx/html/index.html
EXPOSE 80