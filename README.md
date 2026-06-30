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
























