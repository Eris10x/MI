import streamlit as st
import pandas as pd
import plotly.express as px
import numpy as np
from datetime import datetime, timedelta
import plotly.graph_objects as go

# Configuración inicial de la página
st.set_page_config(
    page_title="Guía Interactiva: Dashboards con Streamlit",
    page_icon="📊",
    layout="wide"
)

# Título principal
st.title("📊 Guía Interactiva: Creación de Dashboards con Streamlit")
st.markdown("**Por: Erick E. Alarcón R.**")

# Sidebar para navegación
st.sidebar.title("Navegación")
pagina = st.sidebar.radio(
    "Selecciona una sección:",
    ["Introducción", "Python", "Streamlit", "Dashboard", "Planificación", 
     "Recopilación de requisitos", "Construcción del dashboard", "Caso práctico"]
)

# INTRODUCCIÓN
if pagina == "Introducción":
    st.header("De la intuición a la visualización: el poder de los dashboards interactivos")
    
    st.write("""
    ¿Cansado de tomar decisiones cruciales basándose solo en la intuición? La verdadera necesidad de hoy es 
    transformar datos complejos en visibilidad objetiva y accionable. 
    
    Deja atrás las hojas de cálculo estáticas. Mejor opta por la funcionalidad de un dashboard interactivo, 
    el cual tiene el potencial de brindarte, por ejemplo, la clasificación "semáforo" del rendimiento de tu 
    equipo o gráficos de líneas que muestran el progreso de tus indicadores clave.
    
    **Te invito a seguir el desarrollo de esta guía práctica y visual**, donde usaré Streamlit para transformar 
    conceptos técnicos en herramientas accesibles y útiles. Esta guía está especialmente diseñada para personas 
    con conocimientos, incluso principiantes, en Python, ya que te permitirá construir y publicar dashboards 
    funcionales con poco código. Además, cualquier persona interesada en el mundo de los datos obtendrá 
    información esencial sobre qué es un dashboard, Python y Streamlit.
    """)
    
    st.subheader("📈 Importancia de los gráficos y propósito de la guía")
    
    st.write("""
    En la actualidad, los gráficos tienen un papel fundamental en la toma de decisiones de todos los sectores, 
    desde el deporte hasta los negocios, esto en parte gracias a los avances tecnológicos que cada día nos 
    permiten crear gráficos más complejos y precisos.
    """)
    
    st.info("""
    **Objetivo de esta guía:** Dar a conocer el proceso previo a la creación de dashboards, pero principalmente 
    busca enseñar a usar la librería de Streamlit.
    """)
    
    # VISTA PREVIA INTERACTIVA - SEMÁFORO Y GRÁFICOS DE LÍNEAS
    st.subheader("🔍 Vista previa: Experimenta el poder de un dashboard interactivo")
    
    st.info("""
    **Aquí puedes ver en acción exactamente lo que aprenderás a crear:** un sistema de clasificación por semáforo 
    y gráficos de tendencia que transforman datos crudos en insights accionables.
    """)
    
    # Generar datos de ejemplo para agentes
    np.random.seed(42)
    agentes = ['Ana García', 'Carlos López', 'María Rodríguez', 'Pedro Martínez', 'Laura Hernández']
    ventas_totales = np.random.randint(10000000, 25000000, len(agentes))
    
    datos_agentes = pd.DataFrame({
        'Agente': agentes,
        'Ventas Totales': ventas_totales
    })
    
    # Función para clasificar rendimiento
    def clasificar_rendimiento(ventas):
        if ventas >= 19000000:
            return "🟢 Excelente"
        elif ventas >= 14000000:
            return "🟡 Regular"
        else:
            return "🔴 Necesita mejora"
    
    datos_agentes['Rendimiento'] = datos_agentes['Ventas Totales'].apply(clasificar_rendimiento)
    
    # Crear datos para gráfico de líneas (tendencias mensuales)
    meses = ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio']
    tendencias_data = {}
    
    for agente in agentes:
        base = np.random.randint(500000, 1500000)
        tendencia = [base + np.random.randint(-200000, 400000) * i for i in range(len(meses))]
        tendencias_data[agente] = tendencia
    
    datos_tendencias = pd.DataFrame(tendencias_data)
    datos_tendencias['Mes'] = meses
    
    # Mostrar en dos columnas
    col1, col2 = st.columns(2)
    
    with col1:
        st.subheader("🚦 Clasificación Semáforo - Rendimiento del Equipo")
        
        # Mostrar métricas resumidas
        total_excelente = len(datos_agentes[datos_agentes['Rendimiento'] == "🟢 Excelente"])
        total_regular = len(datos_agentes[datos_agentes['Rendimiento'] == "🟡 Regular"])
        total_mejora = len(datos_agentes[datos_agentes['Rendimiento'] == "🔴 Necesita mejora"])
        
        metric_col1, metric_col2, metric_col3 = st.columns(3)
        with metric_col1:
            st.metric("🟢 Excelente", total_excelente)
        with metric_col2:
            st.metric("🟡 Regular", total_regular)
        with metric_col3:
            st.metric("🔴 Necesita mejora", total_mejora)
        
        # Mostrar tabla con semáforo
        st.dataframe(
            datos_agentes.style.applymap(
                lambda x: 'background-color: #90EE90' if 'Excelente' in str(x) 
                else ('background-color: #FFE4B5' if 'Regular' in str(x) 
                      else 'background-color: #FFB6C1' if 'Necesita mejora' in str(x) 
                      else ''),
                subset=['Rendimiento']
            ).format({
                'Ventas Totales': '${:,.0f}'
            }),
            use_container_width=True
        )
        
        st.caption("**Criterios:** 🟢 ≥ $19M | 🟡 $14M-$19M | 🔴 < $14M")
    
    with col2:
        st.subheader("📈 Progreso de Indicadores Clave")
        
        # Selector de agente para el gráfico
        agente_seleccionado = st.selectbox(
            "Selecciona un agente para ver su tendencia:",
            agentes
        )
        
        # Preparar datos para el gráfico del agente seleccionado
        datos_agente_tendencia = pd.DataFrame({
            'Mes': meses,
            'Ventas': datos_tendencias[agente_seleccionado]
        })
        
        # Crear gráfico de líneas
        fig = px.line(
            datos_agente_tendencia, 
            x='Mes', 
            y='Ventas',
            title=f'Tendencia de Ventas - {agente_seleccionado}',
            markers=True
        )
        
        fig.update_layout(
            yaxis_tickprefix='$',
            yaxis_tickformat=',.0f',
            xaxis_title='Mes',
            yaxis_title='Ventas Mensuales'
        )
        
        # Añadir línea de tendencia
        z = np.polyfit(range(len(meses)), datos_agente_tendencia['Ventas'], 1)
        tendencia_lineal = np.poly1d(z)(range(len(meses)))
        
        fig.add_scatter(
            x=meses,
            y=tendencia_lineal,
            mode='lines',
            line=dict(dash='dash', color='red', width=2),
            name='Tendencia'
        )
        
        st.plotly_chart(fig, use_container_width=True)
        
        # Mostrar estadísticas rápidas
        ventas_actual = datos_agente_tendencia['Ventas'].iloc[-1]
        ventas_inicial = datos_agente_tendencia['Ventas'].iloc[0]
        crecimiento = ((ventas_actual - ventas_inicial) / ventas_inicial) * 100
        
        stat_col1, stat_col2 = st.columns(2)
        with stat_col1:
            st.metric("Ventas Actuales", f"${ventas_actual:,.0f}")
        with stat_col2:
            st.metric("Crecimiento", f"{crecimiento:+.1f}%")
    
    # Llamada a la acción
    st.markdown("---")
    st.write("""
    **¿Listo para crear tus propios dashboards como este?** Esta guía te llevará paso a paso desde los 
    fundamentos de Python y Streamlit hasta la publicación de tu primer dashboard interactivo. 
    ¡Sigue leyendo para comenzar tu journey en el mundo de la visualización de datos!
    """)

