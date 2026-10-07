# Entrega 2 - Datos y preparación

Proyecto seleccionado: **MarketPulse: detector de anomalías y oportunidades tempranas en acciones**. El MVP prioriza activos con comportamientos inusuales y explica sus señales estadísticas. Las alertas se calcularán al cierre de la sesión; esta entrega prepara los datos y no entrena modelos ni genera recomendaciones de compra o venta.

## 1. Qué datos necesita vuestro producto

Una observación representa un activo en una sesión bursátil diaria. Son imprescindibles ticker, fecha, apertura, máximo, mínimo, cierre, cierre ajustado y volumen. De ellos se derivan rentabilidad, rango diario, volumen relativo, volatilidad y distancia a extremos recientes. El cierre ajustado permite comparar rentabilidades evitando saltos debidos a splits y dividendos.

Son deseables las noticias, su sentimiento, sector y calendario de resultados; se aplazan para mantener un MVP pequeño. Se utilizarán AAPL, MSFT, NVDA, AMZN, META y GOOGL, con SPY y QQQ como contexto de mercado futuro. Todos cotizan en USD en mercados estadounidenses; el volumen se interpreta como unidades negociadas del activo.

Se descarga el histórico diario entre 2022-01-01 (inclusive) y 2025-01-01 (exclusive), tres años naturales. Las ventanas usan 20 observaciones anteriores por activo. Los primeros 21 registros válidos carecen del histórico suficiente para todas las variables y se excluyen de Gold. No se crean filas de fines de semana ni se rellenan sesiones ausentes con precios ficticios.

## 2. Fuentes reales y viabilidad

La fuente es **Yahoo Finance**, consultada mediante la biblioteca no oficial **yfinance**. El acceso del MVP no requiere clave de API; el mecanismo concreto es `yf.download` por ticker con `interval="1d"`, `auto_adjust=False` y fechas fijas. Se conservan tanto cierre como cierre ajustado. Instrucciones completas en [data/README.md](../../data/README.md) y adquisición en [el notebook](../../notebooks/02_marketpulse_datos_y_preparacion.ipynb).

- Cobertura: las seis acciones líquidas y los dos ETF citados, con histórico diario suficiente para el periodo elegido; el notebook exige obtener todos los activos y no acepta resultados parciales silenciosos.
- Actualización: podría ejecutarse después del cierre de cada sesión. En esta entrega se conserva un periodo fijo, no se implementa un servicio en tiempo real.
- Estabilidad: no hay garantía contractual de disponibilidad o fidelidad; pueden existir límites de consultas, errores y revisiones retrospectivas de los ajustes. Cada adquisición conserva fecha UTC, parámetros, versiones y huellas SHA-256; la repetición desde Bronze evita depender de otra descarga.
- Alternativa: Alpha Vantage, mediante API con clave y un endpoint diario ajustado, sujeto al plan y límites vigentes. Sus datos deberían convertirse al esquema Bronze equivalente, revisar licencia y unidades, y registrar su procedencia antes de mezclarlos. El pipeline ya admite reproducir una adquisición existente sin conexión.

