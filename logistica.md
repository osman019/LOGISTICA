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


![alt text](image.png)