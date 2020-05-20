# CAP 1
## Intro
### Un poco historia ⌛
- Desde 1945 hasta 1985, las computadoras eran grandes, caras y operaban de forma independiente una de otra.
- A mediados de los 80' 2 avances tecnológicos cambiaron la situación.
  - Desarrollo de microprocesadores potentes.
  - Redes de computadoras de alta velocidad.
- Paralelo a estos avances, se han hecho computadoras mas chicas con gran capacidad de computo(smartphones).
- El resultado de estas tecnologías es que es factible y fácil poner juntos sistemas de computación compuestos de miles de computadoras conectadas. Generalmente son dispersas geográficamente, por esta razón se le dice formar **sistemas distribuidos**.
- Los sistemas distribuidos varían de tamaño y son dinámicos, en el sentido las computadoras pueden unirse o dejar, con la topología y rendimiento de la red cambiando continuamente.

### Qué es un sistema distribuido? 🤔
> Un sistema distribuido es una colección de elementos de computo autónomos que parecen a sus usuarios como un único sistema coherente.

La definición hace referencia a 2 características de los *SD* (Sistemas Distribuidos).

1. Colección de **elementos de computo**: Un elemento de computo autónomo (capaz de comportarse independientemente uno del otro), el cual nos referiremos como **nodo** generalmente, puede ser un dispositivo de harware o un proceso de software.
2. Los usuarios: pueden ser personas o aplicaciones, creen estar tratando con un **único sistema**.

Esto significa que los nodos necesitan colaborar. Cómo establecer esa colaboración yace en el corazón del desarrollo de los sistemas distribuidos. 💓

#### Característica 1: Colección de elementos de computación autónomos
- Consiste de todo tipos de nodos, desde computadoras de alto rendimiento hasta pequeñas computadoras o incluso dispositivos mas pequeños, también procesos de software pueden ser nodos.
- Actúan independientemente uno del otro.
- Cada nodo esta programado para lograr objetivos en común, intercambiando mensajes entre ellos.
- La consecuencia de trabajar con nodos independientes es cada uno tiene su propia **noción del tiempo**, esto genera preguntas respecto a la **sincronización y coordinación** en un SD.
- El hecho de trabajar con una colección de nodos implica manejar la **afiliación y organización** de esa colección. En otras palabras, registrar qué nodos pertenecen al sistema, y proporcionar a cada miembro una lista de los nodos con los que se puede comunicar.
- Gestionar la **pertenencia a un grupo** puede ser extremadamente difícil, aunque solo sea por razones de control de admisión, por ejemplo, un mecanismo que controle a un nodo en unirse o dejar un grupo.
  1. Un mecanismo así es necesario para autenticar al nodo, si esto no es apropiadamente diseñado puede crear un cuello de botella de escalabilidad.
  2. Cada nodo debe verificar si se está comunicando con otro miembro del grupo o no.
  3. Considerando que cada miembro puede comunicarse fácilmente con no miembros podemos enfrentar problemas de confianza si la confiabilidad es un problema dentro del SD.

- Sobre la **organización de la colección**, la práctica muestra que los SD a menudo son organizados como una **red superpuesta** (overlay network [Tarkoma,2010]). En este caso un nodo es típicamente un proceso de software equipado con una lista de procesos a los que puede enviar mensajes. Puede darse el caso que el vecino tenga que ser consultado primero. El pase de mensajes se hace a través de canales TCT/IP o UDP, pero como veremos más adelante, facilidades de más alto nivel pueden estar disponibles.
- Existe 2 tipos de redes superpuestas:
  1. **Superpuesta estructurada** (Structured Overlay): Cada nodo tiene definido el conjunto de vecinos para comunicarse. Por ejemplo, son organizados en un árbol o anillo lógico.
  2. **Superpuesta no estructurada** (Unstructured Overlay): Cada nodo tiene un número de referencias aleatorias seleccionadas a otros nodos.

- Una red superpuesta siempre debe estar **conectada**.
- Una clase conocida de superposiciones está formada por redes punto a punto (P2P).
- Es importante darse cuenta de que la organización de nodos requiere un esfuerzo especial y que a veces es una de las partes más complejas de la administración de sistemas distribuidos.

#### Característica 2: Único sistema coherente
- Un SD debe parecer como un único sistema coherente.
- Algunos investigares van más allá, diciendo que debe ser una vista de sistema único.
- **Vista de sistema único**: significa que los usuarios finales no deben darse cuenta que están lidiando con el hecho que los procesos, los datos y el control están dispersos en una red informática.
- A menudo esto es pedir demasiado, por lo cual se optó por algo más tenue, que es que debe parecer **coherente**.
- Más o menos, un SD es coherente cuando se comporta de acuerdo a las expectativas de sus usuarios.
- Más específicamente, en un único sistema coherente la colección de nodos como un todo operan igual, no importa dónde, cuándo, y cómo interactúan entre sistema y usuario.

