# CAP 1
## Qué es un sistema distribuido? 🤔
> Un sistema distribuido es una colección de elementos de computo autónomos que parecen a sus usuarios como un único sistema coherente.

La definición hace referencia a 2 características de los *SD* (Sistemas Distribuidos).

1. Colección de **elementos de computo**: Un elemento de computo autónomo (capaz de comportarse independientemente uno del otro), el cual nos referiremos como **nodo** generalmente, puede ser un dispositivo de harware o un proceso de software.
2. Los usuarios: pueden ser personas o aplicaciones, creen estar tratando con un **único sistema**.

## Sistemas distribuidos y Middleware
Para asistir el desarrollo de aplicaciones distribuidas, los SD son organizados para tener **una capa de software** que es lógicamente ubicada sobre los respectivos sistemas operativos de las computadoras que son parte del sistema.
Lo que es conocido como **middleware**.

Los Middleware son un **administrador de recursos** que ofrece sus aplicaciones para compartir e implementar eficientemente estos recursos a través de la red. Los servicios que ofrecen son:
  - Facilidades para la comunicación entre aplicaciones.
  - Servicios de seguridad.
  - Servicios de contabilidad.
  - Enmascaramiento y recuperación de fallas.

Son ofrecidos en un entorno en red y pueden ser vistos como un **contenedor** de funciones y componentes de uso común que ya no tiene que ser implementado por aplicaciones por separado.
- Algunos servicios de middleware:
  - **Comunicación**.
  - **Transacción**.
  - **Composición del servicios**.
  - **Fiabilidad**.