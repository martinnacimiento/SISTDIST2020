- [Introducción a los sistemas distribuidos](#introducci%c3%b3n-a-los-sistemas-distribuidos)
- [Ventajas de los sistemas distribuidos con respecto a los centralizados](#ventajas-de-los-sistemas-distribuidos-con-respecto-a-los-centralizados)
- [Ventajas de los sistemas distribuidos con respecto a las PC independientes](#ventajas-de-los-sistemas-distribuidos-con-respecto-a-las-pc-independientes)
- [Desventaja de los sistemas distribuidos](#desventaja-de-los-sistemas-distribuidos)
- [Conceptos de hardware](#conceptos-de-hardware)
  - [Taxonomía de Flynn](#taxonom%c3%ada-de-flynn)
  - [Fuentes de apoyo del apartado](#fuentes-de-apoyo-del-apartado)
- [Multiprocesadores con base en buses](#multiprocesadores-con-base-en-buses)
  - [Características generales](#caracter%c3%adsticas-generales)
  - [Problema](#problema)
    - [El cache, la solución](#el-cache-la-soluci%c3%b3n)
  - [El cache y sus problemas](#el-cache-y-sus-problemas)
    - [Solucionando la incoherencia de memoria](#solucionando-la-incoherencia-de-memoria)
      - [Cache de escritura](#cache-de-escritura)
      - [Cache de monitor](#cache-de-monitor)
- [Multiprocesadores con conmutador](#multiprocesadores-con-conmutador)
  - [Conmutador de cruceta](#conmutador-de-cruceta)
    - [Virtudes](#virtudes)
    - [Debilidades](#debilidades)
  - [Red Omega](#red-omega)

# Introducción a los sistemas distribuidos
- Desde 1945 hasta 1985 solo se conocía **computación centralizada**.
- A mitad de los 80's 2 surgen avances tecnológicos:
  - Microprocesadores.
  - Redes LAN de alta velocidad.
- Surgen los sistemas distribuidos, el cual necesita un software diferente al de los centralizados.
- Los SO para sistemas distribuidos han tenido importantes desarrollos, pero todavía hay un largo camino que recorrer.
- Los usuarios pueden acceder a una gran variedad de recursos computacionales de hardware y software distribuidos entre un gran número de sistemas computacionales conectados.
- ARPANET (iniciada 1968 en EEUU) constituye un gran antecedente de las redes de computadoras.

# Ventajas de los sistemas distribuidos con respecto a los centralizados
- Los sistemas distribuidos generalmente tienen en potencia una proporción **precio/desempeño** mejor que uno centralizado.
- Mayor **confiabilidad** al distribuir la carga de trabajo en muchas máquinas, la falla de una no afecta a las demás.
- Posibilidad de **crecimiento incremental**. Agregar procesadores al sistema gradualmente según las necesidades. No es necesario grandes incrementos en breves lapsos de tiempo.

# Ventajas de los sistemas distribuidos con respecto a las PC independientes
- Satisfacen la necesidad de usuarios de compartir información.
- Compartición de otros recursos como programas y periféricos costosos.
- Lograr mejor comunicación entre personas.
- Mayor flexibilidad, carga de trabajo distribuida entre maquinas disponibles en la forma más eficaz según el criterio adoptado.

# Desventaja de los sistemas distribuidos
- El principal problema es el software, es complejo de diseñar e implementar.
- Principales interrogantes:
  - Qué SO, lenguaje de programación y aplicaciones son adecuados para estos sistemas?
  - Cuánto deben saber los usuarios de la distribución?
  - Qué tanto debe hacer el sistema y qué tanto los usuarios?
- La respuesta a estas interrogantes no es uniforme entre los especialistas:
  - Existen muchos criterios y de interpretaciones.
- Las redes de comunicaciones se deben considerar perdidas de mensajes, saturación en el tráfico, expansión, etc.
- La organización de todos los nodos en el sistema.
- En general se considera que las ventajas superan a las desventajas, si estas últimas se administran seriamente.

# Conceptos de hardware
- Todos los sistemas distribuidos constan de varias CPU organizadas de diversas formas, especialmente respecto de:
  - La forma de **interconectarlas** entre sí.
  - Los **esquemas de comunicación** utilizados.

Existen diversos esquemas de clasificación
## Taxonomía de Flynn
Considera como características esenciales el número de flujo de instrucciones y el de flujos de datos.
- La clasificación incluye equipos SISD, SIMD, MISD, Y MIMD.
  - SISD (Single Instruction Single Data):
    - Poseen un procesador.
  - SIMD (Single Instruction Multiple Data):
    - Ordenar procesadores con una unidad de instrucción que busca una instrucción e instruye a varias unidades de datos para que la lleven en paralelo.
    - Son utiles para los computos que repiten los mismos calculos en varios conjuntos de datos.
  - MISD (Multiple Instruction Single Data):
    - No se presenta en la practica.
  - MIMD (Múltiple Instruction Multiple Data):
    - Todos los sistemas distribuidos son de este tipo.
- Un avance sobre la clasificación de flynn incluye al división de MIMD en 2:
  - **Multiprocesadores**: poseen memoria compartida. Las distintos procesadores comparten el mismo espacio de direcciones virtuales.
  - **Multicomputadoras**: no poseen memoria compartida. Ej: grupo de PC conectadas mediante una red.
- Cada una de estas categorías se puede clasificar según la **arquitectura de la red de interconexión**:
  - **Esquema de bus**:
    - Existe una sola red, bus, cable u otro medio que conecta a todas la máquinas.
  - **Esquema con conmutador**: no existe una sola columna vertebral de conexión.
    - Hay múltiples conexiones y varios patrones de conexionado.
    - Los mensajes pasan por los medios de conexión.
    - Se decide explícitamente la conmutación en cada etapa para dirigir el mensaje.
- Otro aspecto de la clasificación es el **acoplamiento** entre equipos:
  - **Fuertemente acoplados**:
    - Retraso de mensajes entre máquinas corto y la tasa de transmisión alta.
    - Generalmente se los utiliza como **sistemas paralelo**.
  - **Débilmente acoplados**:
    - Retraso de los mensajes entre máquinas grande y la tasa de transmisión es baja.
    - Generalmente se los utiliza como **sistemas distribuidos**
- Generalmente los multiprocesadores están más fuertemente acoplados.

## Fuentes de apoyo del apartado
- [Taxonomía de Flynn](https://es.wikipedia.org/wiki/Taxonom%C3%ADa_de_Flynn)
- [Concepto de multiprocesador](https://es.wikipedia.org/wiki/Multiprocesador)
- [CPU](https://es.wikipedia.org/wiki/Unidad_central_de_procesamiento)

# Multiprocesadores con base en buses
## Características generales
- Consta de cierto número de CPU conectadas a un bus común, junto con un módulo de memoria.
- Un bus típico posee al menos:
  - 32 líneas de direcciones.
  - 32 líneas de datos.
  - 30 líneas de control.
- Todos los elementos precedentes operan en paralelo.
- Para **leer** una palabra de memoria, una cpu:
  - Coloca la dirección de la palabra deseada en las líneas de dirección del bus.
  - Coloca una señal en la líneas de control adecuadas para indicar que se desea leer.
  - La memoria responde y coloca el valor de la palabra en las lineas de datos para permitir la lectura por parte de la CPU solicitante.
- Para **grabar** el procedimiento es similar.
- Solo existe **una memoria**, la cual presenta la propiedad de la **coherencia**:
  - Las modificaciones hechas por una CPU se reflejan de inmediato en la subsiguientes lecturas de la misma o de otra CPU.
## Problema
El **problema** de este esquema es que el bus tiende a sobrecargarse y el rendimiento a disminuir drásticamente.
### El cache, la solución
La solución es agregar una **memoria cache** entre la cpu y el bus:
  - El cache guarda la palabras de acceso reciente.
  - Todas las solicitudes de la memoria pasan a través del cache.
  - Si la palabra solicitada se encuentra en el cache:
    - El cache responde a la cpu.
    - No se hace solicitud alguna al bus.
  - Si el cache es bastante grande.
    - La tasa de encuentros sera alta y la cantidad de trafico en el bus por cada cpu disminuirá drásticamente y esto permite incrementar el número de CPU.
## El cache y sus problemas
El cache trae un nuevo problema, la **incoherencia de la memoria**:
  - Supongamos que las CPU A y B leen la misma palabra de memoria en sus respectivos caches.
  - A escribe sobre la palabra.
  - Cuando B lee esa palabra, obtiene un valor anterior y no el valor actualizado por A.
### Solucionando la incoherencia de memoria
#### Cache de escritura
- La solución a esto consiste en diseñar las cache de tal forma que cuando la palabra sea escrita al cache, también sea escrita a la memoria. Se denomina **cache de escritura**. Causa trafico en el bus en escritura y cuando no encuentra lo solicitado en cache únicamente.
#### Cache de monitor
- Otra solución es si todos los caches realizan un monitoreo constante del bus:
  - Cada vez que se observe una escritura a una dirección de memoria presente en el mismo puede eliminar o actualizar en el cache con el nuevo valor.
  - Estos se denominan **caches monitores**.
- Un diseño con caches de monitores y de escritura es coherente e invisible para el programador, es muy utilizado en multiprocesadores basados en buses.

# Multiprocesadores con conmutador
El esquema anterior resulta apropiado para hasta aproximadamente 64 procesadores. Para superar esta cifra es necesario un método distinto de conexión entre procesadores (CPU) y memoria.

## Conmutador de cruceta
Una posibilidad es dividir la memoria en módulos y conectarlos a la cpu con un conmutador de cruceta (cross-bar switch):
- Cada CPU y cada memoria tiene una conexión que sale de el.
- En cada intersección esta un conmutador del **punto de cruce** (crosspoint switch) electrónico que el hardware puede abrir o cerrar.
  - cuando una cpu desea tener acceso a una memoria particular, el conmutador del punto de cruce que los conecta se cierra momentáneamente.

### Virtudes
- Muchas CPU pueden tener acceso a la memoria al mismo tiempo, aunque no a la misma simultáneamente.

### Debilidades
- Alto número de conmutadores, para $n$ CPU y $n$ memorias se necesitan $n$ X $n$ conmutadores.

## Red Omega
El número de conmutadores del anterior esquema puede resultar prohibitivo, otros esquemas precisan menos conmutadores como la red omega:
- Posee conmutadores 2 X 2:
  - C/U tiene 2 entradas y 2 salidas.
  - C/U puede dirigir cualquiera de las entradas a cualquiera de la salidas.
  - Eligiendo los estados adecuados de los conmutadores, cada CPU podrá tener acceso a cada memoria.
  - Para cada $n$ CPU y $n$ memorias se precisan:
    - $n$ etapas de conmutación.
    - cada etapa tiene $log_2n$ conmutadores para un total de $nlog_2n$ conmutadores:
      - Este número es menor que $n$ X $n$ del esquema anterior, pero sigue siendo muy grande para $n$ grande.