# PYTHON
elif pagina == "Python":
    st.header("🐍 ¿Qué es Python?")
    
    col1, col2 = st.columns([2, 1])
    
    with col1:
        st.write("""
        Python es un lenguaje de programación potente y fácil de aprender en comparación con otros 
        como C y C++. Se caracteriza por tener varios usos en ciencia de datos y desarrollo web.
        
        **Librerías en Python:** Python provee por defecto sus propias librerías, sin embargo, 
        gracias a su comunidad grande y activa, podemos encontrar un gran número de librerías adicionales.
        """)
    
    with col2:
        st.info("""
        **💡 Datos 2024:**
        Python fue el tercer lenguaje más usado por desarrolladores
        """)
    
    # Gráfico de popularidad actualizado
    st.subheader("📊 Popularidad de Lenguajes de Programación 2024")
    
    lenguajes = pd.DataFrame({
        'Lenguaje': ['JavaScript', 'HTML/CSS', 'Python', 'SQL', 'TypeScript'],
        'Porcentaje': [62.3, 52.9, 52.0, 51.0, 38.5]
    })
    
    fig = px.bar(lenguajes, x='Porcentaje', y='Lenguaje', 
                title='Lenguajes más utilizados por desarrolladores (%)',
                orientation='h',
                color='Porcentaje',
                color_continuous_scale='viridis')
    fig.update_layout(yaxis={'categoryorder':'total ascending'})
    st.plotly_chart(fig, use_container_width=True)
    
    # Tipos de librerías interactivo
    st.subheader("📚 Tipos de Librerías en Python")
    
    # Definir ejemplos de librerías
    librerias = {
        "Deep Learning": {
            "TensorFlow": "Redes neuronales y aprendizaje profundo",
            "PyTorch": "Investigación en ML y redes neuronales"
        },
        "Machine Learning": {
            "Scikit-learn": "Algoritmos de ML clásicos",
            "XGBoost": "Algoritmos de boosting para ML"
        },
        "Cálculo numérico": {
            "NumPy": "Operaciones matemáticas y arrays",
            "SciPy": "Algoritmos científicos y matemáticos"
        },
        "Visualización": {
            "Matplotlib": "Gráficos estáticos 2D/3D",
            "Plotly": "Gráficos interactivos y dashboards"
        }
    }
    
    # Selector de categoría
    categoria_seleccionada = st.selectbox(
        "Selecciona una categoría de librerías:",
        list(librerias.keys())
    )
    
    # Mostrar librerías de la categoría seleccionada
    st.write(f"**Ejemplos de {categoria_seleccionada}:**")
    
    col1, col2 = st.columns(2)
    
    with col1:
        for i, (lib, desc) in enumerate(librerias[categoria_seleccionada].items()):
            if i % 2 == 0:
                with st.expander(f"📦 {lib}"):
                    st.write(desc)
    
    with col2:
        for i, (lib, desc) in enumerate(librerias[categoria_seleccionada].items()):
            if i % 2 == 1:
                with st.expander(f"📦 {lib}"):
                    st.write(desc)
    
    # Información adicional sobre librerías
    st.info("""
    **💡 Tip:** Las librerías son compilaciones de código que te permiten acceder a funciones especiales, 
    ahorrando tiempo y ejecutando tareas con menos líneas de código.
    """)

