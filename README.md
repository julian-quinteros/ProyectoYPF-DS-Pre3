# ProyectoYPF-DS-Pre3
## Grupo 14 - Proyecto DS

Miembros:

 - Martínez, Alam / Ingeniero de Petróleos / martinezalam19@gmail.com
 - Quinteros, Julián Ezequiel / Ingeniero de Petróleos / julian15quinteros@gmail.com
# Venteo y quema de gas: factores asociados a la pérdida frente a la venta

## Pregunta de investigación

¿Qué factores (estado, tipo de tierra, estación del año, región offshore y período) están asociados con una mayor proporción o probabilidad de gas venteado o quemado, frente a gas vendido?

	⁠El análisis busca *asociaciones* en datos observacionales. No se afirma causalidad.

## Objetivo

Desarrollar un proyecto de Machine Learning reproducible que:

1.⁠ ⁠Caracterice la disposición del gas producido (venta, venteo y quema) según factores geográficos, temporales y regulatorios.
2.⁠ ⁠Evalúe qué variables aportan información relevante para distinguir o estimar la pérdida de gas.
3.⁠ ⁠Compare modelos de referencia (línea base, modelos interpretables y modelos no lineales) mediante validación adecuada.
4.⁠ ⁠Interprete los resultados y explicite las limitaciones del análisis.

## Dataset

*Archivo:* ⁠ OGORBcsv.csv ⁠
*Fuente:* [completar: por ejemplo, ONRR, Oil and Gas Operations Report, Revenue Based (OGORB), U.S. Department of the Interior. Verificar la fuente y la licencia antes de publicar.]
*Granularidad:* mensual, con registros por fecha de producción, ubicación, tipo de hidrocarburo y destino.
*Cobertura temporal:* enero de 2015 a mayo de 2025.
*Dimensiones originales:* 470.830 filas × 11 columnas.

### Columnas (nombres originales)

| Columna | Descripción |
|---|---|
| ⁠ Production Date ⁠ | Mes de producción (formato MM/DD/YYYY, día siempre 01). |
| ⁠ Land Class ⁠ | Clase de tierra (por ejemplo, federal, tribal). |
| ⁠ Land Category ⁠ | Categoría de tierra (onshore u offshore). |
| ⁠ State ⁠ | Estado de EE. UU. Vacío para registros offshore. |
| ⁠ County ⁠ | Condado. |
| ⁠ FIPS Code ⁠ | Código FIPS del condado. |
| ⁠ Offshore Region ⁠ | Región offshore (Alaska, Golfo, Pacífico). |
| ⁠ Commodity ⁠ | Tipo de hidrocarburo y unidad (⁠ Gas (Mcf) ⁠ u ⁠ Oil (bbl) ⁠). |
| ⁠ Disposition Code ⁠ | Código numérico del destino del volumen. |
| ⁠ Disposition Description ⁠ | Descripción textual del destino. |
| ⁠ Volume ⁠ | Volumen reportado. Viene como texto con separadores de miles y puede tener valores negativos. |

## Preparación de datos (resumen)

•⁠  ⁠*Unidades:* el análisis se realiza solo con gas (Mcf). No se suman volúmenes de gas y petróleo.
•⁠  ⁠*Volumen:* se convierte a numérico quitando separadores de miles. Los valores negativos (reversiones) se truncan a cero solo para el cálculo de proporciones.
•⁠  ⁠*Fechas:* se convierten a ⁠ datetime ⁠ con formato explícito. Se derivan año, mes y estación.
•⁠  ⁠*Destinos:* se clasifican en
  - Venta: códigos 1, 4, 5, 6, 7, 9, 15, 43.
  - Venteo: códigos 61, 62, 63, 68, 69.
  - Quema: códigos 21, 22, 33, 66, 67.
  - Otros destinos (transferencias, inyección, uso en el lugar, ajustes, etc.): excluidos del análisis, porque no son venta ni pérdida.
•⁠  ⁠*Faltantes:* se imputan según la lógica documentada en el notebook. Los faltantes de ⁠ Offshore Region ⁠ en registros onshore se etiquetan como ⁠ onshore ⁠. Los de ⁠ State ⁠, ⁠ County ⁠ y ⁠ FIPS Code ⁠ se completan con ⁠ Offshore ⁠ o ⁠ desconocido ⁠, según ⁠ Land Category ⁠.
•⁠  ⁠*Resultado:* 68.964 registros de gas en el análisis, sin duplicados exactos.
## Limitaciones

•⁠  ⁠Los datos son observacionales: las asociaciones no implican causalidad.
•⁠  ⁠La clasificación de los códigos de disposición depende de la documentación de la fuente y debe verificarse.
•⁠  ⁠La unidad de análisis y la forma de agregar volúmenes condicionan las proporciones calculadas.
•⁠  ⁠Algunos registros tienen ubicación incompleta o volúmenes negativos, lo que puede afectar las estimaciones.
