# Pérdida de control de acceso

## Definición

El control de acceso implementa el cumplimiento de políticas de modo que los usuarios no puedan actuar fuera de los permisos que les fueron asignados. Las fallas del control de acceso conducen a que la información se divulgue de forma no autorizada, a su vez, también existe el caso en el que la información sea modificada o destruida. De la misma forma, la ejecución de una función restringida solo para el negocio puede ser perjudicada.

## Vulnerabilidades comunes de control de acceso

- Violación del principio de mínimo privilegio o denegación por defecto, según el cual el acceso solo debe de ser permitido para capacidades, roles o usuarios particulares, y no dispoible para cualquier persona.

- Eludir las comprobaciones de control de acceso modificando la URL (alteración de parámetros o navegación forzada), el estado interno de la aplicación o la página HTML, o mediante el uso de una herramienta que modifique los pedidos a APIs.

- Permitir ver o editar la cuenta de otra persona, con tan solo conocer su identificador único (referencia directo insegura a objetos)

- Acceder a APIs con controles de acceso inexistentes para los métodos POST, PUT y DELETE.

- Elevación de privilegios. Actuar como usuario sin haber iniciado sesión o actuar o actuar como administrador cuando se inició sesión como usuario regular.

- Manipulación de metadatos, como reutilizar o modificar un token de control de acceso JSON Web Token, una cookie o un campo oculto, manipulándolos para elevar privilegios o abusar de la invalidación de JWTs.

- Configuraciones incorrectas de CORS (uso compartido de recursos de origen cruzado) que permiten el acceso a APIs dedsde orígenes no autorizados o confiables.

- Forzar la navegación a páginas autenticadas siendo usuario no autenticado o a páginas privilegiadas siendo usuario regular.

## Cómo se previene

El control de acceso solo es efectivo si es implementado en el servidor (server-side) o en la API (caso serverless), donde el atacante no puede modificarlo ni manipular metadatos.

### Más soluciones
