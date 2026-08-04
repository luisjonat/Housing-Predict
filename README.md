---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[13], line 34
     30     for linea in bloque[idx_participacion+1:]:
     31         if not linea.strip() or es_separador(linea):
     32             continue
     33 
---> 34         concepto = cortar(linea, *colspecs[0])
     35         if not concepto:
     36             continue
     37 

Cell In[5], line 29, in cortar(linea, ini, fin)
     25         return ""
     26     if fin is None:
     27         return linea[ini:].strip()
     28 
---> 29     return linea[ini:fin].strip()

TypeError: slice indices must be integers or None or have an __index__ method

registros = []

for n, idx in enumerate(idx_corredor):
    fin_bloque = idx_corredor[n+1] if n+1 < len(idx_corredor) else len(lineas)
    bloque = lineas[idx:fin_bloque]
    
    m = patron_corredor.search(bloque[0])
    meta = m.groupdict() if m else {"cod": None, "nombre": None, "periodo": None, "moneda": None}
    
    idx_ramos = next((i for i, l in enumerate(bloque) if "R A M O S" in l), None)
    
    if idx_ramos is None:
        continue
    
    linea_ramos = bloque[idx_ramos]
    nombres_ramo = [cortar(linea_ramos, ini, fin) for ini, fin in colspecs[1:-1]]
    
    etiqueta_total = cortar(linea_ramos, *colspecs[-1])
    
    idx_participacion = next((i for i, l in enumerate(bloque) if l.count('%') >= 5), None)
    
    if idx_participacion is None:
        continue
    
    ancho = colspecs[1][1] - colspecs[1][0]
    centros = [ini + ancho/2 for ini, fin in colspecs[1:]]
    offset_datos = colspecs[0][1]
    
    
    for linea in bloque[idx_participacion+1:]:
        if not linea.strip() or es_separador(linea):
            continue
        
        concepto = cortar(linea, *colspecs[0])
        if not concepto:
            continue
        
        resto = linea[offset_datos:]
        for tok in re.finditer(r'\S+', resto):
            centro_tok = offset_datos + (tok.start() + tok.end())/2
            j = min(range(len(centros)), key=lambda k: abs(centros[k] - centro_tok))
            
            if j == len(centros) -1:
                ramo_col = ramo_nombre = etiqueta_total, etiqueta_total
            else:
                ramo_col, ramo_nombre = j+1, nombres_ramo[j]
                
            registros.append({
                "Corredor_Codigo": meta["cod"],
                "Corredor_nombre": meta["nombre"],
                "Periodo": meta["periodo"],
                "Moneda": meta["moneda"],
                "Ramo_Col": ramo_col,
                "Ramo_Nombre": ramo_nombre,
                "Concepto": concepto,
                "Valor": tok.group(),
            })

---------
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
Cell In[12], line 34
     30     for linea in bloque[idx_participacion+1:]:
     31         if not linea.strip() or es_separador(linea):
     32             continue
     33 
---> 34         concepto = cortar(linea, *colspecs[0])
     35         if not concepto:
     36             continue
     37 

Cell In[5], line 29, in cortar(linea, ini, fin)
     25         return ""
     26     if fin is None:
     27         return linea[ini:].strip()
     28 
---> 29     return linea[ini:fin].strip()

TypeError: slice indices must be integers or None or have an __index__ method
###############                                                                                     
                                                                                     
                                                                                     
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
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        9008903694  BRS INTERNATIONAL LATAM CORRED                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      RC                                                                                                                                                   TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                 295,844,250.00                                                                                                                                          295,844,250.00
 TOTAL INGRESOS                295,844,250.00                                                                                                                                          295,844,250.00
COMISION BASICA                 87,274,054.00                                                                                                                                           87,274,054.00
DEPOSITOS RETENIDOS             59,168,850.00                                                                                                                                           59,168,850.00
RETENCION EN LA FUENTE/PRIM      2,958,442.50                                                                                                                                            2,958,442.50
 TOTAL EGRESOS                 149,401,346.50                                                                                                                                          149,401,346.50
