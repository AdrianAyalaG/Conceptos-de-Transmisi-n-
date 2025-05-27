# Control de movimiento clase 24/04/2025
# 1. Introducción 
El control de movimiento es una disciplina esencial en ingeniería mecatrónica que combina principios mecánicos, eléctricos y computacionales para lograr posicionamiento preciso en sistemas automatizados, desde maquinaria industrial hasta dispositivos médicos y aeroespaciales. Su diseño requiere no solo la selección adecuada de motores, sino también la optimización de transmisiones mecánicas (como tornillos guía, piñones-cremalleras o bandas transportadoras) para adaptar velocidad, torque e inercia entre el motor y la carga, considerando factores críticos como fricción, backlash y eficiencia. El cálculo de inercias reflejadas mediante ecuaciones, es clave para evitar sobredimensionamiento o inestabilidades dinámicas, mientras que herramientas como Simscape Multibody permiten simular y validar estos sistemas, equilibrando parámetros como la relación de inercia, torque pico y ciclos de trabajo para garantizar eficiencia y confiabilidad en aplicaciones reales.  

# 2. Conceptos de Transmisión 
## 2.1. Tornillo guía
  >🔑 ¿Qué es?: Mecanismo que convierte movimiento rotacional (motor) en lineal (carga). Usado en sistemas de posicionamiento de alta precisión (CNC, impresoras 3D).

foto

### 2.1.1 Tipos de tornillos

* ACME (Rosca): Presentan una eficiencia mecánica del 35-85%, caracterizándose por su bajo costo pero mayor fricción en comparación con otros sistemas. Existen dos configuraciones geométricas principales para sus roscas: cuadrada y trapezoidal. La versión cuadrada, aunque más económica, presenta limitaciones estructurales significativas, particularmente en los flancos de la rosca, donde los picos agudos son susceptibles a fatiga y fractura por cargas cíclicas, lo que compromete su vida útil. En contraste, el diseño trapezoidal ofrece superior resistencia mecánica al distribuir las tensiones de forma más uniforme a lo largo del perfil de la rosca, minimizando la concentración de esfuerzos. Esta ventaja estructural aunque no reduce el riesgo de fallo a futuro, garantiza un movimiento más suave y estable de la bandeja o cama, especialmente en aplicaciones con altas cargas dinámicas o ciclos de trabajo continuos.
  
* Tornillos de Esferas (Ball Screws): Eficiencias del 85-95% en tornillos de bolas (vs 35-85% en ACME), menor fricción gracias al contacto rodante, y backlash reducido que garantiza posicionamiento preciso. Es importante tener en cuenta que el backlash es un problema asociado a un fenómeno de torsión, durante el cual, por un instante, no se transmite la fuerza de manera efectiva debido a una discontinuidad o juego en la cadena cinemática.

foto

### 2.1.2 Relación de Transmisión 
* Paso (Lead): Distancia lineal por revolución, en otras palabras, es la relación de cuanto se mueve la capsula cuando el tornillo de una vuelta
* Cabeceo (Pitch): Revoluciones por metro lineal, en otras palabras, es el número de revoluciones que debe tener el tornillo para que la capsula se desplace 1 metro.

Para entender la relación entre el desplazamiento angular del tornillo y el desplazamiento lineal de la capsula (Carriage), se tienen las siguientes ecuaciones: 

$$\Delta\theta= 2\pi(p)\Delta(x)$$



### 2.1.3 Simulink Matlab Multibody

imagen
gif 

## 2.2 Sistema Piñón - Cremallera
>🔑 ¿Qué es?: Mecanismo que convierte movimiento rotacional (piñón) en lineal (cremallera) mediante engrane directo. La cremallera casi siempre es metálica para soportar cargas pesadas y es por ello, que este tipo de transmisión es ideal para aplicaciones que requieren precisión y fuerza en ejes lineales.

foto

### 2.2.1 Relación de Transmisión 
>🔑 ¿Qué es?: Define cómo la velocidad angular del piñón $$w_{pinion}$$ se traduce en velocidad lineal de la cremallera $$V_{rack}$$

$$N = \frac{w_{motor}}{v_{rack}}$$ 

Escrito de otra manera y solo si se están tratando velocidades en rad/segundos:

$$N_{RP}= \frac{1}{r_{pinion}}$$

$$V_{rack}= r_{pinion} * w_{pinion}$$

Donde $$r_{pinion}$$ será el radio del piñón. 

### 2.2.2 Inercia reflejada
>🔑 ¿Qué es?: Inercia equivalente "vista" por el motor:

