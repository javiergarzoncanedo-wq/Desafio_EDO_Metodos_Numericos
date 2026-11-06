Desafío 1: La Paz frente a una Crisis de Agua
DOCUMENTACIÓN TÉCNICA Y README DEL PROYECTO WEB DE SIMULACIÓN EDO
―――――――――――――――――――――――――――――――――――――――――――――――――――――――
1. Descripción General del Proyecto
Este proyecto es una aplicación web interactiva desarrollada para simular y analizar el comportamiento del volumen almacenado en los embalses de Incachaca y Hampaturi que abastecen a la ciudad de La Paz, Bolivia. Utiliza un modelo cuantitativo basado en una Ecuación Diferencial Ordinaria (EDO) de primer orden, comparando la solución analítica exacta con métodos numéricos como el Método de Heun (RK2) y Runge-Kutta de 4.º Orden (RK4).
Propósito del Simulador:
Ofrecer una herramienta interactiva de gestión ambiental y toma de decisiones comunitarias que permita anticipar el día exacto de racionamiento (reserva del 20%) y el colapso por agotamiento total, evaluando políticas de ahorro del consumo urbano frente a episodios de sequía severa.
2. Arquitectura de Software y Tecnologías
La aplicación está construida en una arquitectura de archivo único (Single Page Application - SPA) de ejecución completamente del lado del cliente (Client-Side Rendering), garantizando portabilidad, velocidad inmediata y despliegue sin dependencias de servidor.
•	HTML5 Estructurado: Estructuración de componentes, maquetación receptiva y formularios de entrada de parámetros.
•	Tailwind CSS & FontAwesome: Framework CSS por CDN para el diseño limpio (Light Mode), tarjetas redondeadas (glassmorphism), bordes interactivos e íconos gráficos.
•	Chart.js (v4.x): Renderizado dinámico de la trayectoria del volumen y(t) y el error relativo porcentual comparativo.
•	Motor Lógico JavaScript (ES6+): Implementación en JS puro de la EDO, métodos RK2/RK4, filtros de búsqueda en tiempo real, cambio de escenarios y exportación a formato CSV.
3. Modelo Matemático y Algoritmos Implementados
El balance hídrico del embalse se rige por la siguiente ecuación diferencial ordinaria de primer orden:
dy/dt = R - C - e · y(t)   =>   dy/dt + e · y(t) = R - C
3.1. Solución Analítica Exacta
Resolviendo mediante el factor integrante μ(t) = e^(e·t), la solución matemática exacta queda definida por:
y(t) = [ y₀ - (R - C) / e ] · e^(-e · t) + (R - C) / e
3.2. Métodos Numéricos Integrados
•	Método de Heun (RK2): Algoritmo predictor-corrector de segundo orden con convergencia O(h²).
•	Runge-Kutta de 4.º Orden (RK4): Promedio ponderado de cuatro pendientes (k₁, k₂, k₃, k₄) de cuarto orden con convergencia O(h⁴) y precisión coincidente con la solución exactísima.
4. Funcionalidades Clave de la Aplicación
•	Panel de Parámetros Dinámico: Modificación en tiempo real de volumen inicial (y₀), recarga (R), consumo urbano (C), evaporación (e), paso de tiempo (h) y horizonte de días.
•	Preajustes de Escenarios: Botones de un clic para alternar entre 'Consumo Normal', 'Ahorro del 15%' y 'Sequía (-30% Aportes)'.
•	Visualización Gráfica Dual: Dos gráficos simultáneos para la trayectoria del agua y la evaluación del error porcentual.
•	Tabla de Iteraciones y Exportación CSV: Tabla detallada paso a paso con campo de búsqueda por día t y botón de descarga de la matriz de simulación en CSV.
•	Base de Datos de Resultados Dinámicos: Tabla en la parte inferior que recalcula al instante las variables de entrada y métricas de salida para los 3 escenarios clave según las entradas del usuario.
5. Matriz de Resultados Comparativos por Escenario
A continuación se resume la matriz de simulación generada automáticamente ante los valores base de configuración:
Escenario	y₀	R	C	Reserva (20%)	Agotamiento	Vol. Día 90	Error RK4
1. Consumo Normal	15.0	0.050	0.300	Día 52	Día 66	-4.70 hm³	< 0.00001%
2. Ahorro del 15%	15.0	0.050	0.255	Día 65 (+13d)	Día 84 (+18d)	-1.14 hm³	< 0.00001%
3. Sequía (-30% R)	15.0	0.035	0.300	Día 48 (-4d)	Día 61 (-5d)	-5.97 hm³	< 0.00001%
6. Instalación, Uso y Despliegue
Para ejecutar el proyecto no se requiere instalar servidores backend ni entornos Node.js:
•	1. Descarga del Proyecto: Descargar o clonar el repositorio que contiene el archivo index.html (o simulador_edo_crisis_de_agua_la_paz_corregido.html).
•	2. Ejecución Local: Hacer doble clic sobre el archivo ejecutable HTML o abrirlo desde cualquier navegador web moderno (Google Chrome, Mozilla Firefox, Microsoft Edge, Safari).
•	3. Publicación Web: El archivo es directamente compatible con plataformas de alojamiento estático como GitHub Pages, Vercel, Netlify o servidores Apache/Nginx sin configuración adicional.