MOVIMIENTOS DEL PERIODO        146,442,903.50                                                                                                                                          146,442,903.50
NUESTRO PAGO                   445,410,193.00                                                                                                                                          445,410,193.00
 SALDO ACUMULADO               298,967,289.50-                                                                                                                                         298,967,289.50-
 MOVTO NETO DEPOSITOS PERIO     59,168,850.00                                                                                                                                           59,168,850.00
 SALDO ACUMULADO DE DEPOSIT     59,168,850.00                                                                                                                                           59,168,850.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:        9008903694  BRS INTERNATIONAL LATAM CORRED                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                       R. CIVIL                                                                                                                                            TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                  2,660.00                                                                                                                                                2,660.00
 TOTAL INGRESOS                      2,660.00                                                                                                                                                2,660.00
MOVIMIENTOS DEL PERIODO              2,660.00                                                                                                                                                2,660.00
SALDO ANTERIOR                       1,180.77                                                                                                                                                1,180.77
NUESTRO PAGO                         2,180.93                                                                                                                                                2,180.93
 SALDO ACUMULADO                     1,659.84                                                                                                                                                1,659.84
SALDO ANTERIOR DE DEPOSITOS          2,479.82                                                                                                                                                2,479.82
 MOVTO NETO DEPOSITOS PERIO          2,660.00-                                                                                                                                               2,660.00-
 SALDO ACUMULADO DE DEPOSIT            180.18-                                                                                                                                                 180.18-
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       22920000000  MARSH & MCLENNAN (UK)                               Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MANEJO FIN        M.O.P.                                                                                                                             TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                  71,325,334.00-      7,093,280.00                                                                                                                        64,232,054.00-
 SALDO ACUMULADO                71,325,334.00-      7,093,280.00                                                                                                                        64,232,054.00-
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                         1,931,340.40                                                                                                                         1,931,340.40
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       22950000001  ASSICURAZIONI GENERALI S.P.A.                       Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      T. R. C.                                                                                                                                             TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                     378,455.00                                                                                                                                              378,455.00
 TOTAL INGRESOS                    378,455.00                                                                                                                                              378,455.00
COMISION BASICA                     34,060.95                                                                                                                                               34,060.95
DEPOSITOS RETENIDOS                 75,691.00                                                                                                                                               75,691.00
RETENCION EN LA FUENTE/PRIM          3,784.55                                                                                                                                                3,784.55
 TOTAL EGRESOS                     113,536.50                                                                                                                                              113,536.50
MOVIMIENTOS DEL PERIODO            264,918.50                                                                                                                                              264,918.50
 SALDO ACUMULADO                   264,918.50                                                                                                                                              264,918.50
 MOVTO NETO DEPOSITOS PERIO         75,691.00                                                                                                                                               75,691.00
 SALDO ACUMULADO DE DEPOSIT         75,691.00                                                                                                                                               75,691.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23000000002  LIU - USA                                           Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CUMPLIMIEN        CUMPLIMIEN        E.ELECTRIC        TERRORISMO           PYME            R. CIVIL         TERREMOTO                                TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                  29,451,120.20      26,238,922.66-    847,701,673.00         207,787.09          34,404.64          71,732.60         830,380.42                        852,058,175.29
 SALDO ACUMULADO                29,451,120.20      26,238,922.66-    847,701,673.00         207,787.09          34,404.64          71,732.60         830,380.42                        852,058,175.29
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23000000002  LIU - USA                                           Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      TRANSPORTE                                                                                                                                           TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
 SALDO ACUMULADO
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000000  LIU - BRASIL                                        Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CUMPLIMIEN        CUMPLIMIEN        MIEMBROSJD                                                                                                       TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                  18,593,052.07-        132,647.10-        220,010.06-                                                                                                    18,945,709.23-
 SALDO ACUMULADO                18,593,052.07-        132,647.10-        220,010.06-                                                                                                    18,945,709.23-
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000000  LIU - BRASIL                                        Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CUMPLIMIEN        CUMPLIMIEN                                                                                                                         TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                                             39.61                                                                                                                                39.61
 SALDO ACUMULADO                                           39.61                                                                                                                                39.61
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000001  LIBERTY SURETY                                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CUMPLIMIEN        CUMPLIMIEN                                                                                                                         TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                  16,873,873.28-     34,120,670.34-                                                                                                                       50,994,543.62-
 SALDO ACUMULADO                16,873,873.28-     34,120,670.34-                                                                                                                       50,994,543.62-
