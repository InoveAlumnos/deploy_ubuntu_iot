![Inove banner](/inove.jpg)
Inove Escuela de Código\
info@inove.com.ar\
Web: [Inove](http://inove.com.ar)

---

# Deployar y setup de Ubuntu! [Python]
En este documento se detalla los pasos a seguir para realizar el setup de ubuntu una vez instalado en nuestro dispositivo IoT o en nuestra PC. Para ver los pasos referidos a la descarga de Ubuntu y su instalación, consultar el apunte de clase PDF con el paso a paso y las capturas de pantallas.

# 1 - Setup de Ubuntu server
En esta guía se explica los pasos a seguir para instalar en el sistema:
- herramientas básicas
- mosquitto MQTT
- docker
- python pip y libs
- tmate

Antes de comenzar a instalar cualquier programa en una nueva terminal, debemos ejecutar:
```sh
$ sudo apt-get update
```

## 2 - Instalar paquetes comunes del sistema
Instalar herramientas de red (como el comando ifconfig)
```sh
$ sudo apt-get install -y net-tools
```

## 3 - Instalar mosquitto
Instalar mosquitto y sus clientes (pub y sub)
```sh
$ sudo apt-get install -y mosquitto mosquitto-clients
```

Configurar mosquitto para escuchar por puerto 1883 y por 9001 websockets
```sh
$ sudo touch /etc/mosquitto/conf.d/mosquitto.conf

$ echo -e "allow_anonymous true\nlistener 1883 0.0.0.0\nallow_anonymous true\nlistener 9001\nprotocol websockets" | sudo tee /etc/mosquitto/conf.d/mosquitto.conf

$ sudo service mosquitto restart
```

## 4 - Instalar docker
Los pasos de instalación se obtuvieron de: Cómo instalar docker en Ubuntu

Instalar dependencias necesarias
```sh
$ sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

Bajar repositorio de paquetes de docker:
```sh
$ sudo mkdir -p /etc/apt/keyrings

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o  /etc/apt/keyrings/docker.gpg

$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

$ sudo apt-get update
```

Instalar paquetes de docker
```sh
$ sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

Instalar docker compose
```sh
$ sudo apt-get install -y docker-compose
```

Ensayar que docker funcione
```sh
$ sudo service docker start

$ sudo docker run hello-world
```

Configurar para que docker no necesite utilizar sudo
```sh
$ sudo groupadd docker

$ sudo usermod -aG docker $USER

$ sudo reboot
```

## 5 - Instalar python pip
Instalar pip
```sh
$ sudo apt-get install -y python3-pip
```

## 6 - Ensayar el sistema
Descargar el repositorio de la clase de contenedores y probar el último ejemplo completo lanzado desde docker:
```sh
$ git clone https://github.com/InoveAlumnos/container_iot
```

No olvide instalar las dependencias con el archivo de requirements.txt que se encuentra dentro del repositorio
```sh
$ python3 -m pip install -r requirements.txt
```

Ahora puede lanzar el ejemplo más completo con docker-compose
```sh
$ docker-compose up
```

## 7 - Instalar tmate
Para instalarlo ejecutamos:
```sh
$ sudo apt-get install -y tmate
```

Para utilizarlo lanzamos en la consola el comando “tmate” y deberemos copiar el “ssh” que nos aparece abajo en la barra amarilla. Ese ssh lo compartimos y lo copiamos en nuestra consola y podremos acceder remotamente. Este ssh nos lo debe compartir alguien con acceso al dispositivo en la red del cliente:


# Consultas
alumnos@inove.com.ar

