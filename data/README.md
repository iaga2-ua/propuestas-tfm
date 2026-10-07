# Datos de MarketPulse

Referencia y mecanismo reproducible de acceso a datos reales para la Entrega 2. El código se entrega únicamente en [el notebook](../notebooks/02_marketpulse_datos_y_preparacion.ipynb), sin scripts externos. No se distribuyen datasets grandes ni datos personales.

Fuente: Yahoo Finance mediante [yfinance](https://ranaroussi.github.io/yfinance/reference/api/yfinance.download.html). La biblioteca tiene licencia Apache 2.0; los datos están sujetos a las condiciones de Yahoo y no heredan esa licencia. Véase el [aviso de uso personal](https://pypi.org/project/yfinance/).

## Preparar el entorno

Desde la raíz del repositorio, con Python 3.11 o superior, en PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

Abre `notebooks/02_marketpulse_datos_y_preparacion.ipynb` en VS Code u otro editor compatible con Jupyter, selecciona el intérprete `.venv/Scripts/python.exe` como kernel y ejecuta todas las celdas en orden. El notebook incluye configuración, adquisición, funciones de limpieza, construcción de variables, generación de Gold, vistas de resultados y comprobación de reproducción.

La configuración inicial descarga AAPL, MSFT, NVDA, AMZN, META, GOOGL, SPY y QQQ entre 2022-01-01 (inclusive) y 2025-01-01 (exclusive), con frecuencia diaria. Se necesita Internet para la primera adquisición; no se requiere clave. Si un ticker no aporta datos, el proceso se detiene y no publica un Gold parcial.

## Archivos generados localmente

- `bronze/<TICKER>.csv`: tabla del proveedor sin limpieza, índice de sesión serializado como `Date`.
- `bronze/manifest.json`: origen, parámetros, fecha UTC, versiones, recuentos y SHA-256 de cada CSV.
- `silver/marketpulse.csv`: filas válidas, sin duplicados, y variables por activo.
- `gold/marketpulse.csv`: datos finales sin nulos ni infinitos en las variables requeridas.
- `gold/quality_report.json`: recuentos, descartes, cobertura, versiones y huellas de los artefactos.

Estas carpetas se excluyen de Git. El notebook conserva vistas pequeñas de las tablas y resultados de la verificación. Cada fila Gold representa un ticker en una sesión. El diccionario y las reglas de limpieza están en [la Entrega 2](../docs/entregas/02_datos_y_preparacion.md).

## Repetir sin red

Vuelve a ejecutar todas las celdas con la misma configuración. Si hay un manifiesto Bronze, se verifican su configuración y hashes y se utiliza el snapshot guardado. La última celda procesa nuevamente Bronze sin red y exige igualdad del Gold y de su SHA-256. Conserva las mismas versiones de Python y dependencias para reproducir exactamente.

Bronze nunca se sobrescribe automáticamente. Para otro periodo o grupo de tickers, cambia `START`, `END`, `SYMBOLS` y asigna un `DATA_DIR` nuevo, por ejemplo `ROOT / 'work/datos_2023'`. No cambies parámetros al reutilizar un snapshot existente.

Las ventanas usan 20 observaciones anteriores y la volatilidad necesita además la primera rentabilidad: se eliminan al menos 21 filas iniciales por activo. Solicita suficientes sesiones. No se rellenan huecos: revisa el informe y la cobertura antes de utilizar los datos para ML. No se entrena ningún modelo.
