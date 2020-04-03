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
2. Los **usuarios**: pueden ser personas o aplicaciones, creen estar tratando con un único sistema.

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
