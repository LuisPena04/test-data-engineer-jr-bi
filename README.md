# Ejercicio práctico para Data Engineer Jr BI en Deacero.

En caso de estar interesado en aplicar al test puede contactar por correo a <lsilva@deacero.com>

Debe realizar un fork de este repositorio para desarrollar y entregar su trabajo.

1. Conocimiento teórico.
  - ¿Qué es una base de datos?
    * Es un almacén o conjunto de datos estructurados o no estructurados con una relación entre sus tablas, que cumplen algún objetivo en específico
  - ¿A qué hace regerencia la integridad en Base de datos?
    * Al que la información se almacene correctamente, sin alterar o modificar los datos que lo hagan erroneo.
  - ¿Cuál es el campo que dentro del registro permite la identificación exclusiva y univoca de cada registro?
    * Primary Key
  - ¿El comando ALTER TABLE se utiliza para crear una nueva tabla en la base de datos?
    *No
  - ¿Con que sentencia borras información?
    * DELETE or TRUNCATE
  - ¿Qué palabra clave se usa para filtrar información?
    * WHERE
  - ¿Como se le llama al diagrama que ayuda a visualizar la relación entre tablas de una base de datos?
    * Modelo de entidad - relación
  - ¿Cuál es la sentencia para crear un procedimiento almacenado?
    * CREATE PROCEDURE 
  - ¿Cuál es el comando que se utiliza para ver campos vacíos o desconocidos?
    * WHERE IS NULL
  - ¿Cuál es el comando que crea un objeto dentro de una base de datos?
    * CREATE

2. Ejercicio práctico.  
Dentro de la carpeta data se encuentra el archivo `Examen Práctico.xlsx` en el cual cada hoja del documento hace referencia a una tabla SQL, tomando como base este documento, conteste lo siguiente:
  - Que script se utilizaría para conocer el dato de:
    1. Insertar un registro en la tabla Tbl_Recuperacion
       * INSERT INTO Tbl_Recuperacion (AnioMes, ClaCliente, ImpRecuperacion)
       * VALUES ('202308','120', 200.10)
    3. Eliminar de la tabla Dim_Cliente los registros de los clientes que pertenezcan al AgrupadorCliente 543.
       * DELETE Dim_Cliente
       * WHERE ClaAgrupadorCliente='543'
    5. Conocer el valor Total de ImpRecuperacion e ImpObjetivo por cliente correspondiente al año anterior (2020).
       * SELECT DC.ClaCliente, NombreCliente, SUM(ImpRecuperacion) as ImpRecuperacion,  SUM(ImpObjetivo) as ImpObjetivo
       * FROM Dim_Cliente DC
       * INNER JOIN Tbl_Recuperacion TblRec ON DC.ClaCliente=TblRec.ClaCliente
       * INNER JOIN Tbl_Objetivo TblObj ON DC.ClaCliente=TblObj.ClaCliente
       * WHERE TblRec.AnioMes LIKE '2020%' 
       * GROUP BY DC.ClaCliente,NombreCliente
    7. Conocer el valor de %ImpRecuperacion utilizando la fórmula: ImpRecuperacion / (ImpObjetivo(Mes Anterior) - ImpBonificacion)
       * SELECT DC.ClaCliente,NombreCliente, TblRec.AnioMes,
                SUM(ImpRecuperacion) / (
                 (SELECT SUM(ImpObjetivo)
                 WHERE DATEADD(Month,-1,DATE(LEFT(TblRec.AnioMes,4),RIGTH(TblRec.AnioMes,2),'01'))
                 - SUM(ImpBonificacion)) AS %ImpRecuperacion
       * FROM Dim_Cliente DC
       * INNER JOIN Tbl_Recuperacion TblRec ON DC.ClaCliente=TblRec.ClaCliente
       * INNER JOIN Tbl_Objetivo TblObj ON DC.ClaCliente=TblObj.ClaCliente
       * INNER JOIN Tbl_Bonificacion TblBon ON DC.ClaCliente=TblBon.ClaCliente
       * GROUP BY DC.ClaCliente,NombreCliente,TblRec.AnioMes

  - Utilizando la herramienta Tableau (versión libre o de prueba) diseñe un dashboard que represente los datos de: ImpRecuperacion, ImpObjetivo e ImpBonificaciones de cada cliente y por periodo mensual. Nota: Sobre la página oficial de Tableau puede descargar la versión de prueba, la liga de descarga es: https://www.tableau.com/support/releases/desktop/2021.1.1

  - Dentro de la carpeta data se encuentra el archivo `SP.txt`, este contiene un Stored Procedure que se utiliza para generar las estrellas, mencione que es lo que realiza el procedimiento y que resultado arroja.


Todas las respuestas pueden hacerse en un documento con la herramienta que mejor le convenga. El dashboard puede ser publicado en tableu public y agregar la liga o presentar el reporte en archivo PDF o HTML.

Una vez concluido el reto se debe comunicar al correo correspondiente con la liga al repositorio de github final para evaluar las respuestas.

Suerte a todos!!! :metal: :nerd_face: :computer:
