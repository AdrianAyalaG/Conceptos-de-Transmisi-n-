# Control de movimiento clase 24/04/2025
# Introducción 
El control de movimiento es una disciplina esencial en ingeniería mecatrónica que combina principios mecánicos, eléctricos y computacionales para lograr posicionamiento preciso en sistemas automatizados, desde maquinaria industrial hasta dispositivos médicos y aeroespaciales. Su diseño requiere no solo la selección adecuada de motores, sino también la optimización de transmisiones mecánicas (como tornillos guía, piñones-cremalleras o bandas transportadoras) para adaptar velocidad, torque e inercia entre el motor y la carga, considerando factores críticos como fricción, backlash y eficiencia. El cálculo de inercias reflejadas mediante ecuaciones, es clave para evitar sobredimensionamiento o inestabilidades dinámicas, mientras que herramientas como Simscape Multibody permiten simular y validar estos sistemas, equilibrando parámetros como la relación de inercia, torque pico y ciclos de trabajo para garantizar eficiencia y confiabilidad en aplicaciones reales.  

# 1. Conceptos de Transmisión 
## 1.1. Tornillo guía
  >🔑 ¿Qué es?: Mecanismo que convierte movimiento rotacional (motor) en lineal (carga). Usado en sistemas de posicionamiento de alta precisión (CNC, impresoras 3D).

foto

### 1.1.1 Tipos de tornillos
* ACME (Rosca): Presentan una eficiencia mecánica del 35-85%, caracterizándose por su bajo costo pero mayor fricción en comparación con otros sistemas. Existen dos configuraciones geométricas principales para sus roscas: cuadrada y trapezoidal. La versión cuadrada, aunque más económica, presenta limitaciones estructurales significativas, particularmente en los flancos de la rosca, donde los picos agudos son susceptibles a fatiga y fractura por cargas cíclicas, lo que compromete su vida útil. En contraste, el diseño trapezoidal ofrece superior resistencia mecánica al distribuir las tensiones de forma más uniforme a lo largo del perfil de la rosca, minimizando la concentración de esfuerzos. Esta ventaja estructural aunque no reduce el riesgo de fallo a futuro, garantiza un movimiento más suave y estable de la bandeja o cama, especialmente en aplicaciones con altas cargas dinámicas o ciclos de trabajo continuos.
  
* Tornillos de Esferas (Ball Screws): Eficiencias del 85-95% en tornillos de bolas (vs 35-85% en ACME), menor fricción gracias al contacto rodante, y backlash reducido que garantiza posicionamiento preciso. Es importante tener en cuenta que el backlash es un problema asociado a un fenómeno de torsión, durante el cual, por un instante, no se transmite la fuerza de manera efectiva debido a una discontinuidad o juego en la cadena cinemática.

foto

### 1.1.2 Relación de Transmisión 
* Paso (Lead): Distancia lineal por revolución (
* Cabeceo (Pitch): Revoluciones por metro lineal (


## 1.2 Sistema Piñón - Cremallera
>🔑 ¿Qué es?: Mecanismo que convierte movimiento rotacional (piñón) en lineal (cremallera) mediante engrane directo. La cremallera casi siempre es metálica para soportar cargas pesadas y es por ello, que este tipo de transmisión es ideal para aplicaciones que requieren precisión y fuerza en ejes lineales.

foto

### 1.2.1 Relación de Transmisión 
>🔑 ¿Qué es?: Define cómo la velocidad angular del piñón $$w_{pinion}$$ se traduce en velocidad lineal de la cremallera $$V_{rack}$$

$$N_{RP}= \frac{1}{r_{pinion}}; V_{rack}= r_{pinion} * w_{pinion}$$

Donde  r_{pinion} será el radio del piñón. 

### 1.2.2 Inercia reflejada
>🔑 ¿Qué es?: Inercia equivalente "vista" por el motor:

Cómo formula matemática sería: Inercia del Piñón + Inercia de la carga + Inercia del carro 

$$J_{ref}= J_{pinion}+\frac{1}{\eta(N^{2})_{RP}}(\frac{W_{L}+W_{C}}{g})$$

* η: Eficiencia (típicamente 0.8 - 0.9 para buena eficiencia en el sistema; = 1 en ideal).
* $$W_{C}$$ es el peso de la cremallera

### 1.2.3 Torque reflejado
>🔑 ¿Qué es?: Torque que el motor debe generar para superar todas las fuerzas externas que se oponen al movimiento del sistema.

$$T_{load\to in}=\frac{F_{ext}}{\eta N_{RP}}$$

Donde $$F_{ext}$$ es la suma de todas las fuerzas externas y $$N_{RP}$$ la relación de transmisión adimensional.Es fundamental identificar qué elementos deben reflejarse en una ecuación, y estos corresponden a lo que se encuentra al otro lado de la transformación de energía.

## 1.3 Banda transoortadora 
>🔑 ¿Qué es?: Sistema que transmite movimiento mediante poleas y una banda continua, usado en transporte de materiales o líneas de ensamblaje.

### 1.3.1 Relación de transmisión (Poleas iguales) 

$$N_{BD}= \frac{1}{R_{IP}}; V_{belt}= r_{IP}* w_{IP}$$

$$r_{IP}$$ Es el radio de la polea de entrada, es decir, la que es motriz. 

### 1.3.2 Inercia reflejada
Considera inercias de poleas (2 poleas existentes en el sistema), de la banda y de la carga.

$$J_{ref}= 2J_{P}+\frac{1}{\eta(N^{2}_{RP})}(\frac{W_{L}+W_{C}}{g})$$
