## 📊 Análisis Estadístico y Segmentación de Consumo en ConnectaTel

Este repositorio contiene el análisis de datos exploratorio (EDA), limpieza, auditoría de calidad de datos y segmentación de clientes para la empresa de telecomunicaciones **ConnectaTel**, desarrollado en un entorno reproducible de Python en Jupyter Notebook.

---

## 📌 Objetivos del Proyecto

* **Auditar y Limpiar Datasets:** Tratar valores *sentinel*, nulos, inconsistencias en registros de texto y anomalías técnicas de red.
* **Analizar Patrones de Consumo:** Evaluar la distribución del uso de voz (minutos/llamadas) y mensajería (SMS) por tipo de plan (**Básico** vs. **Premium**).
* **Segmentar Clientes:** Categorizar a los usuarios según su nivel de uso (Bajo, Medio, Alto) y sus grupos etarios (Jóven, Adulto, Adulto Mayor).
* **Generar Insights Ejecutivos:** Proveer recomendaciones estratégicas sobre la oferta comercial de planes y empaquetado de servicios.

---

## 📁 Estructura del Repositorio

```text
├── README.md                 # Descripción general e informe ejecutivo del proyecto
├── notebook_connectatel.ipynb # Jupyter Notebook estructurado con código y visualizaciones
└── data/                     # Datasets analizados
    ├── plans.csv             # Información y límites de los planes de la empresa
    ├── users_latam.csv       # Perfil demográfico de los clientes (4,000 registros)
    └── usage.csv             # Registros de eventos de voz y mensajería (40,000 registros)

## 🛠️ Tecnologías y Librerías Utilizadas

Python 3.x: Lenguaje de programación base del proyecto.
Pandas: Carga, manipulación, agregación y limpieza estructurada de datos.
NumPy: Operaciones vectorizadas de alto rendimiento y lógica condicional.
Matplotlib & Seaborn: Visualización de distribuciones (histogramas, boxplots, countplots) y análisis de outliers.

## 🔍 Hallazgos Críticos de Calidad de Datos

Valores Sentinel en Edad: Se identificaron 55 registros con el valor -999 en age (1.38% de la base), los cuales fueron imputados exitosamente con la mediana de la población (48 años).
Valores Faltantes en Ciudad: Se detectaron 212 registros con '?' en la columna city (5.30%).
Inyección Falso-Positiva en SMS: Se hallaron 16 registros de tipo text contaminados por error con duration = 120.0 minutos. Se corrigió el cálculo de agregación filtrando únicamente los eventos de tipo call, evitando inflar artificialmente 1,920 minutos falsos en la base.
Capping Técnico de Red: Se detectaron 14 llamadas con una duración idéntica de 120.0 minutos (9 en Básico y 5 en Premium), atribuidas a un corte automático de seguridad de la red ante llamadas excesivamente prolongadas.

## 📈 Resumen Ejecutivo e Insights

1. Segmentación de Usuarios
Por Nivel de Uso:
•	Uso Medio: 73.8% (~2,950 usuarios) — Segmento dominante en la operación.
•	Bajo Uso: 19.2% (~770 usuarios).
•	Alto Uso: 7.0% (~280 usuarios).
Por Grupo Etario:
•	Adulto (30-59 años): 50.5% (~2,020 usuarios) — Representa más de la mitad de la base.
•	Adulto Mayor (≥60 años): 30.5% (~1,220 usuarios).
•	Joven (<30 años): 19.0% (~760 usuarios).
💡 Insight Clave: El consumo es transversal a las edades; pertenecer a un grupo etario específico no altera drásticamente la intensidad de uso de los servicios.

## 📈 Rentabilidad y Consumo de Planes
•	Plan Básico: Aporta el 64.88% de los usuarios (2,595 clientes) y genera el 63.7% del tráfico total de voz (58,576.7 min).
•	Plan Premium: Representa el 35.12% de los clientes (1,405 usuarios). Muestra promedios de consumo individual prácticamente idénticos al plan Básico (22.88 min vs. 22.17 min), convirtiéndolo en el segmento con mayor margen de rentabilidad neta para la compañía.
•	Sobredimensionamiento de Cuotas: Ningún cliente en el Plan Premium aprovecha la bolsa de 600 minutos (el consumo orgánico máximo registrado fue de 84.77 min). Asimismo, el uso promedio de SMS (5.5 SMS/usuario) confirma la baja relevancia del servicio de mensajería tradicional frente al uso de datos.

## 💡 Recomendaciones Estratégicas para el Negocio
•	Captura y Análisis del Consumo de Datos (GB): Priorizar como acción técnica inmediata la recolección del consumo de internet por usuario para realizar un diagnóstico más asertivo en relación con las necesidades reales del mercado.
•	Rediseño General de Ofertas de Voz: Reducir sustancialmente bolsas de voz excesivas (como los 600 minutos de Premium) y orientar la propuesta de valor hacia la navegación móvil.
•	Reempaquetado del Plan Premium: Ajustar el umbral de voz a 150 - 200 minutos e integrar beneficios agregados (plataformas de streaming, roaming internacional, gigas libres) para blindar la base contra el downgrade hacia el plan Básico.
•	Optimización de Red y Facturación: Revisar el límite de corte a los 120 minutos en los conmutadores de red para evitar cobros indebidos de excedentes o insatisfacción del cliente cuando ocurra el capping automático.



