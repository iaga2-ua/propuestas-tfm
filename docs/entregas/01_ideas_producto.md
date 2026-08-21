# Entrega 1 — Propuesta inicial de ideas de producto

## Introducción

En esta primera entrega se presentan tres ideas iniciales de proyecto de Data Science / IA. El objetivo no es seleccionar todavía una idea definitiva ni definir una solución técnica completa, sino identificar problemas reales que puedan abordarse mediante datos, analítica, inteligencia artificial o visualización.

Las tres propuestas están orientadas a mejorar procesos de decisión en contextos donde existe incertidumbre, exceso de información o dificultad para interpretar datos de forma objetiva. En cada caso se explica el problema que se pretende resolver, la motivación para desarrollar la idea, el colectivo impactado y el valor potencial que podría aportar una solución basada en datos.

---

## Idea 1 — AlphaSense: sistema de apoyo a decisiones de inversión basado en mercado y sentimiento

### Problema que resuelve

Actualmente, muchos inversores particulares toman decisiones de inversión utilizando información dispersa y difícil de interpretar: precios históricos, noticias financieras, opiniones en redes sociales, comunicados de empresas, recomendaciones de analistas o comentarios en foros. Esta información suele llegar de forma desordenada, con mucho ruido y sin una metodología clara para transformarla en decisiones objetivas.

Esto puede provocar decisiones impulsivas, entradas tardías, ventas precipitadas o falta de control sobre el riesgo. Además, una persona no puede revisar continuamente todas las noticias, movimientos de precio, cambios de volumen o variaciones de sentimiento relacionadas con varios activos financieros.

La decisión que podría mejorar con datos es la identificación de posibles oportunidades de inversión, la evaluación del riesgo de cada operación y la decisión de cuándo sería preferible no actuar. No se trata simplemente de predecir precios, sino de abordar la dificultad real de tomar decisiones financieras razonadas en un entorno con exceso de información e incertidumbre. Una solución basada en datos podría ayudar a estructurar esa información y transformarla en señales más comprensibles para apoyar la toma de decisiones.

### Motivación para realizar el proyecto

La motivación principal es económica y profesional. Un sistema que ayude a interpretar mejor la información financiera y a reducir decisiones impulsivas puede aportar valor a inversores particulares o a personas interesadas en gestionar mejor sus inversiones.

Desde el punto de vista técnico, permite aplicar contenidos relevantes del máster: análisis de datos financieros, series temporales, procesamiento de lenguaje natural, clasificación, evaluación de modelos y visualización de resultados. También tiene una motivación personal, al permitir desarrollar una solución con utilidad práctica y no solo un análisis académico.

Es razonable pensar que existen datos para trabajar la idea, como precios históricos, volumen de negociación, noticias financieras, comunicados de empresas e información textual pública relacionada con activos financieros. Incluso si se concluyera que el sentimiento de noticias o redes no mejora las decisiones, el resultado aportaría evidencia sobre qué señales tienen valor y cuáles no.

### A quién impacta

El proyecto impactaría principalmente a inversores particulares que quieren tomar decisiones más informadas y menos impulsivas. También podría resultar útil para estudiantes de finanzas, pequeños *traders*, analistas en formación o personas interesadas en validar estrategias de inversión de forma objetiva.

El usuario real no sería todo el mundo, sino personas que ya invierten o están interesadas en invertir y que necesitan una herramienta para filtrar información, detectar señales relevantes y entender mejor el riesgo de sus decisiones. No estaría planteado inicialmente para gestionar dinero de terceros ni para sustituir a un asesor financiero profesional, sino como una herramienta de análisis y apoyo a la decisión.

### Por qué tiene valor

El valor del proyecto está en transformar información dispersa en indicadores más claros y útiles. Puede ayudar a ahorrar tiempo, reducir el ruido informativo, detectar riesgos y evitar operaciones basadas únicamente en intuición o emociones.

