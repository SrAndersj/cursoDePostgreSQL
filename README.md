
entorno conda pycharm 

```commandline

sudo apt update
sudo apt install postgresql

sudo snap install curl
sudo apt install curl

curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub -o packages-pgadmin-org.pub


```


Instalar la clave pública del repositorio:


```commandline
sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg packages-pgadmin-org.pub

```
Crear el archivo de configuración del repositorio:

```commandline

echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" | sudo tee /etc/apt/sources.list.d/pgadmin4.list

```

Actualizar la lista de paquetes:

```commandline

sudo apt update

```


Instalar pgAdmin (puedes elegir entre el modo de escritorio o el modo web):

Para instalar en ambos modos:


```commandline

sudo apt install pgadmin4

```

Para instalar solo en el modo de escritorio:


```commandline
sudo apt install pgadmin4-desktop


```


Para instalar solo en el modo web:


```commandline

sudo apt install pgadmin4-web

```
Configurar el servidor web (solo si has instalado pgAdmin en el modo web):


```commandline

sudo /usr/pgadmin4/bin/setup-web.sh

```


iniciar Pgadmin 

```commandline
/usr/pgadmin4/bin/pgadmin4

```