# STREAMLIT
elif pagina == "Streamlit":
    st.header("🚀 ¿Qué es Streamlit?")
    
    col1, col2 = st.columns([3, 1])
    
    with col1:
        st.write("""
        Es una librería de Python de código abierto con la cual se pueden crear aplicaciones web 
        de ciencia de datos. 
        
        **¿Qué es una aplicación web?** Es un software que se ejecuta en el navegador y mediante 
        este interactúas (no solo consumes información como en una página web). Digamos que es 
        una aplicación (celular o pc) que funciona desde el navegador.
        
        Streamlit se creó para que científicos de datos con conocimiento en Python puedan publicar 
        resultados, pese a no tener conocimientos en programación web.
        """)
    
    with col2:
        st.warning("""
        **⚠️ Dato importante:**
        Streamlit **no** es una librería que Python trae por defecto.
        """)
    
    # Ventajas y desventajas
    col1, col2 = st.columns(2)
    
    with col1:
        st.subheader("✅ Ventajas")
        st.success("""
        - Permite crear aplicaciones con poco código
        - Integración con bibliotecas de ciencia de datos
        - Componentes interactivos
        - Fácil de aprender
        """)
    
    with col2:
        st.subheader("❌ Desventajas")
        st.error("""
        - Personalización limitada
        - Requiere instalación adicional
        - Menos opciones de diseño que herramientas web nativas
        """)
    
    # Ejemplos de uso interactivo actualizados
    st.subheader("💡 Usos comunes de Streamlit")
    
    # Diccionario de usos con enlaces y descripciones
    usos_info = {
        "Dashboards": {
            "descripcion": "Perfecto para mostrar métricas de negocio en tiempo real",
            "ejemplos": [
                {"nombre": "Población de Estados Unidos", "url": "https://population-dashboard.streamlit.app/?ref=blog.streamlit.io"}
            ]
        },
        "Análisis de información": {
            "descripcion": "Ideal para explorar datasets y compartir hallazgos",
            "ejemplos": [
                {"nombre": "Análisis del rendimiento de varias acciones en el tiempo", "url": "https://demo-stockpeers.streamlit.app/?ref=streamlit-io-gallery-finance-business"},
                {"nombre": "Analiza los hábitos de lectura de una persona", "url": "https://goodreads.streamlit.app/?ref=streamlit-io-gallery-data-visualization"}
            ]
        },
        "Encuestas": {
            "descripcion": "Crear formularios y encuestas interactivas",
            "ejemplos": [
                {"nombre": "Encuesta para evaluar satisfacción de pacientes en un hospital", "url": "https://mehedi-framework-patientsatisfaction-form.streamlit.app/?ref=streamlit-io-gallery-geography-society"}
            ]
        },
        "Juegos simples": {
            "descripcion": "Desarrolla juegos básicos como laberintos y aventuras RPG",
            "ejemplos": [
                {"nombre": "Aventura RPG", "url": "https://adventure.streamlit.app/?ref=streamlit-io-gallery-sports-fun"},
                {"nombre": "Laberinto", "url": "https://dungeon.streamlit.app/?ref=streamlit-io-gallery-sports-fun"}
            ]
        },
        "Prototipos rápidos": {
            "descripcion": "Ideal para probar ideas rápidamente y visualizar datos",
            "ejemplos": [
                {"nombre": "Muestra la integración y visualización de gráficos interactivos de la librería Apache ECharts", "url": "https://echarts.streamlit.app/?ref=streamlit-io-gallery-favorites"}
            ]
        }
    }
    
    uso_seleccionado = st.selectbox(
        "Selecciona un uso común para ver más detalles:",
        list(usos_info.keys())
    )
    
    # Mostrar información del uso seleccionado
    info = usos_info[uso_seleccionado]
    st.write(f"**Descripción:** {info['descripcion']}")
    
    st.write("**Ejemplos en línea:**")
    for ejemplo in info['ejemplos']:
        st.markdown(f"- [{ejemplo['nombre']}]({ejemplo['url']})")
    
    # Ejemplo de código simple - AHORA VISUALIZADO DIRECTAMENTE
    st.subheader("🛠️ Ejemplo rápido de Streamlit")
    
    st.write("**Código:**")
    st.code("""
import streamlit as st
import pandas as pd

# Título de la app
st.title('Mi primera app con Streamlit')

# Cargar datos
data = pd.DataFrame({
    'A': [1, 2, 3, 4],
    'B': [10, 20, 30, 40]
})

# Mostrar datos
st.write('Mis datos:', data)

# Slider interactivo
x = st.slider('Selecciona un valor:', 0, 100, 50)
st.write(f'Valor seleccionado: {x}')
    """, language='python')
    
    st.write("**Resultado (simulado en esta misma app):**")
    
    # Simulamos el resultado del código anterior
    st.title('Mi primera app con Streamlit')
    
    data = pd.DataFrame({
        'A': [1, 2, 3, 4],
        'B': [10, 20, 30, 40]
    })
    
    st.write('Mis datos:', data)
    
    x = st.slider('Selecciona un valor:', 0, 100, 50, key="demo_slider")
    st.write(f'Valor seleccionado: {x}')

# DASHBOARD
elif pagina == "Dashboard":
    st.header("📈 ¿Qué es un Dashboard?")
    
    st.write("""
    Es una herramienta visual que proporciona datos relevantes para una mejor toma de decisiones. 
    Permite comprender la situación actual, y además ayuda a identificar tendencias o problemas potenciales.
    
    Los dashboards se pueden aplicar a un sin fin de áreas, tales como recursos humanos, contabilidad, ventas, etc.
    """)
    
    # Lista comparativa de herramientas
    st.subheader("🛠️ Comparación de herramientas para dashboards")
    
    col1, col2 = st.columns(2)
    
    with col1:
        st.markdown("""
        **Power BI**
        - ✅ Integración con Microsoft Office
        - ✅ Fácil de usar
        - ✅ Buen soporte empresarial
        - ❌ Licencias costosas
        - ❌ Menos flexibilidad para personalización
        
        **Google Data Studio**
        - ✅ Gratuito
        - ✅ Integración con Google services
        - ✅ Fácil colaboración
        - ❌ Limitado en transformación de datos
        - ❌ Menos opciones de visualización
        """)
    
    with col2:
        st.markdown("""
        **Tableau**
        - ✅ Visualizaciones poderosas
        - ✅ Gran capacidad de análisis
        - ✅ Comunidad activa
        - ❌ Muy costoso
        - ❌ Curva de aprendizaje pronunciada
        
        **Streamlit**
        - ✅ Totalmente personalizable
        - ✅ Gratuito y open-source
        - ✅ Integración con Python
        - ❌ Requiere conocimientos de programación
        - ❌ Personalización limitada en componentes básicos
        """)
    
    # Recomendación
    st.info("""
    **🤔 ¿Streamlit o Power BI?**
    
    **Conviene usar Streamlit si:**
    - Ya sabes Python y conoces las librerías de Ciencias de datos
    - Necesitas máxima flexibilidad y personalización
    - Tu equipo tiene habilidades de programación
    
    **Conviene usar Power BI si:**
    - Trabajas con el entorno de MS Office
    - Necesitas una solución rápida sin programación
    - Tu organización ya usa el ecosistema Microsoft
    """)

