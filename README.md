with open(ruta + "Planilla_Stos_Rva_lmic_062026_Brok.txt") as f1:
    lineas_1 = f1.readlines()
<br>
for i, linea in enumerate(lineas_1):
    if "--------" in linea:
        fila_inicio = i+1
        break
<br>
encabezado = lineas_1[:fila_inicio]
encabezado_texto = "".join(encabezado)
detalle = "".join(lineas_1[fila_inicio:])
<br>
for i in range(fila_inicio, len(lineas_1)):
    print(i, repr(lineas_1[i]))
<br>
for i in range(7,17):
    linea_1 = lineas_1[i]
    print(''.join([str(i//10) for i in range(len(linea_1))]))
    print(''.join([str(i%10) for i in range(len(linea_1))]))
    print(linea_1)
<br>
rows_2 = lineas_1[8]
<br>
print("NUM                :", repr(rows_2[0:2]))
print("RAMO_PROD          :", repr(rows_2[2:8]))
print("POLIZA             :", repr(rows_2[12:20]))
print("ANEXO              :", repr(rows_2[24:28]))
print("ASEGURADO          :", repr(rows_2[28:54]))
print("NUMERO_SINIESTRO   :", repr(rows_2[54:74]))
print("FECHA_SINIESTRO    :", repr(rows_2[75:86]))
print("VALOR_SINIESTRO    :", repr(rows_2[98:113]))
print("PARTICIPACION      :", repr(rows_2[119:125]))
print("REASEGURADOR_VALOR :", repr(rows_2[133:145]))
<br>
registros_1 = []
<br>
for fila in lineas_1[fila_inicio:]:
    
    if not fila.strip():
        continue
    
    if fila.strip().startswith("Ramo..:"):
        continue
    
    registros_1.append({
        'NUM' : fila[0:2].strip(),
        'RAMO_PROD' : fila[2:6].strip(),
        'POLIZA' : fila[12:20].strip(),
        'ANEXO' : fila[25:28].strip(),
        'ASEGURADO' : fila[28:54].strip(),
        'NUMERO_SINIESTO' : fila[54:75].strip(),
        'FECHA_SINIESTRO' : fila[75:86].strip(),
        'VALOR_SINIESTRO' : fila[90:103].strip(),
        'PARTICIPACION' : fila[113:125].strip(),
        'REASEGURADOR_VALOR' : fila[125:145].strip()
    })
<br>
df_2  = pd.DataFrame(registros_1)
<br>
def limpiar_texto(valor):
    if isinstance(valor, str):
        return re.sub(r'[\x00-\x08\x0B-\x0C\x0E-\x1F\x7F-\x9F]', '', valor)
    return valor
<br>
df_2 = df_2.map(limpiar_texto)
<br>
with pd.ExcelWriter(
    ruta + "Planilla_Stos_Pagos_062026_Brok.xlsx", 
    engine="openpyxl"
) as writer:
    pd.DataFrame({'ENCABEZADO': encabezado}).to_excel(
        writer,
        sheet_name="Reporte", 
        index=False,
        header=False
    )
    df_2.to_excel(
        writer,
        sheet_name="Reporte",
        startrow=len(encabezado) + 2,
        index=False
    ) 
<br>
Tengo desarrollado el anterior proceso, basicamente lo que hace es leer un txt, identificar los encabezados y luego manualmente e identifica la posición de las columnas. Quiero ahora, si es posible, identificar la posición de las columnas de manera automatica, dado que ahora tengo un archivo con multiples tablas hacia abajo y posiblemente cada una tengo una estructura diferente, es decir, no todas las tablas tienen las mismas columnas. Cómo podría hacer esto?

######################################################
Mi archivo en cuestion es el siguiente, aclaro que lo siguiente solo es parte de las tablas pero más o menos hacia baja tiene la misma logica:
<br>
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:               518  HOWDEN CORREDORES DE REASEGURO                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MANEJO FIN        MANEJO FIN                                                                                                                         TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                   2,465,753.00                                                                                                                                            2,465,753.00
DEPOSITOS LIBERADOS              6,000,000.00                                                                                                                                            6,000,000.00
 TOTAL INGRESOS                  8,465,753.00                                                                                                                                            8,465,753.00
COMISION BASICA                    628,767.00                                                                                                                                              628,767.00
SINIESTROS PAGADOS                                  7,054,640.00                                                                                                                         7,054,640.00
DEPOSITOS RETENIDOS                246,575.00                                                                                                                                              246,575.00
RETENCION EN LA FUENTE/PRIM         24,657.53                                                                                                                                               24,657.53
 TOTAL EGRESOS                     899,999.53       7,054,640.00                                                                                                                         7,954,639.53
MOVIMIENTOS DEL PERIODO          7,565,753.47       7,054,640.00-                                                                                                                          511,113.47
 SALDO ACUMULADO                 7,565,753.47       7,054,640.00-                                                                                                                          511,113.47
SALDO ANTERIOR DE DEPOSITOS      6,000,000.00                                                                                                                                            6,000,000.00
 MOVTO NETO DEPOSITOS PERIO      5,753,425.00-                                                                                                                                           5,753,425.00-
 SALDO ACUMULADO DE DEPOSIT        246,575.00                                                                                                                                              246,575.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:               518  HOWDEN CORREDORES DE REASEGURO                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      RC                                                                                                                                                   TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                            .18                                                                                                                                                     .18
 SALDO ACUMULADO                          .18                                                                                                                                                     .18
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        8000678400  THB COLOMBIA S.A. CORREDORES D                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MIEMBROSJD        MIEMBROSJD        CASCO NAV.                                                                                                       TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                                                    2,959,620.00-                                                                                                     2,959,620.00-
 TOTAL INGRESOS                                                        2,959,620.00-                                                                                                     2,959,620.00-
SINIESTROS PAGADOS                                                    76,141,738.10                                                                                                     76,141,738.10
 TOTAL EGRESOS                                                        76,141,738.10                                                                                                     76,141,738.10
MOVIMIENTOS DEL PERIODO                                               79,101,358.10-                                                                                                    79,101,358.10-
SALDO ANTERIOR                  30,029,500.00      30,029,500.00-  5,047,875,873.66-                                                                                                 5,047,875,873.66-
NUESTRO PAGO                                                         219,090,901.00                                                                                                    219,090,901.00
SU PAGO                                                            5,242,267,200.20                                                                                                  5,242,267,200.20
 SALDO ACUMULADO                30,029,500.00      30,029,500.00-    103,800,932.56-                                                                                                   103,800,932.56-
SALDO ANTERIOR DE DEPOSITOS                                           59,570,867.00                                                                                                     59,570,867.00
 MOVTO NETO DEPOSITOS PERIO                                            2,959,620.00                                                                                                      2,959,620.00
 SALDO ACUMULADO DE DEPOSIT                                           62,530,487.00                                                                                                     62,530,487.00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                              256,499.99                                                                                                        256,499.99
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        8000678400  THB COLOMBIA S.A. CORREDORES D                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CASCO NAV.         R. CIVIL         CYBER             CYBER                                                                                          TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                      16,950.85          21,000.00                                                                                                                            37,950.85
 TOTAL INGRESOS                     16,950.85          21,000.00                                                                                                                            37,950.85
COMISION BASICA                      3,390.17           5,250.00                                                                                                                             8,640.17
DEPOSITOS RETENIDOS                  1,695.09           4,200.00                                                                                                                             5,895.09
 TOTAL EGRESOS                       5,085.26           9,450.00                                                                                                                            14,535.26
MOVIMIENTOS DEL PERIODO             11,865.59          11,550.00                                                                                                                            23,415.59
SALDO ANTERIOR                      13,769.30          10,936.08          13,741.42             301.68-                                                                                     38,145.12
NUESTRO PAGO                        25,633.94          19,135.16                                                                                                                            44,769.10
 SALDO ACUMULADO                          .95           3,350.92          13,741.42             301.68-                                                                                     16,791.61
SALDO ANTERIOR DE DEPOSITOS          8,222.01           4,050.41                                                                                                                            12,272.42
 MOVTO NETO DEPOSITOS PERIO          1,695.09           4,200.00                                                                                                                             5,895.09
 SALDO ACUMULADO DE DEPOSIT          9,917.10           8,250.41                                                                                                                            18,167.51
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        8300103854  ARTHUR J GALLAGHER RE COLOMBIA                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CYBER                                                                                                                                                TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
 SALDO ACUMULADO
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        8600523309  CARPENTER MARSH FAC COL. CORRE                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      LUCRO CES.        TERRORISMO        TERRORISMO        MANEJO FIN        MANEJO FIN        MANEJO FIN        RC                RC                     TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                   3,257,908.38      34,312,742.23      28,446,487.65-    324,017,568.55-      5,954,375.50-    813,543,779.05-    425,026,804.10-      4,498,458.90-  1,563,916,823.14-
NUESTRO PAGO                                                                                                                                     429,525,263.00-                       429,525,263.00-
 SALDO ACUMULADO                 3,257,908.38      34,312,742.23      28,446,487.65-    324,017,568.55-      5,954,375.50-    813,543,779.05-      4,498,458.90       4,498,458.90-  1,134,391,560.14-
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        8600523309  CARPENTER MARSH FAC COL. CORRE                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      LUCRO CES.        LUCRO CES.        TERRORISMO        TERRORISMO        TERRORISMO           PYME              PYME              PYME          CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                      80,534.99-                                                                                     22,854.81-
 SALDO ACUMULADO                    80,534.99-                                                                                     22,854.81-
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        8600523309  CARPENTER MARSH FAC COL. CORRE                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      RC                RC                TRANSPORTE        TRANSPORTE        TERRE PYME        TERRE PYME                                                 TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                                                  .47-                                                                                                              .47-
DEPOSITOS LIBERADOS                                                        7,127.92                                                                                                          7,127.92
 TOTAL INGRESOS                                                            7,127.45                                                                                                          7,127.45
COMISION BASICA                                                                 .06-                                                                                                              .06-
DEPOSITOS RETENIDOS                                                             .05-                                                                                                              .05-
RETENCION EN LA FUENTE/PRIM                                                    3.06                                                                                                              3.06
 TOTAL EGRESOS                                                                 2.95                                                                                                              2.95
MOVIMIENTOS DEL PERIODO                                                    7,124.50                                                                                                          7,124.50
SALDO ANTERIOR                          80.00                             11,034.21             182.49         103,001.87                                                                   10,908.77
 SALDO ACUMULADO                        80.00                             18,158.71             182.49         103,001.87                                                                   18,033.27
SALDO ANTERIOR DE DEPOSITOS                                                7,127.92                                                                                                          7,127.92
 MOVTO NETO DEPOSITOS PERIO                                                7,127.97-                                                                                                         7,127.97-
 SALDO ACUMULADO DE DEPOSIT                                                     .05-                                                                                                              .05-
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                               10,435.07                                                                                                         10,435.07


Cómo instalar una versión anterior de SQLTools

Ve a Extensions (Ctrl+Shift+X)
Busca SQLTools y haz clic en el engranaje ⚙️ que aparece al lado
Selecciona "Install Another Version..."
Te aparece una lista de todas las versiones disponibles
Prueba con versiones anteriores a la actual — empieza por una que tenga unos meses de antigüedad y ve bajando si sigue pidiendo Node

Lo mismo para SQLTools SQLite (el driver):

También necesitas bajar su versión en paralelo, porque las versiones del driver y la extensión base deben ser compatibles entre sí

El problema real de este enfoque
Te lo digo con franqueza para que tomes la mejor decisión: bajar versiones de extensiones en VS Code es una solución frágil porque:

VS Code tiende a actualizar las extensiones automáticamente, y un día te despiertas con la versión nueva otra vez y el mismo problema
Puedes desactivar las actualizaciones automáticas, pero entonces te quedas sin correcciones de bugs o mejoras de seguridad
La compatibilidad entre versiones del driver y la extensión base puede ser complicada de mantener manualmente

Mi recomendación honesta
Dado todo lo que hemos visto en esta conversación, el camino más estable para tu caso tiene dos opciones claras:
Si quieres interfaz visual para las consultas (escribir SQL y ver tablas sin código Python) → instala DB Browser for SQLite (sqlitebrowser.org). Es una aplicación independiente, gratuita, sin Node, sin extensiones, y es exactamente lo que necesitas para explorar y consultar tu base visualmente. Abre tu Base_Central.db directamente.
Si prefieres quedarte en VS Code → sigue con el notebook de Python que ya tienes armado. Para tu flujo de reaseguros (consultar + exportar a Excel) es suficiente y más robusto que depender de versiones específicas de extensiones.
¿Quieres que te guíe con DB Browser for SQLite? Es la alternativa más limpia si quieres la experiencia visual de escribir SQL y ver resultados en tabla, sin depender de Node.


import sqlite3
import pandas as pd
from pathlib import Path

# Ajusta esta ruta a donde tengas tu archivo .db
RUTA_BASE = "Base_Central.db"

conn = sqlite3.connect(RUTA_BASE)
print(f"Conectado a: {RUTA_BASE}")

def consultar(query: str, connection=conn) -> pd.DataFrame:
    """Ejecuta una consulta SQL y devuelve el resultado como DataFrame."""
    return pd.read_sql(query, connection)


def listar_tablas(connection=conn) -> pd.DataFrame:
    """Lista todas las tablas existentes en la base."""
    return consultar("SELECT name FROM sqlite_master WHERE type='table';", connection)


def info_tabla(nombre_tabla: str, connection=conn) -> pd.DataFrame:
    """Muestra las columnas y tipos de una tabla específica."""
    return consultar(f"PRAGMA table_info({nombre_tabla});", connection)


def exportar_excel(df: pd.DataFrame, nombre_archivo: str, carpeta: str = "exportes") -> None:
    """Exporta un DataFrame a Excel dentro de la carpeta indicada (la crea si no existe)."""
    Path(carpeta).mkdir(exist_ok=True)
    ruta_completa = Path(carpeta) / nombre_archivo
    df.to_excel(ruta_completa, index=False)
    print(f"Exportado: {ruta_completa.resolve()}")

# Vista rápida de una tabla
consultar("SELECT * FROM Incurridos_Generales LIMIT 10;")

# Ejemplo: filtrar por fecha y ramo, sumando montos
query_ejemplo = """
SELECT
    Ramo,
    SUM(Monto) AS Total_Incurrido
FROM Incurridos_Generales
WHERE Fecha >= '2026-01-01'
GROUP BY Ramo
ORDER BY Total_Incurrido DESC;
"""

resultado = consultar(query_ejemplo)
resultado

exportar_excel(resultado, "Incurridos_por_Ramo.xlsx")

conn.close()
print("Conexión cerrada.")



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

<img width="959" height="502" alt="image" src="https://github.com/user-attachments/assets/70370aa9-044f-4f48-b543-76d336c8326b" />

l
























