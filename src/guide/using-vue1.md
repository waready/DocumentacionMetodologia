# Preparación Modelo Básico y conversión masiva



## 1.	Revisar propiedades modelos GX16.

Una vez configurado el modelo compilar uno o dos objetos (identificar objetos con fechas, etc). Luego revisar .java >> hacer checklist de que revisar en el .java


<img :src="$withBase('/img/01.png')" class="center">


<img :src="$withBase('/img/02.png')" class="center">


<img :src="$withBase('/img/03.png')" class="center">


<img :src="$withBase('/img/04.png')" class="center">


<img :src="$withBase('/img/05.png')" class="center">


`Custom JDBC driver:	com.microsoft.sqlserver.jdbc.SQLServerDriver`
`Custom JDBC URL: 	 jdbc:sqlserver://<server>:1433;databaseName=<DBName>;SelectMethod=cursor`

a Previo a CACHE_TTL_0
     ENABLE_CACHE_FILE=0

b Agregar debajo de USE_JDBC_DATASOURCE
    JDBC_DRIVER=com.microsoft.sqlserver.jdbc.SQLServerDriver
    
`DB_URL=jdbc:sqlserver://fuentes2019:1433;databaseName=btwebgx16;SelectMethod=cursor`


<img :src="$withBase('/img/06.png')" class="center">

`Custom JDBC URL: jdbc:oracle:thin:@<server>:1521:btweb`

a Debajo de DB_URL agregar la siguiente línea
    `JDBC_URL_EXTRA=SetBigStringTryClob=true;oracle.net.CONNECT_TIMEOUT=10000000;oracle.jdbc.ReadTimeout=60000`

b Agregar al final		
    GENERATE_DB_AUDIT_INFO=0
    APPLICATION_NAME=FuentesGx16Orcl
    IS_FULL_SERVICES=1

<img :src="$withBase('/img/07.png')" class="center">


## KB Preferences – Java generator


* **Classpath**: copiarse directorio ExObjects y añadir los .jar

```bh E:\ExObjectsGx16\gxclass16u9.jar;E:\ExObjectsGx16\gxcommon16u9.jar;E:\ExObjectsGx16\serverextensions.jar;E:\ExObjectsGx16\ActiveDirectory.jar;
E:\ExObjectsGx16\ojdbc10.jar;E:\ExObjectsGx16\service.jar;E:\ExObjectsGx16\SSOBA.jar;E:\ExObjectsGx16\xercesImpl.jar;E:\ExObjectsGx16\procser.jar;
E:\ExObjectsGx16\BTReporting.jar;E:\ExObjectsGx16\btsdl.jar;E:\ExObjectsGx16\BTInvoker_prod.jar;E:\ExObjectsGx16\btv4context.jar;
E:\ExObjectsGx16\btservices16.jar;E:\ExObjectsGx16\DynamicSQL.jar;E:\ExObjectsGx16\opentracing-jaeger.jar;E:\ExObjectsGx16\EventBus-3.1.jar;
E:\ExObjectsGx16\GXOpenTracing-1.0.jar;E:\ExObjectsGx16\BTScreenMeta.jar;E:\ExObjectsGx16\jcifs-1.2.9.jar;E:\ExObjectsGx16\KerberosLogin.jar;
E:\ExObjectsGx16\log4j-api-2.3.jar;E:\ExObjectsGx16\log4j-core-2.3.jar;E:\ExObjectsGx16\log4j-1.2.16.jar;E:\ExObjectsGx16\servlet-api.jar
```


* **Compilador**: AdoptOpenJDK\jdk-11.0.5.10-hotspot


* **List of external SP (AS)**

