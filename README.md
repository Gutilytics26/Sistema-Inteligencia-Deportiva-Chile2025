Scouting System Intelligence — Chile 2025
Sistema de Valuación y Gemelos Estadísticos · Primera División Chilena

El mercado de fichajes en el fútbol chileno carece de herramientas objetivas de valuación. Los clubes toman decisiones millonarias basadas en observación subjetiva y valores de mercado desactualizados.
Este sistema responde una pregunta concreta: ¿Cuánto debería valer realmente un jugador según su rendimiento estadístico comparado con sus pares?
Mediante un modelo de similitud estadística aplicado a 731 jugadores reales de la Primera División chilena 2025, el sistema estima el Fair Value de mercado de cada jugador, identifica sus gemelos estadísticos y diagnostica si está infravalorado, sobrevalorado o en precio justo.

Origen de los datos
Los datos provienen del cruce de dos fuentes internacionales:
- Transfermarkt - Web Scraping propio con Python
- Sofascore - Dataset proporcionado por RCL Scout Group


El pipeline de integración incluyó:

- Normalización de nombres de jugadores con unicodedata para resolver inconsistencias entre fuentes
- Deduplicación y validación de tipos de datos
- Construcción de dataset unificado con métricas de rendimiento y valor de mercado

Modelo de Fair Value
El corazón del sistema es un modelo de valuación basado en similitud coseno con las siguientes características:
# Filtro de pares comparables por posición y rango etario (±3 años)
# Escalado de features con StandardScaler
# Similitud coseno transformada de [-1, 1] → [0, 100]
# Fair Value = promedio ponderado por Similitud × Minutos jugados

¿Por qué similitud coseno?
Porque captura la dirección del perfil estadístico del jugador independientemente de la escala de las métricas un delantero de equipo grande y uno de equipo chico pueden tener perfiles estadísticos similares aunque sus volúmenes absolutos difieran.
Diagnóstico de mercado automático:

🟢 Infravalorado — Fair Value supera el valor actual en más de €150.000
🔴 Sobrevalorado — Valor actual supera el Fair Value en más de €150.000
🟡 Precio justo — Diferencia dentro del umbral
🧒 Potencial de exportación — Jugadores menores de 25 años con perfil proyectable

Funcionalidades del Dashboard
Análisis individual de jugador

- Búsqueda por nombre con normalización de caracteres
- Valor actual vs Fair Value estimado con delta
- Diagnóstico automático de posición de mercado

Posicionamiento en el mercado

- Scatter plot interactivo: Similitud estadística vs Valor de mercado
- Identificación visual del jugador analizado vs sus pares comparables
- Líneas de referencia de valor medio y similitud media

 Gemelos estadísticos IA

- Top 5 jugadores más similares estadísticamente
- Filtrados por misma posición y rango etario
- Barra de progreso de similitud porcentual

Stack Tecnológico: Python, Pandas / NumPy, scikit-learn, Plotly Express, Streamlit, BeautifulSoup / Selenium, unicodedata.

🚀 Correr el proyecto localmente
bash# Clonar el repositorio
git clone https://github.com/tu-usuario/scouting-chile-2025.git
cd scouting-chile-2025

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar la app
streamlit run app.py

Autor
Diego Gutiérrez Ávila
Data & Financial Analyst | Process Automation | Sports Analytics