SALDO ANTERIOR DE DEPOSITOS        456,063.00                                                                                                                                              456,063.00
 SALDO ACUMULADO DE DEPOSIT        456,063.00                                                                                                                                              456,063.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000001  LIBERTY SURETY                                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CUMPLIMIEN        CUMPLIMIEN        CUMPLIMIEN        CUMPLIMIEN        CUMPLIMIEN        CUMPLIMIEN                                                 TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                       2,945.87                                                    42.68-                                                                                      2,903.19
 SALDO ACUMULADO                     2,945.87                                                    42.68-                                                                                      2,903.19
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      ASISMOTOS         CUMPLIMIEN        CUMPLIMIEN        MIEMBROSJD        MIEMBROSJD        MIEMBROSJD        MIEMBROSJD        E.ELECTRIC       CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                                                                                                                                          250,816.30
 TOTAL INGRESOS                                                                                                                                                         250,816.30
COMISION BASICA                                                                                                                                                          47,667.00
DEPOSITOS RETENIDOS                                                                                                                                                      50,163.00
RETENCION EN LA FUENTE/PRIM                                                                                                                                               2,508.16
 TOTAL EGRESOS                                                                                                                                                          100,338.16
MOVIMIENTOS DEL PERIODO                                                                                                                                                 150,478.14
SALDO ANTERIOR                   3,884,452.91                .19-        286,572.62-      6,500,000.00-     15,600,331.00          24,693.05-            122.76- 10,770,354,766.62-
NUESTRO PAGO                                                                                                                                                        628,524,415.93
 SALDO ACUMULADO                 3,884,452.91                .19-        286,572.62-      6,500,000.00-     15,600,331.00          24,693.05-            122.76- 11,398,728,704.41-
SALDO ANTERIOR DE DEPOSITOS                                                                                                                                          21,973,720.00
 MOVTO NETO DEPOSITOS PERIO                                                                                                                                              50,163.00
 SALDO ACUMULADO DE DEPOSIT                                                                                                                                          22,023,883.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      E.ELECTRIC        E.ELECTRIC        E.ELECTRIC        E.ELECTRIC        E.ELECTRIC        LUCRO CES.        LUCRO CES.        TERRORISMO       CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                                                                                                    173,528.00                            483,678.14
DEPOSITOS LIBERADOS                                                                                                             1,429,143.00                          2,019,637.00-
 TOTAL INGRESOS                                                                                                                 1,602,671.00                          1,535,958.86-
COMISION BASICA                                                                                                                    34,706.00                             94,541.00
DEPOSITOS RETENIDOS                                                                                                                34,706.00                             96,736.00
RETENCION EN LA FUENTE/PRIM                                                                                                         1,735.28                              4,836.79
 TOTAL EGRESOS                                                                                                                     71,147.28                            196,113.79
MOVIMIENTOS DEL PERIODO                                                                                                         1,531,523.72                          1,732,072.65-
SALDO ANTERIOR                         106.80-            841.64-     81,512,558.50-            451.51-          1,286.00-      9,033,666.80-            391.84-     90,449,252.68
NUESTRO PAGO                                                                                                                   16,067,991.00                         94,174,211.85
 SALDO ACUMULADO                       106.80-            841.64-     81,512,558.50-            451.51-          1,286.00-     23,570,134.08-            391.84-      5,457,031.82-
SALDO ANTERIOR DE DEPOSITOS                                                                                                     3,500,947.00                         29,278,406.00
 MOVTO NETO DEPOSITOS PERIO                                                                                                     1,394,437.00-                         2,116,373.00
 SALDO ACUMULADO DE DEPOSIT                                                                                                     2,106,510.00                         31,394,779.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 003
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      TERRORISMO        TERRORISMO        TERRORISMO        TERRORISMO        TERRORISMO        MANEJO FIN        MANEJO G.         MANEJO G.        CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                                                                                                                     1,508,232.79
DEPOSITOS LIBERADOS
 TOTAL INGRESOS                                                                                                                                    1,508,232.79
COMISION BASICA                                                                                                                                      286,564.00
DEPOSITOS RETENIDOS                                                                                                                                  301,647.00
RETENCION EN LA FUENTE/PRIM                                                                                                                           15,082.33
 TOTAL EGRESOS                                                                                                                                       603,293.33
MOVIMIENTOS DEL PERIODO                                                                                                                              904,939.46
SALDO ANTERIOR                      51,626.01-      3,397,486.78-      8,900,575.74       2,248,978.26       9,219,134.00-      8,309,398.62       2,273,860.54       1,574,403.19
NUESTRO PAGO
 SALDO ACUMULADO                    51,626.01-      3,397,486.78-      8,900,575.74       2,248,978.26       9,219,134.00-      8,309,398.62       3,178,800.00       1,574,403.19