# PLANIFICACIÓN
elif pagina == "Planificación":
    st.header("📋 Planificación")
    
    st.write("""
    La planificación adecuada es crucial para crear un dashboard efectivo. 
    """)
    
    # Información sobre origen basada en el PDF
    st.subheader("🎯 Origen")
    st.write("""
    Define el objetivo del dashboard y los problemas que se buscan resolver. Esto con el fin de que la 
    estructura y diseño sea el idóneo.
    """)
    
    # Fuentes de datos interactivas basadas en el PDF
    st.subheader("📊 Selección de fuentes de datos")
    st.write("Selecciona de dónde saldrán los datos y cómo se accederá a ellos.")
    
    # Diccionario con información de fuentes de datos
    fuentes_datos = {
        "Excel": {
            "ventajas": "• Fácil acceso y manipulación",
            "descripcion": "Archivos de Excel (.xlsx, .xls) son ampliamente utilizados en entornos empresariales",
            "uso_tipico": "Datos estructurados, reportes mensuales, datos financieros"
        },
        "SQL": {
            "ventajas": "• Ideal para manejar grandes volúmenes",
            "descripcion": "Bases de datos relacionales como MySQL, PostgreSQL, SQL Server",
            "uso_tipico": "Datos transaccionales, aplicaciones web, sistemas empresariales"
        },
        "CSV": {
            "ventajas": "• Ligeros, portables y fáciles de leer",
            "descripcion": "Archivos de texto separados por comas, universales y compatibles",
            "uso_tipico": "Intercambio de datos, exportaciones de sistemas, datos simples"
        }
    }
    
    fuente_seleccionada = st.selectbox(
        "Selecciona una fuente de datos para ver más detalles:",
        list(fuentes_datos.keys())
    )
    
    # Mostrar información de la fuente seleccionada
    info_fuente = fuentes_datos[fuente_seleccionada]
    
    col1, col2 = st.columns(2)
    
    with col1:
        st.info(f"**{fuente_seleccionada}**")
        st.write(info_fuente["ventajas"])
    
    with col2:
        with st.expander("📋 Detalles completos"):
            st.write(f"**Descripción:** {info_fuente['descripcion']}")
            st.write(f"**Uso típico:** {info_fuente['uso_tipico']}")

