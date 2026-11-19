FROM nginx:alpine
LABEL autor="Mateusz Roznicki" data="2026-05-11"
COPY index.html style.css script.js /usr/share/nginx/html/
COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN date > /usr/share/nginx/html/build.txt
RUN apk add --no-cache nodejs npm && npm install -g htmlhint
RUN htmlhint /usr/share/nginx/html/index.html
EXPOSE 80