SALDO ANTERIOR DE DEPOSITOS                                                                                                                          301,647.00-
 MOVTO NETO DEPOSITOS PERIO                                                                                                                          301,647.00
 SALDO ACUMULADO DE DEPOSIT
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 004
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MANEJO G.         CASCO NAV.        CASCO NAV.           PYME              PYME              PYME              PYME              PYME          CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                                                            1,482,232.39
DEPOSITOS LIBERADOS                                                                       5,605,419.00-
 TOTAL INGRESOS                                                                           4,123,186.61-
COMISION BASICA                                                                             290,102.00
SINIESTROS PAGADOS                                                                       17,085,942.80
DEPOSITOS RETENIDOS                                                                         296,448.00
RETENCION EN LA FUENTE/PRIM                                                                  14,822.34
 TOTAL EGRESOS                                                                           17,687,315.14
MOVIMIENTOS DEL PERIODO                                                                  21,810,501.75-
SALDO ANTERIOR                   1,606,331.19-      1,353,633.95          24,049.11-    134,894,616.53          52,194.01-         58,876.29-     22,327,500.30       3,688,427.45
NUESTRO PAGO                                                                            303,979,981.71
SU PAGO                                                                                  23,772,598.20
 SALDO ACUMULADO                 1,606,331.19-      1,353,633.95          24,049.11-    167,123,268.73-         52,194.01-         58,876.29-     22,327,500.30       3,688,427.45
SALDO ANTERIOR DE DEPOSITOS                                                              89,479,771.00
 MOVTO NETO DEPOSITOS PERIO                                                               5,901,867.00
 SALDO ACUMULADO DE DEPOSIT                                                              95,381,638.00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                                             329,588,182.80
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 005
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                         PYME            R. CIVIL          R. CIVIL          R. CIVIL          R. CIVIL          R. CIVIL         RC                R.MAQUINAR       CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                     13,000,000.00                                                                                                        250,554.80
DEPOSITOS LIBERADOS                                 2,400,000.00
 TOTAL INGRESOS                                    15,400,000.00                                                                                                        250,554.80
COMISION BASICA                                     1,560,000.00                                                                                                         47,606.00
SINIESTROS PAGADOS                                  6,303,261.60
DEPOSITOS RETENIDOS                                 2,600,000.00                                                                                                         50,111.00
RETENCION EN LA FUENTE/PRIM                           130,000.00                                                                                                          2,505.55
 TOTAL EGRESOS                                     10,593,261.60                                                                                                        100,222.55
MOVIMIENTOS DEL PERIODO                             4,806,738.40                                                                                                        150,332.25
SALDO ANTERIOR                  12,392,186.50-     57,318,339.92          10,680.00-        298,539.08-      1,256,806.31-          9,622.94          50,000.00-     21,540,709.17
NUESTRO PAGO                                       76,997,737.35                                                                                                     43,467,036.22
SU PAGO
 SALDO ACUMULADO                12,392,186.50-     14,872,659.03-         10,680.00-        298,539.08-      1,256,806.31-          9,622.94          50,000.00-     21,775,994.80-
SALDO ANTERIOR DE DEPOSITOS                        12,969,984.00                                                                                                     20,261,363.00
 MOVTO NETO DEPOSITOS PERIO                           200,000.00                                                                                                         50,111.00
 SALDO ACUMULADO DE DEPOSIT                        13,169,984.00                                                                                                     20,311,474.00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                       572,490,496.80
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 006
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      R.MAQUINAR        R.MAQUINAR        SUSTRACCIO        SUSTRACCIO        SUSTRACCIO        SUSTRACCIO        SUSTRACCIO        TRANSPORTE       CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                                           478,787.70                                                                                     425,519.99
DEPOSITOS LIBERADOS                                                                                                                                                      85,104.00-
 TOTAL INGRESOS                                                          478,787.70                                                                                     340,415.99
COMISION BASICA                                                           90,981.00                                                                                      80,849.00
SINIESTROS PAGADOS
DEPOSITOS RETENIDOS                                                       95,758.00                                                                                      85,104.00
RETENCION EN LA FUENTE/PRIM                                                4,787.88                                                                                       4,255.20
 TOTAL EGRESOS                                                           191,526.88                                                                                     170,208.20