Referencias: [documentación de descarga de yfinance](https://ranaroussi.github.io/yfinance/reference/api/yfinance.download.html), [proyecto y condiciones de uso](https://pypi.org/project/yfinance/), [API alternativa](https://www.alphavantage.co/documentation/).

## 3. Uso, privacidad y datos personales

Los datos son cotizaciones y volúmenes agregados por activo y fecha; no se necesitan nombres, cuentas, posiciones ni operaciones de personas. No se recogen noticias ni publicaciones de usuarios en esta fase. Se limita la adquisición a ocho activos y al periodo definido; no se guardan credenciales.

La licencia Apache 2.0 de la biblioteca yfinance no otorga una licencia sobre los datos de Yahoo. El proyecto yfinance indica que Yahoo Finance está destinado a uso personal y remite a las condiciones del proveedor. El uso académico no implica permiso automático de redistribución o explotación comercial: antes de esos usos se deberán revisar los términos vigentes y obtener las autorizaciones necesarias. Referencia: [aviso del proveedor de la biblioteca](https://pypi.org/project/yfinance/).

Por minimización y condiciones de uso, el repositorio contiene instrucciones reproducibles de acceso en lugar de publicar cotizaciones masivas. Bronze, Silver y Gold se generan localmente y se excluyen de Git. Si después se añade texto de redes, se reconsiderarán la necesidad de datos personales, los permisos de la plataforma y el uso de agregados sin identificadores.

## 4. Del dato bruto al dato utilizable

`Yahoo Finance -> Bronze/Raw -> Silver -> Gold`

### Bronze / Raw

El notebook guarda `data/bronze/<TICKER>.csv` con la tabla diaria recibida, sin limpiar, imputar ni calcular variables. Serializa el índice de sesión como `Date` y conserva los valores y columnas de la respuesta de yfinance, incluidos los nulos. La capa conserva la respuesta de la biblioteca, no la respuesta HTTP original de Yahoo. `manifest.json` registra fuente, instante de adquisición UTC, símbolos, fechas, parámetros, versiones, número de filas y hash por CSV. No se sobrescribe un Bronze existente: se reutiliza o se elige otro directorio de datos.

### Silver

`data/silver/marketpulse.csv` identifica cada fila por `(symbol, date)`. Normaliza nombres y tickers, convierte fechas y números, ordena cronológicamente por activo y elimina duplicados exactos. Si dos filas distintas tienen la misma clave, se detiene para no escoger arbitrariamente una cotización.

Se descartan filas con fecha o ticker ausente, valores no finitos, precios nulos o no positivos, volumen nulo, negativo o fraccionario y OHLC incoherente (máximo inferior a apertura/cierre/mínimo o mínimo superior a ellos). Se permite volumen cero y se evita dividir por una media de volumen cero. No se imputa ni se normaliza usando todo el histórico. El informe de calidad cuenta los descartes; las sesiones que falten deben revisarse antes de entrenar, porque una rentabilidad entre observaciones separadas puede abarcar varias sesiones.

Se conserva el cierre del proveedor y se calcula `daily_return` sobre cierre ajustado. Para comparar extremos con ese cierre, máximo y mínimo diarios se multiplican por `adj_close / close`. Las medias y extremos móviles terminan en t-1; incluyen exclusivamente las 20 observaciones previas del mismo activo. Las características de t se conocen al cierre de t. La volatilidad es la desviación típica muestral de las rentabilidades previas, sin anualizar.

### Gold

`data/gold/marketpulse.csv` contiene una fila por activo y sesión con todas las variables válidas. Elimina el calentamiento inicial y otras filas con variables indefinidas, sin rellenarlas con cero. Los datos se utilizarán en la siguiente fase para comparar baselines y métodos de detección de anomalías. No incluye objetivos futuros, puntuaciones aprendidas ni etiquetas de anomalía inventadas.

| Columna | Significado y uso posterior |
|---|---|
| `date`, `symbol` | Sesión y ticker; clave única, orden temporal y agrupación |
| `close`, `adj_close` | Cierre del proveedor y cierre ajustado, en USD |
| `volume` | Unidades negociadas; actividad de la sesión |
| `daily_return` | `adj_close_t / adj_close_anterior - 1`; movimiento de precio |
| `intraday_range_pct` | `(high - low) / close`; amplitud relativa de la sesión |
| `volume_ma_20` | Media de volumen de las 20 observaciones anteriores |
| `relative_volume` | Volumen actual / media anterior; actividad inusual |
| `volatility_20` | Desviación típica muestral de 20 rentabilidades anteriores |
| `rolling_high_20`, `rolling_low_20` | Extremos ajustados de las 20 observaciones anteriores |
| `distance_to_high_20`, `distance_to_low_20` | `adj_close / extremo_anterior - 1`; proximidad o ruptura del rango |

Rentabilidades, rangos, distancias y volatilidad son fracciones: 0.02 equivale al 2 %. El volumen relativo es un múltiplo: 2 equivale a dos veces la media. No se anualiza ninguna variable. `quality_report.json` informa filas por capa, descartes, cobertura por ticker y hashes del Gold, del manifiesto Bronze y del notebook.

Para reproducir: instalar `requirements.txt`, abrir `notebooks/02_marketpulse_datos_y_preparacion.ipynb`, seleccionar el Python de `.venv` y ejecutar todas las celdas en orden. Si existe Bronze, el notebook verifica las huellas del snapshot y reconstruye Silver y Gold sin red; de lo contrario descarga los datos. La última celda comprueba que el replay produce el mismo Gold. Para otra adquisición, configurar un directorio `DATA_DIR` nuevo. La reproducción exacta requiere mantener también las versiones del entorno; otra descarga del mismo periodo puede variar por revisiones del proveedor.

## 5. Riesgos y limitaciones

Faltan noticias y eventos que expliquen la causa de una anomalía; el precio y volumen solo permiten describir la señal.
La selección de grandes empresas y ETF estadounidenses introduce sesgo de selección y supervivencia y no representa todo el mercado.
Los datos diarios no permiten detectar movimientos intradía y los ajustes retrospectivos no garantizan una evaluación histórica punto a punto.
Si Yahoo dejara de estar disponible, se reutilizaría el snapshot Bronze y se adaptaría una fuente diaria ajustada alternativa tras revisar cobertura y condiciones.
