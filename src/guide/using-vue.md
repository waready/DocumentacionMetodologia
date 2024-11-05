# Requisitos previos a convertir

## Bantotal

Al momento de recibir los modelos del cliente, tratar de compilar la KB de manera masiva en GX8. En caso de no compilar devolver al cliente.

## Cliente

* Solicitar KBs que compilen en GX8. Cuando recibimos tratamos de compilar en GX8, si no compila, devolvemos.

* Solicitar SP, Funciones, CL (según corresponda), y toda programación no GX que no esté en las KB.

* Solicitar nomenclaturas de tablas y programas que debemos convertir.

* Solicitar al cliente query con lista de cantidad de tablas que se tiene en producción actualmente (armar query)

* Solicitar KB de WF separada. En el resto de KBS no pueden existir objetos WF.

* Solicitar el repositorio de clases con nomenclatura particular de Producción, y validar que no faltan programas en las KB. Si faltan, comunicar al cliente.

* nuevo enlace