MOVIMIENTOS DEL PERIODO                                                  287,260.82                                                                                     170,207.79
SALDO ANTERIOR                       3,506.09-            106.68-    108,223,801.09          16,682.85-            149.53-          1,683.29-         68,432.88-     41,422,855.19-
NUESTRO PAGO                                                          91,470,463.23
SU PAGO
 SALDO ACUMULADO                     3,506.09-            106.68-     17,040,598.68          16,682.85-            149.53-          1,683.29-         68,432.88-     41,252,647.40-
SALDO ANTERIOR DE DEPOSITOS                                           40,899,860.00                                                                                      85,104.00-
 MOVTO NETO DEPOSITOS PERIO                                               95,758.00                                                                                     170,208.00
 SALDO ACUMULADO DE DEPOSIT                                           40,995,618.00                                                                                      85,104.00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 007
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      TRANSPORTE        TRANSPORTE        TERRE PYME        TERRE PYME        TERRE PYME        TERRE PYME        TERRE PYME                               TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
PRIMAS CEDIDAS                                                         2,053,592.07                                                                                                     20,106,942.18
DEPOSITOS LIBERADOS                                                   11,098,871.00-                                                                                                    14,979,888.00-
 TOTAL INGRESOS                                                        9,045,278.93-                                                                                                     5,127,054.18
COMISION BASICA                                                          404,809.00                                                                                                      2,937,825.00
SINIESTROS PAGADOS                                                                                                                                                                      23,389,204.40
DEPOSITOS RETENIDOS                                                      410,721.00                                                                                                      4,021,394.00
RETENCION EN LA FUENTE/PRIM                                               20,535.92                                                                                                        201,069.45
 TOTAL EGRESOS                                                           836,065.92                                                                                                     30,549,492.85
MOVIMIENTOS DEL PERIODO                                                9,881,344.85-                                                                                                    25,422,438.67-
SALDO ANTERIOR                     233,478.16-        407,715.18-    121,588,898.53         997,672.06-        361,102.77-        228,458.49-     23,068,355.12                     10,312,620,052.84-
NUESTRO PAGO                                                         384,569,270.09                                                                                                  1,639,251,107.38
SU PAGO                                                                                                                                                                                 23,772,598.20
 SALDO ACUMULADO                   233,478.16-        407,715.18-    272,861,716.41-        997,672.06-        361,102.77-        228,458.49-     23,068,355.12                     11,953,521,000.69-
SALDO ANTERIOR DE DEPOSITOS                                           98,688,534.00                                                                                                    316,665,834.00
 MOVTO NETO DEPOSITOS PERIO                                           11,509,592.00                                                                                                     19,001,282.00
 SALDO ACUMULADO DE DEPOSIT                                          110,198,126.00                                                                                                    335,667,116.00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                           35,450,000.00                                                                                                    937,528,679.60
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CUMPLIMIEN        CUMPLIMIEN        TERRORISMO        MANEJO FIN        MANEJO FIN           PYME            R. CIVIL          R. CIVIL        CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                                                        1,628.75                                                 1,628.75
 TOTAL INGRESOS                                                            1,628.75                                                 1,628.75
MOVIMIENTOS DEL PERIODO                                                    1,628.75                                                 1,628.75
SALDO ANTERIOR                                             13.00-         20,483.95           9,000.00                             63,329.13          23,661.24
NUESTRO PAGO                                                              18,012.00                                                59,754.28           6,150.00
 SALDO ACUMULADO                                           13.00-          4,100.70           9,000.00                              5,203.60          17,511.24
SALDO ANTERIOR DE DEPOSITOS                                               11,489.73                                                28,933.49           6,195.00
 MOVTO NETO DEPOSITOS PERIO                                                1,628.75-                                                1,628.75-
 SALDO ACUMULADO DE DEPOSIT                                                9,860.98                                                27,304.74           6,195.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000002  LSM - LIBERTY SPECIALTY MARKET                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                       R. CIVIL          R. CIVIL         TRANSPORTE        TRANSPORTE        TRANSPORTE        TERRE PYME                                                 TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                                                                                                                 1,544.01                                                 4,801.51
 TOTAL INGRESOS                                                                                                                     1,544.01                                                 4,801.51
MOVIMIENTOS DEL PERIODO                                                                                                             1,544.01                                                 4,801.51
SALDO ANTERIOR                          34.82-             34.82           8,173.89                                                45,386.03                                               170,021.24
NUESTRO PAGO                                                                                                                       40,029.60                                               123,945.88
 SALDO ACUMULADO                        34.82-             34.82           8,173.89                                                 6,900.44                                                50,876.87