Cómo formula matemática sería: Inercia del Piñón + Inercia de la carga + Inercia del carro 

$$J_{ref} = J_{pinion}+\frac{1}{\eta N^{2}}(\frac{W_{L}+W_{C}}{g})$$

* η: Eficiencia (típicamente 0.8 - 0.9 para buena eficiencia en el sistema; = 1 en ideal).
* $$W_{C}$$ es el peso de la cremallera
* La inercia del piñón $$J_{pinion}$$ se da en unidades de $$Kg*m^2$$

### 2.2.3 Torque reflejado
>🔑 ¿Qué es?: Torque que el motor debe generar para superar todas las fuerzas externas que se oponen al movimiento del sistema.

$$T_{load\to in}=\frac{F_{ext}}{\eta N_{RP}}$$

* Donde $$F_{ext}$$ es la suma de todas las fuerzas externas y $$N_{RP}$$ la relación de transmisión adimensional. Es fundamental identificar qué elementos deben reflejarse en una ecuación de este porte, y estos corresponden a lo que se encuentra al otro lado de la transformación de energía.

* Entre las observaciones más importantes de este sistema, cabe recalcar que a nivel estructural, requiere una correcta lubricación y mantenimiento para evitar desgaste prematuro por contacto constante, y una buena alineación para resistir adecuadamente las cargas radiales y axiales.
  
## 2.3 Banda transoortadora 
>🔑 ¿Qué es?: Sistema que transmite movimiento mediante poleas y una banda continua, usado en transporte de materiales, líneas de ensamblaje o producción, clasificación y distribucion de productos. 

### 2.3.1 Relación de transmisión (Poleas iguales) 

$$N_{BD}= \frac{1}{R_{IP}}; V_{belt}= r_{IP}* w_{IP}$$

$$r_{IP}$$ Es el radio de la polea de entrada, es decir, la que es motriz. 

### 2.3.2 Inercia reflejada
Considera inercias de poleas (2 poleas existentes en el sistema), de la banda, la carga y el carro.

$$J_{ref} = \color{Red} 2J_{p}\color{Yellow} +\frac{1}{\eta N^{2}}(\frac{W_{L}+W_{C}+W_{Belt}}{g})$$

* La inercia en las dos poleas se toman como si fueran valores iguales y este valor NO se refleja. La parte amarilla se refleja totalmente. 

### 2.3.3 Torque de carga 
Se presenta igual que con el tornillo guia y el sistema piñón-cremallera 

$$T_{load\to in}=\frac{F_{ext}}{\eta N_{BD}}$$

# 3. Conclusiones 
La transmisión en un tornillo sin fin, determinada por el número de hilos del tornillo y los dientes de la rueda, permite alcanzar grandes reducciones en un solo paso, siendo especialmente adecuada para sistemas de alta carga y baja velocidad; sin embargo, cuando se requiere transformar el movimiento rotacional en lineal con mayor precisión y eficiencia, mecanismos como el husillo de bolas ofrecen ventajas notables, ya que, a diferencia de la rosca directa, reducen la fricción mediante la recirculación de bolas, lo que mejora significativamente la vida útil, la precisión y la eficiencia, aunque a costa de una mayor complejidad y precio. Por otro lado, el sistema piñón-cremallera también convierte el movimiento rotativo en lineal, pero a través de una relación directa entre la velocidad angular del piñón y la velocidad lineal de la cremallera, lo cual lo hace más adecuado para trayectorias largas y repetitivas, a diferencia del tornillo, que se emplea comúnmente en recorridos más cortos y con mayor necesidad de precisión. En cuanto a los parámetros del tornillo, el paso y el cabeceo son esenciales para entender el desplazamiento por vuelta, ya que su relación inversa permite obtener movimientos lineales más o menos rápidos según se requiera, lo cual tiene implicaciones directas en la inercia reflejada al motor: un mayor paso reduce dicha inercia, mejorando la respuesta dinámica del sistema, aunque puede comprometer la precisión en aplicaciones de control fino. Esta inercia reflejada es un concepto clave en el modelado de sistemas mecatrónicos, ya que permite representar todos los elementos en un único dominio, rotacional o lineal, lo cual simplifica el análisis y el diseño de controladores. Finalmente, en mecanismos como bandas transportadoras con múltiples rodillos, aunque la velocidad lineal de la banda permanece constante, las velocidades angulares de los rodillos varían según sus radios, lo que, al igual que en los demás sistemas mencionados, exige una cuidadosa sincronización para garantizar un funcionamiento armónico y eficiente.

# 4. Referencias 