# RECOPILACIÓN DE REQUISITOS
elif pagina == "Recopilación de requisitos":
    st.header("🎙️ Recopilación de requisitos")
    
    st.write("""
    Conocer las necesidades: Realizar entrevistas a los principales interesados para determinar 
    las necesidades y expectativas con respecto al dashboard.
    """)
    
    # Checklist interactivo (sin simulador de entrevista)
    st.subheader("📝 Checklist para la entrevista")
    
    col1, col2 = st.columns(2)
    
    with col1:
        st.markdown("""
        **Requisitos de información:**
        - ¿Qué indicadores se van a mostrar?
        - ¿Cómo cambian en el tiempo?
        - ¿Qué periodos de tiempo son relevantes?
        - ¿Qué nivel de detalle necesitas?
        - ¿Qué comparativas son importantes?
        """)
    
    with col2:
        st.markdown("""
        **Requisitos funcionales:**
        - ¿Qué filtros necesita el usuario?
        - ¿Necesita actualización en tiempo real?
        - ¿Qué tipo de gráficos prefiere?
        - ¿Necesita exportar datos?
        - ¿Qué dispositivos usará para ver el dashboard?
        """)
    
    # Consejos adicionales
    with st.expander("💡 Consejos para una entrevista efectiva"):
        st.markdown("""
        - **Prepara preguntas específicas** pero deja espacio para respuestas abiertas
        - **Escucha activamente** y toma notas de los requisitos no mencionados inicialmente
        - **Pide ejemplos concretos** de reportes o métricas que usan actualmente
        - **Confirma tu entendimiento** repitiendo los requisitos clave
        - **Establece prioridades** - no todos los requisitos son igual de importantes
        """)