SALDO ANTERIOR DE DEPOSITOS                                                                                                        34,202.32                                                80,820.54
 MOVTO NETO DEPOSITOS PERIO                                                                                                         1,544.01-                                                4,801.51-
 SALDO ACUMULADO DE DEPOSIT                                                                                                        32,658.31                                                76,019.03
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000003  LIBERTY INTERN UNDERWRIT CANAD                      Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MIEMBROSJD        MIEMBROSJD         R. CIVIL          R. CIVIL                                                                                      TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                  10,882,471.00         113,626.38-     19,828,531.00         331,850.59-                                                                                 30,265,525.03
 SALDO ACUMULADO                10,882,471.00         113,626.38-     19,828,531.00         331,850.59-                                                                                 30,265,525.03
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23020000003  LIBERTY INTERN UNDERWRIT CANAD                      Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                       R. CIVIL                                                                                                                                            TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
 SALDO ACUMULADO
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       23050000000  GLOBAL RE BROKER                                    Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CUMPLIMIEN                                                                                                                                           TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
 SALDO ACUMULADO
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       40200000000  CARPENTER MARSH FAC (JLT RE)                        Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      LUCRO CES.        TERRORISMO        TERRORISMO        MANEJO FIN        MANEJO FIN        MANEJO FIN        MANEJO G.            PYME          CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                  32,825,923.90       1,533,706.88         300,227.11   1,024,350,141.54-      7,773,743.29-      6,749,461.94-        447,834.98       1,556,693.15
 SALDO ACUMULADO                32,825,923.90       1,533,706.88         300,227.11   1,024,350,141.54-      7,773,743.29-      6,749,461.94-        447,834.98       1,556,693.15
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       40200000000  CARPENTER MARSH FAC (JLT RE)                        Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                         PYME           RC                T. R. C.          T. R. C.          T. R. C.          T. R. C.          T. R. C.          T. R. C.         CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                       6,619.69-            700.00-     19,777,898.30-      4,571,478.38-     94,073,610.75-        102,241.85      32,823,256.12-      1,706,544.34-
 SALDO ACUMULADO                     6,619.69-            700.00-     19,777,898.30-      4,571,478.38-     94,073,610.75-        102,241.85      32,823,256.12-      1,706,544.34-
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                          921,596,936.35
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 003
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       40200000000  CARPENTER MARSH FAC (JLT RE)                        Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      TRANSPORTE        TERRE PYME        TERRE PYME                                                                                                       TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                          59.40-     16,856,059.33-        300,227.11                                                                                                  1,171,622,718.10-
 SALDO ACUMULADO                        59.40-     16,856,059.33-        300,227.11                                                                                                  1,171,622,718.10-
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                                                                                                                                            921,596,936.35
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       40200000000  CARPENTER MARSH FAC (JLT RE)                        Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      RC                RC                RC                TRANSPORTE        TRANSPORTE        TRANSPORTE        TRANSPORTE                               TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                                                                                  519.92                                                   460.52-                                59.40
 SALDO ACUMULADO                                                                                519.92                                                   460.52-                                59.40
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       40300000000  REASESORES                                          Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                       R. CIVIL          R. CIVIL          R. CIVIL          R. CIVIL                                                                                      TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                   6,725,222.20-        242,163.20-         11,184.10-         17,742.29-                                                                                  6,996,311.79-
 SALDO ACUMULADO                 6,725,222.20-        242,163.20-         11,184.10-         17,742.29-                                                                                  6,996,311.79-
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE    302,062,132.30                                                                                                                                          302,062,132.30
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       40300000000  REASESORES                                          Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MANEJO FIN         R. CIVIL                                                                                                                          TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                 12,950.00                                                                                                                                               12,950.00
 TOTAL INGRESOS                     12,950.00                                                                                                                                               12,950.00
MOVIMIENTOS DEL PERIODO             12,950.00                                                                                                                                               12,950.00
 SALDO ACUMULADO                    12,950.00                                                                                                                                               12,950.00
