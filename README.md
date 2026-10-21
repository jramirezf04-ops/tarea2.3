# Práctica: Configuración y Conectividad de Motores de Bases de Datos en Red

**Servidor (IP):** 192.168.0.26
**Cliente:** Linux Mint (Máquina Virtual)

---

## Estado del Servidor
Antes de comenzar con los clientes, he comprobado que los tres motores de bases de datos se encuentran en ejecución en el servidor (PostgreSQL y MariaDB como servicios de `systemd`, y Oracle Database en un contenedor gestionado con `podman`)[cite: 20].
![Estado de los servicios en el servidor](01.png)

---

## 1. PostgreSQL

### 1.1. Conexión mediante Cliente de Consola
Tras habilitar la escucha remota en el servidor, he instalado el paquete `postgresql-client` en mi máquina cliente para poder acceder por terminal[cite: 15].
![Instalación de postgresql-client](13.png)

Me he conectado remotamente con el comando `psql -h 192.168.0.26 -U pguser -d dbpg -W`.

### 1.2. Conexión mediante Cliente Gráfico (pgAdmin 4)
He instalado la versión Desktop de pgAdmin 4. He registrado el servidor remoto apuntando a la base de datos `dbpg` y he establecido la conexión con éxito, visualizando el panel de rendimiento[cite: 16].
![Panel de pgAdmin 4 conectado](14.png)

---

## 2. MariaDB

### 2.1. Conexión mediante Cliente de Consola (mariadb-client)
Tras ajustar los permisos de red en el servidor, he realizado la conexión por terminal desde mi cliente utilizando el comando `mariadb -h 192.168.0.26 -u muser -p dbm`, logrando acceder al monitor de la base de datos[cite: 17].
![Conexión exitosa a MariaDB por consola](15.png)

### 2.2. Conexión mediante Cliente Web (phpMyAdmin)
He instalado Apache y phpMyAdmin, configurando el archivo `config.inc.php` para apuntar el host hacia la IP de mi servidor remoto. La interfaz web muestra correctamente la conexión al servidor y a la base de datos `dbm`[cite: 18].
![phpMyAdmin mostrando la base de datos dbm](16.png)

---

## 3. Oracle Database

### 3.1. Conexión mediante Oracle SQL Developer
Primero, he preparado el entorno instalando Java (JDK) y `unzip`[cite: 21], herramientas necesarias para ejecutar la aplicación. 
![Instalación de dependencias](02.png)

A continuación, he descargado el archivo `.zip` oficial sin JRE[cite: 22] y lo he descomprimido en el directorio `/opt/`[cite: 23].
![Descarga de SQL Developer](03.png)
![Descompresión del archivo](04.png)

He iniciado la aplicación ejecutando su script[cite: 24] y he accedido a la pantalla de bienvenida[cite: 25].
![Pantalla de carga de SQL Developer](05.png)
![Pantalla de bienvenida de SQL Developer](06.png)

Para integrarlo en el sistema, he creado un acceso directo (`.desktop`)[cite: 9]. Finalmente, he configurado una nueva conexión hacia el servicio remoto utilizando el usuario `orauser` y el nombre de servicio `FREEPDB1`[cite: 10].
![Creación del acceso directo de SQL Developer](07.png)
![Configuración de conexión en SQL Developer](08.png)

### 3.2. Conexión mediante Visual Studio Code
También he configurado VS Code como cliente alternativo para Oracle. He descargado el instalador `.deb` oficial para Linux[cite: 11] y he aceptado añadir los repositorios de Microsoft en el gestor de paquetes durante la instalación[cite: 12].
![Descarga de VS Code](09.png)
![Configuración de repositorios de VS Code](10.png)

Una vez instalado, he buscado y añadido la extensión oficial "Oracle SQL Developer for VS Code" desde el Marketplace[cite: 13].
![Instalación de la extensión de Oracle en VS Code](11.png)

Utilizando la interfaz de esta extensión, he creado la conexión al servicio `FREEPDB1` del servidor remoto en la IP `192.168.0.26`[cite: 14].
![Conexión a Oracle configurada en VS Code](12.png)

---

## 4. Clientes Multi-SGBD: DBeaver Community

He instalado el paquete `.deb` de DBeaver Community en la máquina cliente. A través de este cliente gráfico universal, he configurado y descargado los controladores JDBC correspondientes para conectarme de forma simultánea a los tres motores de bases de datos alojados en el servidor:

1. **PostgreSQL:** Conexión a `dbpg` con usuario `pguser`.
2. **MariaDB:** Conexión a `dbm` con usuario `muser`.
3. **Oracle Database:** Conexión al servicio `FREEPDB1` por el puerto `1521` con el usuario `orauser`.

En la siguiente imagen se comprueba el éxito de la operación al tener las tres conexiones activas y desplegadas en el mismo entorno[cite: 19].
![Ventana principal de DBeaver con PostgreSQL, MariaDB y Oracle](17.png)