También puede aportar transparencia al mostrar por qué una señal parece relevante: por ejemplo, si se debe a un aumento de volumen, una noticia importante, un cambio de sentimiento o una combinación de varios factores. Además, permitiría evaluar objetivamente si las señales textuales añaden valor frente a utilizar únicamente datos de mercado.

---

## Idea 2 — MarketPulse: detector de anomalías y oportunidades tempranas en acciones

### Problema que resuelve

En los mercados financieros existen situaciones en las que una acción empieza a comportarse de forma inusual antes de un movimiento relevante. Por ejemplo, puede aumentar repentinamente el volumen de negociación, crecer el número de menciones en redes, aparecer noticias importantes, cambiar el sentimiento del mercado o producirse una ruptura técnica en el precio.

Detectar estas situaciones manualmente es difícil, especialmente cuando se quieren monitorizar muchas empresas al mismo tiempo. Muchos inversores particulares se enteran de estos movimientos demasiado tarde, cuando la noticia ya se ha difundido ampliamente o cuando el precio ya ha subido o bajado de forma significativa.

La decisión que podría mejorar con datos es la detección temprana de activos que merecen atención. En lugar de revisar manualmente cientos de gráficos, noticias y fuentes de información, el sistema podría señalar qué acciones presentan comportamientos anómalos y por qué. No es simplemente un ejercicio técnico de detección de anomalías: responde al caso de uso real de priorizar la atención en un entorno con demasiados activos e información para analizar manualmente.

### Motivación para realizar el proyecto

La motivación económica es relevante, ya que detectar antes ciertos movimientos o riesgos podría ayudar a tomar decisiones de inversión mejor informadas. Sin embargo, la meta no se limita a intentar obtener rentabilidad, sino a construir una herramienta que ayude a interpretar qué está ocurriendo en el mercado.

Desde el punto de vista profesional y técnico, el proyecto permite aplicar análisis de series temporales, detección de anomalías, clasificación, procesamiento de texto, creación de indicadores y visualización de alertas. La idea está además bien delimitada: en vez de anticipar cada movimiento de precio, se busca identificar un subconjunto pequeño de situaciones donde existen señales inusuales que justifican un análisis más profundo.

Existen potencialmente datos para desarrollar la idea, como precios históricos, volumen, volatilidad, noticias, menciones sociales y eventos relevantes de empresas.

### A quién impacta

El proyecto impactaría a inversores particulares, pequeños *traders*, analistas financieros en formación y personas que necesitan monitorizar muchos activos de forma eficiente.

También podría ser útil para usuarios que no buscan una recomendación automática de compra o venta, sino una alerta que indique dónde está ocurriendo algo relevante. Por ejemplo, una persona que sigue acciones tecnológicas podría utilizarlo para identificar cuáles presentan cambios anómalos de volumen, sentimiento o comportamiento de precio. El colectivo beneficiado sería cualquier persona o pequeño equipo que tenga que revisar muchas oportunidades de mercado con recursos limitados.

### Por qué tiene valor

El principal valor del proyecto es el ahorro de tiempo y la detección temprana de situaciones relevantes. En lugar de analizar manualmente grandes cantidades de información, el usuario podría concentrarse en los activos que presentan señales anómalas.

También aporta valor al detectar riesgos: una anomalía no tiene por qué ser una oportunidad positiva; puede indicar incertidumbre, una noticia negativa, aumento de volatilidad o deterioro del sentimiento. Por último, ayudaría a priorizar qué activos revisar y qué señales estudiar con más detalle, generando conocimiento sobre qué combinaciones de señales suelen preceder movimientos importantes y cuáles no.

---

## Idea 3 — SmartPortfolio: optimizador de carteras personales con control de riesgo

### Problema que resuelve

Muchas personas que invierten construyen sus carteras de forma poco estructurada. Pueden comprar acciones, fondos o ETF de manera aislada, sin analizar correctamente la relación entre activos, la exposición a sectores concretos, la volatilidad global o el riesgo real de la cartera.