SALDO ANTERIOR DE DEPOSITOS          6,023.60                                                                                                                                                6,023.60
 MOVTO NETO DEPOSITOS PERIO         12,950.00-                                                                                                                                              12,950.00-
 SALDO ACUMULADO DE DEPOSIT          6,926.40-                                                                                                                                               6,926.40-
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       51400000000  GUY CARPENTER & CO                                  Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MANEJO FIN        MANEJO FIN         R. CIVIL         CYBER             CYBER             RC                RC                RC               CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                   5,713,398.44       2,415,000.09-      2,166,598.96-      1,470,000.00-        590,000.00-      4,567,102.56       2,478,500.00-         21,397.26
 SALDO ACUMULADO                 5,713,398.44       2,415,000.09-      2,166,598.96-      1,470,000.00-        590,000.00-      4,567,102.56       2,478,500.00-         21,397.26
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       51400000000  GUY CARPENTER & CO                                  Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      INC CORP                                                                                                                                             TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
RETENCION EN LA FUENTE/PRIM         13,792.69-                                                                                                                                              13,792.69-
 TOTAL EGRESOS                      13,792.69-                                                                                                                                              13,792.69-
MOVIMIENTOS DEL PERIODO             13,792.69                                                                                                                                               13,792.69
SALDO ANTERIOR                  48,245,809.63                                                                                                                                           49,427,608.84
 SALDO ACUMULADO                48,259,602.32                                                                                                                                           49,441,401.53
SALDO ANTERIOR DE DEPOSITOS     12,214,129.03                                                                                                                                           12,214,129.03
 SALDO ACUMULADO DE DEPOSIT     12,214,129.03                                                                                                                                           12,214,129.03
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       51400000000  GUY CARPENTER & CO                                  Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MIEMBROSJD        MIEMBROSJD        MIEMBROSJD        LUCRO CES.        LUCRO CES.        LUCRO CES.        LUCRO CES.        TERRORISMO       CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                                                                                    4.58                                                                        1.28
 SALDO ACUMULADO                                                                                  4.58                                                                        1.28
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       51400000000  GUY CARPENTER & CO                                  Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      TERRORISMO        TERRORISMO        MANEJO FIN        MANEJO FIN           PYME              PYME              PYME              PYME          CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                                             14.27-                                                    4.56
 SALDO ACUMULADO                                           14.27-                                                    4.56
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 003
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       51400000000  GUY CARPENTER & CO                                  Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                       R. CIVIL          R. CIVIL         R.MAQUINAR        TRANSPORTE        TRANSPORTE        TERRE PYME        TERRE PYME        TERRE PYME       CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                                                                                                                          5.85
 SALDO ACUMULADO                                                                                                                        5.85
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 004
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       51400000000  GUY CARPENTER & CO                                  Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      TERRE PYME                                                                                                                                           TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                                                                                                                                                                                   2.00
 SALDO ACUMULADO                                                                                                                                                                                 2.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       56700000000  WILLIS RE MIAMI                                     Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      RC                                                                                                                                                   TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                     612,000.00-                                                                                                                                             612,000.00-
 SALDO ACUMULADO                   612,000.00-                                                                                                                                             612,000.00-
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       56700000001  WILLIS RE COLOMBIA                                  Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      RC                RC                                                                                                                                 TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                     611,663.75             335.78                                                                                                                           611,999.53
 SALDO ACUMULADO                   611,663.75             335.78                                                                                                                           611,999.53
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       56700000001  WILLIS RE COLOMBIA                                  Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                       R. CIVIL          R. CIVIL          R. CIVIL                                                                                                        TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                            .01-                                                                                                                                                    .01-
 SALDO ACUMULADO                          .01-                                                                                                                                                    .01-
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       57100000000  AON RE                                              Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MIEMBROSJD        MIEMBROSJD        MIEMBROSJD        MIEMBROSJD        MANEJO FIN        MANEJO FIN        MANEJO FIN        MANEJO G.        CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                                                                                          2,081,250.00-
 TOTAL INGRESOS                                                                                              2,081,250.00-
MOVIMIENTOS DEL PERIODO                                                                                      2,081,250.00-
SALDO ANTERIOR                 491,634,129.33-     22,725,000.00-      2,348,740.00-    539,409,804.98     788,194,202.31-        254,047.75-    459,069,424.30         117,461.55-
 SALDO ACUMULADO               491,634,129.33-     22,725,000.00-      2,348,740.00-    539,409,804.98     790,275,452.31-        254,047.75-    459,069,424.30         117,461.55-