#### Sistemas distribuidos y Middleware
Para asistir el desarrollo de aplicaciones distribuidas, los SD son organizados para tener **una capa de software** que es lógicamente ubicada sobre los respectivos sistemas operativos de las computadoras que son parte del sistema.
Lo que es conocido como **middleware**.

- Middleware es lo mismo para un sistema distribuido como lo que es un sistema operativo para una computadora: un **administrador de recursos** que ofrece sus aplicaciones para compartir e implementar eficientemente estos recursos a través de la red.
- Junto a la gestión de recursos, ofrece servicios que son encontrados en la mayoría de sistemas operativos:
  - Facilidades para la comunicación entre aplicaciones.
  - Servicios de seguridad.
  - Servicios de contabilidad.
  - Enmascaramiento y recuperación de fallas.

- La diferencia con el sistema operativo, es que los servicios de middleware son ofrecidos en un entorno en red.
- Note también que la mayoría de servicios son útiles para varías aplicaciones. Por lo que el middleware puede ser visto como un **contenedor** de funciones y componentes de uso común que ya no tiene que ser implementado por aplicaciones por separado.
- Algunos servicios de middleware:
  - **Comunicación**: Uno común es el llamado **Llamada al procedimiento remoto** (RPC). Permite a una app invocar una función que es implementada y ejecutada en una computadora remota como si fuera localmente disponible.
  - **Transacción**:
  - **Composición del servicio**:
  - **Fiabilidad**:

### Objetivos de diseño

Solo porque se puede no significa que sea buena idea construir un sistema distribuido. 4 objetivos se tienen que dar para que valga la pena el esfuerzo. Un sistema distribuido debe:
  - Hacer los recursos fáciles de acceder.
  - Ocultar el hecho que los recursos están distribuidos en la red.
  - Ser abiertos.
  - Ser escalables.

#### Apoyando el intercambio de recursos
El objetivo es hacer fácil para los usuarios (y aplicaciones) acceder y compartir recursos remoto. Las razones pueden ser tanto desde lo económico hasta como conectar usuarios y recursos hace más fácil colaborar e intercambiar información.

#### Haciendo transparente la distribución
Otro objetivo es ocultar el hecho que los procesos y recursos son físicamente distribuidos. En otras palabras intenta hacerlo transparente al usuario final y aplicaciones.

Tipos de transparencias:
- **Acceso**: Oculta las diferencias de representación de datos y cómo un objeto es accedido.
- **Ubicación**: Oculta dónde un objeto es ubicado.
- **Re-ubicación**: Oculta que un objeto puede ser movido a otro ubicación mientras esta en uso.
- **Migración**: Oculta que un objeto puede moverse a otra ubicación.
- **Replicación**: Oculta que un objeto es replicado.
- **Concurrencia**: Oculta que un objeto puede ser compartido por varios usuarios independientes.
- **Fallo**: Oculta el fallo y recuperación de un objeto.

*Objeto puede ser un proceso o recurso.

Si bien es preferible la transparencia, no es buena idea intentar dejar a ciegas al usuario de todos los aspectos de distribución. Apuntar a la transparencia de distribución puede ser un buen objetivo al diseñar e implementar sistemas distribuidos, pero que debe considerarse junto con otros temas como el **rendimiento** y la **comprensión**. El precio para lograr la transparencia total puede ser sorprendentemente alto.

#### Ser abierto
Un sistema distribuido abierto es esencialmente un sistema que ofrece componentes que pueden ser fácilmente usados o integrados dentro de otro sistema. A menudo, un sistema distribuido abierto en sí consistirá de componentes que se originan en otro lugar.

##### Interoperabilidad, componibilidad, y extensibilidad

Para ser abierto los componentes deben adherirse a reglas estándares que describen las **sintaxis** y **semántica** de lo que ellos ofrecen (ej. qué servicio proporcionan). Un enfoque general es definir servicios a través de **interfaces** usando un lenguaje de definición de interfaz (IDL). Una definición de interfaz escrita con un IDL solamente captura la sintaxis del servicio. La semántica es dada por medio del lenguaje natural.

Las especificaciones adecuadas son *completas* y *neutrales*. Estas son importantes para la **interoperabilidad** y **portabilidad**.

- **Interoperabilidad**: grado de coexistencia y trabajo en conjunto de 2 sistemas o componentes de diferente fabricante, solo confiando es sus interfaces.
- **Portabilidad**: hasta qué punto una app para un sistema distribuido A puede ejecutarse, sin modificaciones, en uno B con las mismas interfaces.
- **Extensibilidad**: fácil configuración de diferentes componentes, agregar y sacar componentes sin afectar al resto del sistema.

##### Separar la política del mecanismo
Para lograr flexibilidad en sistemas distribuidos abiertos, es clave organizar el sistema como una colección de componentes pequeños, reemplazables y adaptables. Esto implica no solo dar definiciones de interfaces de alto nivel (para usuarios y apps), sino también para las partes internas del sistema y cómo se conectan.

La necesidad de cambiar un sistema distribuido a menudo es por un componente que no da una política óptima para un usuario o app específico.