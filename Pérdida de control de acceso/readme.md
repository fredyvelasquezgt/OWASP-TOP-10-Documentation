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

- A excepción de los recursos públicos, denegar por defecto.

- Implementar mecanismos de control de acceso una única vez y reutilizarlos en toda la app, incluyendo la minimización del uso de CORS.

- El control de acceso debe implementar su cumplimiento a nivel de datos y no permitir que el usuario pueda crear, leer, actualizar o borrar cualquier dato.

- Los modelos de dominio deben hacer cumplir los requisitos únicos de límite de negocio de aplicaciones.

- Deshabilitar el listado de directorios del servidor web y asegurarse de que los archivos de metadatos (por ejemplo una carpeta .git) y archivos de respaldo no puedan ser accedidos a partir de la raíz del sitio web.

- Registrar las fallas de control de acceso (loggin), alertando a los administradores cuando sea apropiado, por ejemplo, cuando hayan fallas repetidas.

- Establecer límites a la tasa de accesos permitidos a APIs y controladores de forma de poder minimizar el daño provocado por herramientas automatizadas de ataque.

- Los identificadores de sesiones deben invalidarse en el servidor luego de cerrar la sesión. Los tokens JWT deberían de ser preferiblemente de corta duración para minimizar la ventan de oportunidades de ataque. Para JWT de mayor duración, es recomendable seguir los estándares OAuth de revocación de acceso.

> Tanto desarrolladores como personal de control de calidad deben de incluir pruebas funcionales de control de acceso tanto a nivel unitario como de integración.

## Ejemplos de escenarios de ataque

1. La aplicación utiliza datos no verificados en una llamada SQL que accede a información de una cuenta:

```
 pstmt.setString(1, request.getParameter("acct"));
 ResultSet results = pstmt.executeQuery( );
```

Un atacante simplemente modifica el parametro 'acct' en el navegador para enviar el número de cuenta que desee. Si no es verificado correctamente, el atacante puede acceder a la cuenta de cualquier usuario.

`https://example.com/app/accountInfo?acct=notmyacct`

2. Un atacante simplemente navega a un URL especifico. Se deberían de requerir derechos de administrador para acceder a la página de administración.

```
 https://example.com/app/getappInfo
 https://example.com/app/admin_getappInfo
```

Si un usuario no autenticado puede acceder a cualquiera de las páginas, es una falla. Si una persona que no es administrador puede acceder a la página de administración, esto es también una falla.