SALDO ANTERIOR DE DEPOSITOS                                                                                  2,081,250.00-
 MOVTO NETO DEPOSITOS PERIO                                                                                  2,081,250.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       57100000000  AON RE                                              Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      CASCO NAV.        CASCO NAV.         R. CIVIL          R. CIVIL          R. CIVIL          R. CIVIL         RC                RC               CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                                                                                                                                3,598,490.00-
 TOTAL INGRESOS                                                                                                                                    3,598,490.00-
MOVIMIENTOS DEL PERIODO                                                                                                                            3,598,490.00-
SALDO ANTERIOR                   3,661,174.17       1,312,384.29-    161,202,477.60-      1,394,240.69-        391,440.00-  2,198,600,124.84-      4,741,476.28       1,142,364.71-
 SALDO ACUMULADO                 3,661,174.17       1,312,384.29-    161,202,477.60-      1,394,240.69-        391,440.00-  2,198,600,124.84-      1,142,986.28       1,142,364.71-
SALDO ANTERIOR DE DEPOSITOS                                                                                                                        3,598,490.00-
 MOVTO NETO DEPOSITOS PERIO                                                                                                                        3,598,490.00
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 003
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       57100000000  AON RE                                              Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      T. R. C.          T. R. C.          T. R. C.          M.O.P.            M.O.P.                                                                       TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
DEPOSITOS LIBERADOS                                                                                                                                                                      5,679,740.00-
 TOTAL INGRESOS                                                                                                                                                                          5,679,740.00-
MOVIMIENTOS DEL PERIODO                                                                                                                                                                  5,679,740.00-
SALDO ANTERIOR                 773,381,592.44-     38,246,437.44-    806,507,819.55     732,669,990.55-    585,076,421.50                                                            2,815,148,512.72-
 SALDO ACUMULADO               773,381,592.44-     38,246,437.44-    806,507,819.55     732,669,990.55-    585,076,421.50                                                            2,820,828,252.72-
SALDO ANTERIOR DE DEPOSITOS                                                                                                                                                              5,679,740.00-
 MOVTO NETO DEPOSITOS PERIO                                                                                                                                                              5,679,740.00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                                             295,781,364.55                                                                                 295,781,364.55
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       57100000000  AON RE                                              Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      RESP.CIVIL        MIEMBROSJD        MIEMBROSJD        MIEMBROSJD        MIEMBROSJD        MANEJO FIN        MANEJO FIN        MANEJO FIN       CONTINUA...
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                                        171,555.47          26,957.64-          5,945.37-          1,380.39-         15,410.76          17,352.21-             11.81-
NUESTRO PAGO                                          148,069.49
 SALDO ACUMULADO                                       23,485.98          26,957.64-          5,945.37-          1,380.39-         15,410.76          17,352.21-             11.81-
SALDO ANTERIOR DE DEPOSITOS                            73,585.40
 SALDO ACUMULADO DE DEPOSIT                            73,585.40
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                           128,561.52
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 002
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       57100000000  AON RE                                              Periodo..: 2026-06                                                    Moneda..: DOLLAR
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MANEJO FIN         R. CIVIL          R. CIVIL          R. CIVIL         RCP MEDICA        RCP MEDICA        TRANSPORTE                               TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                         183.14                                                                    6,844.00-          2,242.00-                                              126,415.95
NUESTRO PAGO                                                                                                                                                                               148,069.49
 SALDO ACUMULADO                       183.14                                                                    6,844.00-          2,242.00-                                               21,653.54-
SALDO ANTERIOR DE DEPOSITOS                                                                                                                                                                 73,585.40
 SALDO ACUMULADO DE DEPOSIT                                                                                                                                                                 73,585.40
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
RESERVA SINIESTROS PARTE RE                                                                                                                                                                128,561.52
                                                                                     HDI SEGUROS COLOMBIA SA                                                                  Fecha.: 2026/07/22
                                                                         GERENCIA  DE  REASEGUROS  Y  RIESGOS  PATRIMONIALES                                                  Hoja No.: 001
                                                                            REASEGURO  CEDIDO  -  CONTRATOS FACULTATIVOS
 Corredor:       86050580060  AP CORREDORES INTERNACIONALES                       Periodo..: 2026-06                                                    Moneda..: PESO COLOMBIANO
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
       R A M O S                      MANEJO G.                                                                                                                                            TOTAL
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 PARTICIPACION                                 %                 %                 %                 %                 %                 %                 %                 %                 %
SALDO ANTERIOR                  19,017,059.11                                                                                                                                           19,017,059.11
 SALDO ACUMULADO                19,017,059.11                                                                                                                                           19,017,059.11



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
























