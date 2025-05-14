# Control de movimiento clase 24/04/2025
# Introducción 
El control de movimiento es una disciplina esencial en ingeniería mecatrónica que combina principios mecánicos, eléctricos y computacionales para lograr posicionamiento preciso en sistemas automatizados, desde maquinaria industrial hasta dispositivos médicos y aeroespaciales. Su diseño requiere no solo la selección adecuada de motores, sino también la optimización de transmisiones mecánicas (como tornillos guía, piñones-cremalleras o bandas transportadoras) para adaptar velocidad, torque e inercia entre el motor y la carga, considerando factores críticos como fricción, backlash y eficiencia. El cálculo de inercias reflejadas mediante ecuaciones, es clave para evitar sobredimensionamiento o inestabilidades dinámicas, mientras que herramientas como Simscape Multibody permiten simular y validar estos sistemas, equilibrando parámetros como la relación de inercia, torque pico y ciclos de trabajo para garantizar eficiencia y confiabilidad en aplicaciones reales.  

# 1. Conceptos de Transmisión 
## 1.1. Tornillo guía
  >🔑 ¿Qué es?: Mecanismo que convierte movimiento rotacional (motor) en lineal (carga). Usado en sistemas de posicionamiento de alta precisión (CNC, impresoras 3D).
### 1.1.1 Tipos de tornillos
* ACME (Rozca): Presentan una eficiencia mecánica del 35-85%, caracterizándose por su bajo costo pero mayor fricción en comparación con otros sistemas. Existen dos configuraciones geométricas principales para sus roscas: cuadrada y trapezoidal. La versión cuadrada, aunque más económica, presenta limitaciones estructurales significativas, particularmente en los flancos de la rosca, donde los picos agudos son susceptibles a fatiga y fractura por cargas cíclicas, lo que compromete su vida útil. En contraste, el diseño trapezoidal ofrece superior resistencia mecánica al distribuir las tensiones de forma más uniforme a lo largo del perfil de la rosca, minimizando la concentración de esfuerzos. Esta ventaja estructural aunque no reduce el riesgo de fallo a futuro, garantiza un movimiento más suave y estable de la bandeja o cama, especialmente en aplicaciones con altas cargas dinámicas o ciclos de trabajo continuos.
  
* Tornillos de Esferas (Ball Screws): Eficiencias del 85-95% en tornillos de bolas (vs 35-85% en ACME), menor fricción gracias al contacto rodante, y backlash reducido que garantiza posicionamiento preciso.




