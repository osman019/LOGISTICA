ENTIDADES 
Asignación de Ruta
id_asignacion
id_ruta
id_vehiculo
id_conductor
id_auxiliar
2. Ruta
id_ruta
descripcion
id_sucursal_origen
id_sucursal_destino
3. Vehículo
id_vehiculo
placa
modelo
id_conductor
4. Conductor
id_conductor
nombre_conductor
licencia_conductor
5. Auxiliar
id_auxiliar
nombre_auxiliar
6. Paquete
id_paquete
numero_seguimiento
peso
dimensiones
contenido
valor_declarado
tipo_servicio
destino
id_cliente
7. Cliente
id_cliente
nombre_cliente
correo
direccion
telefono
8. Ciudad
id_ciudad
nombre_ciudad
id_pais
9. País
id_pais
nombre_pais
10. Sucursal
id_sucursal
nombre_sucursal
direccion
id_ciudad
11. Envío
id_envio
id_paquete
estado_envio
id_sucursal_origen
id_sucursal_destino
fecha_envio
fecha_entrega
12. Seguimiento
id_seguimiento
id_paquete
fecha_hora
ubicacion_actual
estado_actual



Relaciones y Cardinalidad
Asignación de Ruta:

1 a 1 con Ruta
1 a 1 con Vehículo
1 a 1 con Conductor
1 a 1 con Auxiliar
Ruta:

N a 1 con Sucursal (Origen)
N a 1 con Sucursal (Destino)
Paquete:

N a 1 con Cliente
Envio:

N a 1 con Paquete
N a 1 con Sucursal (Origen)
N a 1 con Sucursal (Destino)
Seguimiento:

N a 1 con Paquete
Sucursal:

N a 1 con Ciudad
Ciudad:

N a 1 con País
Vehículo:

N a 1 con Conductor
Cliente:

N a 1 con Ciudad
Conductor:

1 a N con Vehículo


MODELO FISICO

ASIGANCION DE RUTA
CREATE TABLE `asignacion_ruta` (
  `id_asignacion` int NOT NULL AUTO_INCREMENT,
  `id_ruta` int DEFAULT NULL,
  `id_vehiculo` int DEFAULT NULL,
  `id_conductor` int DEFAULT NULL,
  `id_auxiliar` int DEFAULT NULL,
  PRIMARY KEY (`id_asignacion`),
  KEY `id_ruta` (`id_ruta`),
  KEY `id_vehiculo` (`id_vehiculo`),
  KEY `id_conductor` (`id_conductor`),
  KEY `id_auxiliar` (`id_auxiliar`),
  CONSTRAINT `asignacion_ruta_ibfk_1` FOREIGN KEY (`id_ruta`) REFERENCES `ruta` (`id_ruta`),
  CONSTRAINT `asignacion_ruta_ibfk_2` FOREIGN KEY (`id_vehiculo`) REFERENCES `vehiculo` (`id_vehiculo`),
  CONSTRAINT `asignacion_ruta_ibfk_3` FOREIGN KEY (`id_conductor`) REFERENCES `conductor` (`id_conductor`),
  CONSTRAINT `asignacion_ruta_ibfk_4` FOREIGN KEY (`id_auxiliar`) REFERENCES `auxiliar` (`id_auxiliar`)
)

AUXILIAR
CREATE TABLE `auxiliar` (
  `id_auxiliar` int NOT NULL AUTO_INCREMENT,
  `nombre_auxiliar` varchar(100) NOT NULL,
  PRIMARY KEY (`id_auxiliar`)
)

CIUDAD
CREATE TABLE `ciudad` (
  `id_ciudad` int NOT NULL AUTO_INCREMENT,
  `nombre_ciudad` varchar(100) NOT NULL,
  `id_pais` int DEFAULT NULL,
  PRIMARY KEY (`id_ciudad`),
  KEY `id_pais` (`id_pais`),
  CONSTRAINT `ciudad_ibfk_1` FOREIGN KEY (`id_pais`) REFERENCES `pais` (`id_pais`)
) 



CLIENTE
CREATE TABLE `cliente` (
  `id_cliente` int NOT NULL AUTO_INCREMENT,
  `nombre_cliente` varchar(100) NOT NULL,
  `correo` varchar(100) NOT NULL,
  `direccion` varchar(255) DEFAULT NULL,
  `telefono` varchar(20) DEFAULT NULL,
  PRIMARY KEY (`id_cliente`)
)

CONDUCTOR
CREATE TABLE `conductor` (
  `id_conductor` int NOT NULL AUTO_INCREMENT,
  `nombre_conductor` varchar(100) NOT NULL,
  `licencia_conductor` varchar(50) NOT NULL,
  PRIMARY KEY (`id_conductor`)
)

