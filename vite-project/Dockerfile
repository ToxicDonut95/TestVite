FROM nginx:latest

COPY dist/ /usr/share/nginx/html

RUN rm -rf /etc/nginx/conf.d/default.conf

COPY nginx.conf /etc/nginx/conf.d/

CMD ["nginx", "-g", "daemon off;"]