# CONSTRUCCIÓN DEL DASHBOARD
elif pagina == "Construcción del dashboard":
    st.header("🛠️ Construcción del dashboard")
    
    st.write("""
    Selecciona el tipo de gráfico según tus necesidades. Cada tipo de visualización tiene propósitos 
    específicos y es más efectivo para ciertos tipos de datos.
    """)
    
    # Selector de tipos de gráficos - TODOS los mencionados en el PDF
    tipo_grafico = st.selectbox(
        "Selecciona un tipo de gráfico para explorar:",
        [
            "Gráfico de columnas", "Gráfico de barras", "Gráfico de líneas", 
            "Gráfico de dispersión", "Gráfico de pastel", "Gráfico de tabla",
            "Gráfico de cajas y bigotes", "Gráfico de burbujas"
        ]
    )
    
    # Variable para controlar si mostramos el gráfico estándar
    mostrar_grafico_estandar = True
    
    # Generar datos de ejemplo según el tipo de gráfico
    if tipo_grafico == "Gráfico de columnas":
        st.info("**Útil para:** Comparar entre categorías. Eje X: datos cualitativos, Eje Y: datos cuantitativos")
        datos = pd.DataFrame({
            'Ciudad': ['Ciudad A', 'Ciudad B', 'Ciudad C', 'Ciudad D', 'Ciudad E'],
            'Ventas': [25, 35, 30, 40, 20],
            'Meta': [30, 30, 30, 30, 30]
        })
        fig = px.bar(datos, x='Ciudad', y=['Ventas', 'Meta'], 
                    title='Ventas por Ciudad vs Meta', barmode='group')
        
    elif tipo_grafico == "Gráfico de barras":
        st.info("**Útil para:** Comparar entre categorías (recomendado para más de 10 categorías)")
        datos = pd.DataFrame({
            'Producto': ['Producto A', 'Producto B', 'Producto C', 'Producto D', 'Producto E', 'Producto F'],
            'Cantidad Vendida': [150, 200, 180, 220, 190, 210]
        })
        fig = px.bar(datos, y='Producto', x='Cantidad Vendida', 
                    title='Gráfico de Barras - Productos Más Vendidos', 
                    orientation='h', color='Cantidad Vendida')
        
    elif tipo_grafico == "Gráfico de líneas":
        st.info("**Útil para:** Mostrar tendencias o progresos a través del tiempo")
        datos = pd.DataFrame({
            'Mes': ['Ene', 'Feb', 'Mar', 'Abr', 'May', 'Jun', 'Jul', 'Ago'],
            'Ventas': [100, 150, 130, 200, 180, 220, 210, 240],
            'Gastos': [80, 90, 100, 110, 95, 120, 115, 130]
        })
        fig = px.line(datos, x='Mes', y=['Ventas', 'Gastos'], 
                     title='Tendencia Mensual de Ventas y Gastos', markers=True)
        
    elif tipo_grafico == "Gráfico de dispersión":
        st.info("**Útil para:** Mostrar la relación entre dos variables cuantitativas")
        np.random.seed(42)
        datos = pd.DataFrame({
            'Tamaño (m²)': np.random.randint(50, 200, 50),
            'Precio (millones)': np.random.randint(1, 5, 50) + np.random.rand(50),
            'Zona': np.random.choice(['Norte', 'Sur', 'Este', 'Oeste'], 50)
        })
        fig = px.scatter(datos, x='Tamaño (m²)', y='Precio (millones)', color='Zona',
                        title='Relación entre Tamaño y Precio de Propiedades',
                        trendline="ols")
        
    elif tipo_grafico == "Gráfico de pastel":
        st.info("**Útil para:** Conjuntos de datos pequeño. Representa los números en porcentaje y el total debe dar 100%")
        datos = pd.DataFrame({
            'Ciudad': ['Salamanca', 'Silao', 'León', 'Irapuato', 'Celaya'],
            'Porcentaje': [12.5, 25, 37.5, 15, 10.5]
        })
        fig = px.pie(datos, values='Porcentaje', names='Ciudad', 
                    title='Distribución de Ventas por Ciudad')
        
    elif tipo_grafico == "Gráfico de tabla":
        st.info("**Útil para:** Mostrar datos en filas y columnas para comparar valores. Útil para tops.")
        datos = pd.DataFrame({
            'Agente': ['Ana García', 'Carlos López', 'María Rodríguez', 'Pedro Martínez'],
            'Ventas Totales': [21850000, 19500000, 14200000, 12500000],
            'Propiedades Vendidas': [45, 38, 32, 28],
            'Rendimiento': ['🟢 Excelente', '🟡 Regular', '🔴 Necesita mejora', '🔴 Necesita mejora']
        })
        
        # Mostrar como tabla con estilo
        st.dataframe(
            datos.style.format({
                'Ventas Totales': '${:,.0f}'
            }).applymap(
                lambda x: 'background-color: #90EE90' if 'Excelente' in str(x) 
                else ('background-color: #FFE4B5' if 'Regular' in str(x) 
                      else 'background-color: #FFB6C1' if 'Necesita mejora' in str(x) 
                      else ''),
                subset=['Rendimiento']
            ),
            use_container_width=True
        )
        st.plotly_chart(px.bar(datos, x='Agente', y='Ventas Totales', 
                              title='Ranking de Agentes - Tabla Complementaria'), 
                       use_container_width=True)
        # No mostrar el gráfico estándar para tablas
        mostrar_grafico_estandar = False
        
    elif tipo_grafico == "Gráfico de cajas y bigotes":
        st.info("**Útil para:** Visualizar distribuciones, comparar grupos y detectar datos atípicos")
        np.random.seed(42)
        datos = pd.DataFrame({
            'Zona': np.repeat(['Norte', 'Sur', 'Este', 'Oeste'], 25),
            'Precio': np.concatenate([
                np.random.normal(2.5, 0.5, 25),
                np.random.normal(3.0, 0.6, 25),
                np.random.normal(2.8, 0.4, 25),
                np.random.normal(3.2, 0.7, 25)
            ])
        })
        fig = px.box(datos, x='Zona', y='Precio', 
                    title='Distribución de Precios por Zona',
                    points="all")
        fig.update_layout(yaxis_title='Precio (millones)')
        
    else:  # Gráfico de burbujas
        st.info("**Útil para:** Gráfico de dispersión que representa 3 variables cuantitativas")
        datos = pd.DataFrame({
            'Ingresos (millones)': np.random.randint(10, 50, 20),
            'Clientes': np.random.randint(100, 1000, 20),
            'Tamaño Empresa': np.random.randint(1, 100, 20),
            'Sector': np.random.choice(['Tecnología', 'Inmobiliario', 'Retail', 'Servicios'], 20)
        })
        fig = px.scatter(datos, x='Ingresos (millones)', y='Clientes',
                        size='Tamaño Empresa', color='Sector',
                        title='Gráfico de Burbujas: Ingresos vs Clientes vs Tamaño',
                        hover_name='Sector', size_max=40)
    
    # Mostrar el gráfico estándar (excepto para tablas que ya se mostraron)
    if mostrar_grafico_estandar:
        st.plotly_chart(fig, use_container_width=True)
    
    # Información adicional sobre selección de gráficos
    with st.expander("📋 Guía rápida para seleccionar gráficos"):
        st.markdown("""
        - **Comparar categorías:** Barras o Columnas
        - **Tendencias en el tiempo:** Líneas
        - **Relación entre variables:** Dispersión o Burbujas
        - **Distribución de partes:** Pastel (solo pocas categorías)
        - **Distribuciones estadísticas:** Cajas y bigotes
        - **Datos detallados:** Tablas
        """)