El problema no siempre es elegir mal un activo concreto, sino no gestionar bien el conjunto. Una persona puede pensar que está diversificada porque tiene muchas posiciones, cuando en realidad todas dependen de factores similares, como el mismo sector, la misma divisa o el mismo mercado.

La decisión que podría mejorar con datos es la asignación de capital: cuánto peso debería tener cada activo, cuándo conviene rebalancear, cómo reducir concentración y cómo comparar una cartera frente a una alternativa más simple, como un índice o una cartera diversificada. No es solo un ejercicio técnico de optimización, sino una respuesta a un problema real de planificación financiera: muchas personas invierten sin comprender el riesgo global de sus decisiones.

### Motivación para realizar el proyecto

La motivación principal es ayudar a tomar mejores decisiones de inversión desde una perspectiva de riesgo y planificación. A diferencia de un sistema centrado en operaciones de corto plazo, esta idea busca mejorar la gestión de una cartera a medio o largo plazo.

Desde el punto de vista técnico, permite aplicar análisis exploratorio, modelado de riesgo, optimización, simulación, visualización de datos y evaluación de estrategias. Tiene relevancia económica y personal porque muchas personas invierten sus ahorros sin herramientas claras para entender si su cartera está equilibrada. Una solución así podría ayudar a identificar concentraciones excesivas, riesgos ocultos o decisiones de rebalanceo razonables.

Es viable pensar que existen datos para trabajar la idea, como precios históricos de acciones o ETF, índices de mercado, información sectorial, volatilidad y correlaciones entre activos.

### A quién impacta

El proyecto impactaría principalmente a inversores particulares que gestionan sus propios ahorros y quieren entender mejor el riesgo de su cartera. También podría resultar útil para estudiantes de finanzas, asesores financieros en formación o personas que invierten en ETF y quieren comparar distintas asignaciones.

El usuario concreto sería alguien que ya tiene una cartera o quiere construir una y necesita apoyo para responder preguntas como si está suficientemente diversificada, qué activos concentran más riesgo, cómo se comportaría la cartera ante distintos escenarios o cuándo tendría sentido rebalancear. No estaría dirigido a grandes entidades financieras, sino a usuarios particulares o pequeños perfiles inversores que necesitan una herramienta sencilla y basada en datos.

### Por qué tiene valor

El proyecto tiene valor porque puede mejorar la toma de decisiones y la planificación financiera. Una herramienta así permitiría visualizar el riesgo real de una cartera, detectar concentración excesiva y comparar distintas alternativas de asignación de capital.

También puede ahorrar tiempo, al automatizar cálculos que normalmente requerirían hojas de cálculo o conocimientos financieros avanzados. Además, aporta transparencia mediante métricas como volatilidad, rentabilidad histórica, *drawdown*, correlación entre activos y exposición por sectores. Su valor no depende de acertar movimientos de corto plazo: puede ayudar a construir carteras más equilibradas, comprensibles y alineadas con el nivel de riesgo del usuario.

---

## Conclusión inicial

Las tres ideas planteadas tienen relación con Data Science, IA o analítica aplicada a decisiones financieras, pero abordan problemas diferentes.

**AlphaSense** es la idea más ambiciosa: busca apoyar decisiones de inversión combinando datos de mercado y sentimiento. Tiene un alto potencial de valor, pero también mayor complejidad y riesgo.

**MarketPulse** se centra en detectar situaciones anómalas y oportunidades tempranas. Está especialmente acotada y permite construir una solución de alerta y priorización.

**SmartPortfolio** está orientada a planificación y control del riesgo. Puede ser menos llamativa, pero tiene un caso de uso claro, datos razonablemente disponibles y utilidad directa para inversores particulares.

De cara a las siguientes entregas, **AlphaSense** y **MarketPulse** parecen las más prometedoras por combinar valor económico, interés técnico y la posibilidad de construir una solución basada en datos con impacto práctico.
