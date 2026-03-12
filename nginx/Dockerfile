FROM nginx:alpine

# Замена конфигурации по умолчанию
COPY nginx.conf /etc/nginx/nginx.conf
# Статика главной страницы
COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
