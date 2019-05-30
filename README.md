# Pasos para implementar de Servidor GrayLog
## Configurar el uso de memoria:
- $ sudo sysctl -w vm.max_map_count=262144
## Copiar los archivos de configuración de las variables de entorno
### Elastic Search
En el archivo .elastic.env.bak se puede encontrar un ejemplo con las variables para configurar el servicio de Elastic Search de nuestro compose de docker, debe copiar a un archivo .elastic.env.
### Gray Log
En el archivo .gray.env.bak se puede encontrar un ejemplo con las variables para configurar el servicio de Garylog Server de nuestro compose de docker, debe copiar a un archivo .gray.env.
