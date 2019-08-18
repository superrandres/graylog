# Pasos para implementar de Servidor GrayLog
## Configurar el uso de memoria:
- $ sudo sysctl -w vm.max_map_count=262144
## Copiar los archivos de configuración de las variables de entorno
### Elastic Search
En el archivo .elastic.env.bak se puede encontrar un ejemplo con las variables para configurar el servicio de Elastic Search de nuestro compose de docker, debe copiar a un archivo .elastic.env.
### Gray Log
En el archivo .gray.env.bak se puede encontrar un ejemplo con las variables para configurar el servicio de Garylog Server de nuestro compose de docker, debe copiar a un archivo .gray.env.

### Para ejecutar fuera de docker compose:
docker run -d --restart=always --name=mongo -v /logs/mongo-data-graylog:/data/db -p 27017:27017 mongo:3

docker run -d --restart=always --name=elasticsearch -e ES_JAVA_OPTS="-Xms512m -Xmx512m" -e http.host=0.0.0.0 -e transport.host=localhost -e network.host=0.0.0.0 -p 9300:9300 docker.elastic.co/elasticsearch/elasticsearch-oss:6.6.1

docker run -d --restart=always --name=gray-log --link mongo --link elasticsearch -e GRAYLOG_HTTP_EXTERNAL_URI=http://logger.ucacue.edu.ec/ -e GRAYLOG_PASSWORD_SECRET=j6rmFUQMFXOcBOp3oePhyxKrE4IoM1BuSvgIBVL0HfQNvgWm2mjPp7iSOhEuEaM59VBAjCQEFqVTRRiBFfeT1vNTRffX2y3S -e GRAYLOG_ROOT_PASSWORD_SHA2=ebe4bc1e16310fcc8a661c75c1aebd09dbb606580d062291afd4afcbf9bfae65 -p 9001:9000 -p 5140:5140/udp graylog/graylog:3.0

docker run -d --restart=always --name=nginx-log -v /home/ronald/DockerProjects/gray-log/nginx.conf:/etc/nginx/conf.d/default.conf:ro -p 8005:80 nginx nginx -g 'daemon off;'

docker rm -f mongo elasticsearch gray-log nginx-log
