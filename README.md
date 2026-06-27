---------------------------------------------------------------------------
OverflowError                             Traceback (most recent call last)
Cell In[15], line 5
      1 Incurridos_Generales = pd.read_excel(Path_Incurridos + "SENT INCURRIDOS GENERALES_31032026.xlsx", sheet_name='GCExcel 1', engine='openpyxl')
      2 Incurridos_Vida = pd.read_excel(Path_Incurridos + 'SENT INCURRIDOS VIDA 31032026.xlsx', sheet_name='GCExcel 1', engine='openpyxl')
      3 
      4 conn = sqlite3.connect("Base_Central")
----> 5 Incurridos_Generales.to_sql("Incurridos_Generales", conn, if_exists='replace', index=False)
      6 Incurridos_Vida.to_sql("Incurridos_Vida", conn, if_exists='replace', index=False)
      7 conn.close

File c:\Users\Luis.Pereguez\AppData\Local\Programs\Python\Python314\Lib\site-packages\pandas\core\generic.py:3052, in NDFrame.to_sql(self, name, con, schema, if_exists, index, index_label, chunksize, dtype, method)
   3048         3
   3049         """  # noqa: E501
   3050         from pandas.io import sql
   3051 
-> 3052         return sql.to_sql(
   3053             self,
   3054             name,
   3055             con,

File c:\Users\Luis.Pereguez\AppData\Local\Programs\Python\Python314\Lib\site-packages\pandas\io\sql.py:841, in to_sql(frame, name, con, schema, if_exists, index, index_label, chunksize, dtype, method, engine, **engine_kwargs)
    836     raise NotImplementedError(
    837         "'frame' argument should be either a Series or a DataFrame"
    838     )
...
-> 2571     conn.executemany(self.insert_statement(num_rows=1), data_list)
   2572 except Error as exc:
   2573     raise DatabaseError("Execution failed") from exc

OverflowError: Python int too large to convert to SQLite INTEGER



Estimado equipo de TI / [Nombre del responsable],

Por medio del presente correo solicito autorización para instalar SQL Server Express (o Developer Edition) en mi equipo corporativo.

Actualmente cuento con SQL Server Management Studio 22 (SSMS) instalado, el cual es la interfaz gráfica para administrar y consultar bases de datos. Sin embargo, para que esta herramienta funcione correctamente, requiere conectarse a una instancia del motor de base de datos SQL Server, la cual no se encuentra instalada en el equipo.

Al intentar conectarme, el sistema arroja el siguiente error:
"Error relacionado con la red o específico de la instancia mientras se establecía una conexión con el servidor SQL Server. No se encontró el servidor o éste no estaba accesible."

Esta instalación es necesaria para [indicar aquí el propósito: desarrollo de aplicaciones, pruebas locales, capacitación, etc.]. La edición solicitada es gratuita y de uso exclusivo para entornos de desarrollo, por lo que no representa costo adicional para la compañía.

Quedo atento a su respuesta y a cualquier procedimiento interno que deba seguir para gestionar esta solicitud.


https://drive.google.com/file/d/1m8m0aQDfvAXEUCEOvE0MIVMwxiXUGbMA/view

https://drive.google.com/file/d/10vsir64GmyDzjLR2rJM0XVS3OBc2ZcI5/view

https://drive.google.com/file/d/1FfHbg1asN8m8lwSrGks1VinBsmpd-Yf2/view

https://drive.google.com/file/d/1ke4KqMO6syeP-usYnIKKM6U6QfQZxWnJ/view

https://drive.google.com/file/d/1RR4DdF1tYSqNONG8m3lXAFc68sqMCjjE/view

https://drive.google.com/file/d/1KTOcXSpfhrXvzeeB83kOIf7qT0GRcuES/view

<img width="778" height="473" alt="image" src="https://github.com/user-attachments/assets/e9a3b84a-e284-45c0-b8ff-1fe359a44014" />


