ENVIO 
CREATE TABLE `envio` (
  `id_envio` int NOT NULL AUTO_INCREMENT,
  `id_paquete` int DEFAULT NULL,
  `estado_envio` enum('recibido','en tránsito','entregado','retenido en aduana') NOT NULL,
  `id_sucursal_origen` int DEFAULT NULL,
  `id_sucursal_destino` int DEFAULT NULL,
  `fecha_envio` date DEFAULT NULL,
  `fecha_entrega` date DEFAULT NULL,
  PRIMARY KEY (`id_envio`),
  KEY `id_paquete` (`id_paquete`),
  KEY `id_sucursal_origen` (`id_sucursal_origen`),
  KEY `id_sucursal_destino` (`id_sucursal_destino`),
  CONSTRAINT `envio_ibfk_1` FOREIGN KEY (`id_paquete`) REFERENCES `paquete` (`id_paquete`),
  CONSTRAINT `envio_ibfk_2` FOREIGN KEY (`id_sucursal_origen`) REFERENCES `sucursal` (`id_sucursal`),
  CONSTRAINT `envio_ibfk_3` FOREIGN KEY (`id_sucursal_destino`) REFERENCES `sucursal` (`id_sucursal`)
) 



PAIS
CREATE TABLE `pais` (
  `id_pais` int NOT NULL AUTO_INCREMENT,
  `nombre_pais` varchar(100) NOT NULL,
  PRIMARY KEY (`id_pais`)
)

PAQUETE
CREATE TABLE `paquete` (
  `id_paquete` int NOT NULL AUTO_INCREMENT,
  `numero_seguimiento` varchar(50) NOT NULL,
  `peso` decimal(10,2) NOT NULL,
  `dimensiones` varchar(100) DEFAULT NULL,
  `contenido` text,
  `valor_declarado` decimal(10,2) DEFAULT NULL,
  `tipo_servicio` enum('nacional','internacional','exprés','estándar') NOT NULL,
  `destino` varchar(255) NOT NULL,
  `id_cliente` int DEFAULT NULL,
  PRIMARY KEY (`id_paquete`),
  KEY `id_cliente` (`id_cliente`),
  CONSTRAINT `paquete_ibfk_1` FOREIGN KEY (`id_cliente`) REFERENCES `cliente` (`id_cliente`)
)

RUTA
CREATE TABLE `ruta` (
  `id_ruta` int NOT NULL AUTO_INCREMENT,
  `descripcion` varchar(255) NOT NULL,
  `id_sucursal_origen` int DEFAULT NULL,
  `id_sucursal_destino` int DEFAULT NULL,
  PRIMARY KEY (`id_ruta`),
  KEY `id_sucursal_origen` (`id_sucursal_origen`),
  KEY `id_sucursal_destino` (`id_sucursal_destino`),
  CONSTRAINT `ruta_ibfk_1` FOREIGN KEY (`id_sucursal_origen`) REFERENCES `sucursal` (`id_sucursal`),
  CONSTRAINT `ruta_ibfk_2` FOREIGN KEY (`id_sucursal_destino`) REFERENCES `sucursal` (`id_sucursal`)
)




SEGUIMIENTO
CREATE TABLE `seguimiento` (
  `id_seguimiento` int NOT NULL AUTO_INCREMENT,
  `id_paquete` int DEFAULT NULL,
  `fecha_hora` datetime NOT NULL,
  `ubicacion_actual` varchar(255) DEFAULT NULL,
  `estado_actual` enum('recibido','en tránsito','entregado','retenido en aduana') NOT NULL,
  PRIMARY KEY (`id_seguimiento`),
  KEY `id_paquete` (`id_paquete`),
  CONSTRAINT `seguimiento_ibfk_1` FOREIGN KEY (`id_paquete`) REFERENCES `paquete` (`id_paquete`)
)

SUCURSAL
CREATE TABLE `sucursal` (
  `id_sucursal` int NOT NULL AUTO_INCREMENT,
  `nombre_sucursal` varchar(100) NOT NULL,
  `direccion` varchar(255) NOT NULL,
  `id_ciudad` int DEFAULT NULL,
  PRIMARY KEY (`id_sucursal`),
  KEY `id_ciudad` (`id_ciudad`),
  CONSTRAINT `sucursal_ibfk_1` FOREIGN KEY (`id_ciudad`) REFERENCES `ciudad` (`id_ciudad`)
)

VEHICULO
CREATE TABLE `vehiculo` (
  `id_vehiculo` int NOT NULL AUTO_INCREMENT,
  `placa` varchar(10) NOT NULL,
  `modelo` varchar(100) DEFAULT NULL,
  `id_conductor` int DEFAULT NULL,
  PRIMARY KEY (`id_vehiculo`),
  KEY `id_conductor` (`id_conductor`),
  CONSTRAINT `vehiculo_ibfk_1` FOREIGN KEY (`id_conductor`) REFERENCES `conductor` (`id_conductor`)
) 








![alt text](image.png)