# CASO PRÁCTICO
elif pagina == "Caso práctico":
    st.header("🏢 Caso práctico: Agencia 'Max House'")
    
    st.write("""
    **Contexto:** La agencia administra 10 agentes de bienes raíces en México. 
    La dirección quiere ver el rendimiento de sus agentes y su progreso en el tiempo.
    """)
    
    # Información del caso
    col1, col2 = st.columns(2)
    
    with col1:
        st.subheader("🎯 Origen")
        st.markdown("""
        - **Objetivo:** Clasificar agentes según desempeño (premiar/capacitar/baja)
        - **Problema:** No hay visibilidad clara del rendimiento
        """)
    
    with col2:
        st.subheader("📊 Fuente de datos")
        st.markdown("""
        - **Tipo:** Archivo Excel
        - **Frecuencia:** Actualización mensual
        """)
    
    # Requisitos del dashboard
    st.subheader("📋 Recopilación de requisitos")
    
    st.markdown("""
    **Clasificación de agentes:**
    - 🟢 **Excelente:** ≥ 19 millones anuales
    - 🟡 **Regular:** 14-19 millones anuales  
    - 🔴 **Malo:** < 14 millones anuales
    """)
    
    st.markdown("""
    **Funcionalidades requeridas:**
    - Filtro por periodo y por agente
    - Panel tipo semáforo para clasificación
    - Ranking de mejores y peores agentes
    - Gráfico de progreso temporal
    """)
    
    # Estructura propuesta del dashboard
    st.subheader("🏗️ Construcción del dashboard")
    
    estructura = st.expander("Ver estructura completa")
    with estructura:
        st.markdown("""
        1. **Filtros en barra lateral:**
           - Selección de años
           - Selección de agente
        
        2. **Sección principal:**
           - Tabla de ranking de tops
           - Gráfico de líneas de ventas en el tiempo
           - Panel de rendimiento del agente (semáforo)
        """)

# Footer
st.markdown("---")
st.caption("Guía práctica para la creación de dashboards usando Streamlit - Por Erick E. Alarcón R.")