*  PP006SRV FX00313 PP014RPG FX00113 PBATCALL PBATCA4 PBAT098 PCSW007F PP014JAS PFXRP000 PFXRW000 RFXRP100 PBPS834 PBSA440 PR51021 PR51024 PBPA546 PBPA547 PBPA548 PBPA604 PFCWTP10 PFCWTP20 PFCWTP30 PFCWTP31 PFCWTP40 PVALW005 PFCW1100 PFCWDF10  PBPH002 PBCX003 PBCX004 PBPA849 PBCGN102 PFCWCORP PFCW1100 PCMXR103 QSIGNON PRTEOPCC GETCL PPLS019D PTDDEBUG RFXRP500 rfxrp650 pfxrp001 pfxrw001 pcv00007 prgap014 ppls020p rfs00192 PZ0E4042 execsql ppls016i ppls061 pfct653 PFXRW000 px9996a8 bTCALL PIF00159 PFXGXN98 RFXRP200 PJBUHG3 PPLS020X FX00513 PJBXI252 PJBXP700 PFXBVS65 PPLS075 ZONANUM PSNW0105 PW103SV1 PP006RBX RP014JP5 qcmdexc PW103SRV PP014JASUs EXECSQL


<img :src="$withBase('/img/09.png')" class="center">

<img :src="$withBase('/img/10.png')" class="center">

<img :src="$withBase('/img/11.png')" class="center">

## CONFIG.GX en directorio de la KB

Es necesario que cada KB contenga en el directorio principal el archivo CONFIG.GX con las siguientes entradas:
FMT_NAME=T
Statement_Id_Prefix = W*
DoNotTranslateLiterals=y

<img :src="$withBase('/img/12.png')" class="center">



::: tip Nota
Es importante y recomendado verificar la existencia del archivo, así como revisar las preferencias de la KB cuando se descarga una KB institucional.
Cuando se convierte una KB desde otra versión o se crea una nueva es imprescindible. El no hacerlo llevará a regenerar todos los objetos de la KB cuando se detecte que las clases fueron mal generadas.
:::

::: warning advertencia
This is a warning
:::

::: danger
This is a dangerous warning
:::

::: details
This is a details block, which does not work in IE / Edge
:::


## Entradas en CONFIG.GX

### FMT_NAME=T

Utilizada por el generador RPG para que las tablas se impacten sin el prefijo T de la transacción

### Statement_Id_Prefix = *

Asigna un prefijo a cada cursor generado en los programas. Estos son únicos en una KB, pero no entre KB distintas, pudiendo generar conflictos

<img :src="$withBase('/img/13.png')" class="center">

### DoNotTranslateLiterals=y

Esta propiedad hace que no se genere la invocación a una función asociada a cada texto de Bantotal, incluyendo procedimientos, para traducir los mismos. Está asociada a la propiedad Translation type= Runtime, la cual se definió con otro propósito. No tenerla impacta enormemente en la performance.
2.	Sobre la KB básica consolidar todos los xpz de GX16. Antes de convertir analizar y buscar programas que estén en más de una KB (query para identificar).

Alternativa: por cada modelo tomar los objetos y exportar. Luego sobre el objeto .gxl sacar la lista de los objetos para comparar en cada modelo si se encuentra repetido.
 
3.	 KB básica y Producción Básica con los objetos FR* que tomamos como inicial. Se consolidan objetos y se impactan atributos. El método de copiado de clases, pasarlo por la herramienta Copy.bat
  Hacer un modelo básico y publicarlo en un repo para tenerlo.

4.	Mantener un traza y log del pasaje de datos. Identificar que dio error. Si el cliente tiene WF, se debe dejar BKP de las tablas de V8.
 
5.	 Armar Bitácora compartida donde indiquemos: (consultar a Gaucho doc ejemplo)
Fecha generación KBs,
Fecha de cambio de propiedades,
Fecha de regeneraciones,
Etc.
Esto nos sirve para luego cotejar con la fecha de los programas y poder identificar más rápido errores.
 
> definir procedimiento, comunicación previa y alguien que lleve el orden de como se van a hacer las cosas.



