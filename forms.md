# Reto de Formularios

## Descripción

El reto consiste en crear formularios utilizando el stack de desarrollo web de tu preferencia. El objetivo es practicar la creación de formularios, validaciones, seguridad y manejo de datos en el backend.

Cada formulario debe incluir validaciones, gestión de errores, mensajes de éxito o fallo para la usabilidad, y medidas de seguridad contra ataques como CSRF y XSS. Se recomienda usar Regex, tokens CSRF y Captcha.

Recuerda guardar tu progreso en un repositorio de Git, así tendrás disponible el código que has creado para usarlo en tus proyectos o mostrarlo como evidencia de tu conocimiento.

**Ten en cuenta que para los retos adicionales es preferible que no modifiques el formulario original.** Copia el formulario o crea una nueva rama de git y trabajar en una versión alternativa.

Todo lo descrito aquí es requerido en el mundo real pero **si en algún momento piensas "esto está muy difícil", toma un respiro** y analízalo desde otras perspectivas. Si no te sale a la primera, no te preocupes, La idea es que aprendas y practiques.

## Reto de Super Saiyajin fase 1: Envío de datos

![ssj1](https://static.wikia.nocookie.net/dragonball/images/2/2b/Goku_transforms_into_a_Super_Saiyan_for_the_first_time_%28Full_Color_Manga%29.png/revision/latest/scale-to-width/200)

Crea un formulario de contactos con los campos `email` y `name`.  
Envía los datos en formato `application/json`.  
Guarda los datos en el servidor.  
Devuelve una respuesta indicando si la operación fue exitosa.  

**Recomendaciones:**
- Los campos requeridos no deben estar vacíos.
- Valida el formato de los datos, longitud y caracteres permitidos.
    - ¿El correo debería permitir más de un "@" o más de un "."?
    - ¿El nombre debería permitir emojis, caracteres chinos o caracteres invisibles?.
- Ten en cuenta el charset de los datos.
- Cuidado los espacios en blanco al inicio y al final. También con los datos que son sólo espacios en blanco.

**Reto adicional:**  
Valida que el `email` sea único en toda tu base de datos de contactos.

**Reto adicional:**  
Agrega un campo opcional `notes` para permitir al usuario ingresar notas adicionales.  
El campo `notes` debe permitir saltos de línea y caracteres especiales pero protégete contra ataques XSS y caracteres invisibles.  

## Reto de Super Saiyajin fase 2: Formulario con archivo multimedia

![ssj2](https://static.wikia.nocookie.net/dragonball/images/5/56/Nhaca.jpg/revision/latest/scale-to-width-down/300)

Crea un formulario con un campo `file` para cargar una imagen.  
Valida el tipo de archivo y el tamaño máximo permitido.  
Envía los datos en formato `multipart/form-data`.  
Guarda el archivo en el servidor.  
Devuelve una respuesta indicando si la carga fue exitosa.  
Si fue exitosa, devuelve la URL del archivo.  

**Reto adicional:**  
Renombra los archivos cargados para evitar colisiones. Es decir, si el usuario carga un archivo con el mismo nombre, no lo sobrescribas.

**Reto adicional:**  
Permite la carga de múltiples imágenes en el mismo campo.  
Devuelve una lista con las URLs de los archivos cargados.  

## Reto de Super Saiyajin fase 3: Formulario con archivo de datos

![ssj3](https://static.wikia.nocookie.net/dragonball/images/8/82/SS3_FCM.png/revision/latest/scale-to-width-down/200)

Crea un formulario con un campo `file` para cargar un archivo CSV.  
Valida el tipo de archivo y el tamaño máximo permitido.  
Envía los datos en formato `multipart/form-data`.  
Procesa el archivo y almacena los datos en el servidor.  
Valida el encabezado del CSV contra una estructura esperada antes de procesarlo.  
Devuelve una respuesta indicando si la carga fue exitosa.  
Si fue exitosa, indica cuántas filas se procesaron correctamente.  

**Reto adicional:**  
Permite la carga de múltiples archivos CSV en el mismo campo. Devuelve la cantidad de filas procesadas por cada archivo.  

**Reto adicional:**  
Procesa el archivo CSV usando iteradores en el servidor.  

**Reto adicional:**  
Agrega un campo requerido `secure` en forma de checkbox para el manejo de errores.  

Si el checkbox `secure` está marcado:
- Cuando el procesamiento del archivo CSV falla, devuelve un mensaje de error indicando la fila y la columna donde ocurrió el error.
- Revierte los datos procesados hasta el momento.

Si el checkbox `secure` no está marcado:
- Cuando el procesamiento del archivo CSV falla, acumula los errores pero almacena los datos correctos.
- Devuelve un mensaje de error indicando la lista de filas y columnas donde ocurrieron los errores, así como la cantidad de filas procesadas correctamente.

**Reto adicional:**  
Permite que el usuario descargue todos los contactos creados en un archivo CSV.  
Usa `Transfer-Encoding: chunked` en la respuesta para enviar el archivo de manera incremental.  

**Reto adicional:**  
Permite que el usuario descargue todos los contactos creados en un archivo CSV.  
Durante la descarga, guarda el archivo en el servidor en forma de cache.  
Si el usuario vuelve a descargar los contactos creados, devuelve el archivo guardado en el servidor hasta que se envíe un nuevo archivo CSV que se procese correctamente guardando nuevos contactos.  

## Reto de Super Saiyajin God: Formularios dinámicos

![ssjGod](https://static.wikia.nocookie.net/dragonball/images/6/68/SSG_profile1.png/revision/latest/scale-to-width-down/200)

Crea un formulario de contactos con conjuntos dinámicos de campos.
Incluye en cada conjunto los campos `email` y `name`.  
Permite agregar, actualizar y eliminar conjuntos de campos.  
Envía los datos en formato `application/json`.  
Devuelve una respuesta indicando si la operación fue exitosa.  

**Al cargar la página del formulario:**

- Muestra los contactos existentes.  
- Si no hay contactos, muestra solo la opción para agregar uno nuevo.  

**Al eliminar un contacto:**
- Muestra un mensaje de confirmación antes de eliminarlo.

**Al presionar "Enviar":**

- Guarda los contactos nuevos que el usuario haya agregado.  
- Actualiza los contactos que el usuario haya editado.  
- Elimina los contactos que el usuario haya marcado para eliminar.  

**Ejemplo conceptual de formset:**

![ejemplo de formset](https://whoisnicoleharris.com/assets/img/formset-animation.gif)

**Reto adicional:**  
Los **contactos existentes** eliminados por el usuario deben seguir siendo visibles pero no editables.  
El botón de "Eliminar" para los contactos existentes eliminados debe cambiar a "Restaurar".  
Si el usuario presiona "Restaurar", el contacto debe volver a ser editable y el botón de "Restaurar" debe cambiar al de "Eliminar".  
Los **nuevos contactos** que el usuario haya agregado y eliminado en el mismo formulario deben eliminarse completamente tras la confirmación.  

**Reto adicional:**  
Implementa reordenamiento de contactos.  
Al crear un nuevo contacto, el usuario puede moverlo a una posición diferente.  
Ten en cuenta que el usuario puede eliminar contactos y el orden debe actualizarse.  
Al cargar la página del formulario, los contactos existentes deben mostrarse en el orden correcto.  

**Reto adicional:**  
Implementa formularios dinámicos anidados.  
Incluye un formulario dinámico de etiquetas en cada conjunto de campos que representa a un contacto.  
Al agregar un nuevo contacto, junto a los campos de información del contacto, agrega un formulario dinámico de etiquetas.  
Valida que cada etiqueta sea una única palabra sin espacios ni símbolos.  
El usuario **puede agregar y eliminar etiquetas** pero no actualizar las etiquetas existentes.  
Si el usuario agrega el mismo texto en varias etiquetas del mismo contacto, sólo se debe guardar una vez.  
Al cargar la página del formulario, para los contactos existentes, muestra las etiquetas en el contacto correspondiente y en orden alfabético.  

**Reto adicional:**  
Agrega un campo opcional `avatar` para cargar una imagen asociada a cada contacto.  
Valida el tipo de archivo y el tamaño máximo permitido.  
Envía los datos del formulario en formato `multipart/form-data`.  
Muestra la imagen correspondiente (no la URL) al cargar la página del formulario si el contacto ya existe.  
Guarda la nueva imagen si el usuario la reemplaza en un contacto existente.  
Mantén la imagen anterior si el campo no se modifica en un contacto existente.  

**Reto adicional:**  
Agrega un campo opcional `attachments` para cargar archivos adjuntos a cada contacto en formato imagen o pdf.  
Valida el tipo de archivo y el tamaño máximo permitido.  
Envía los datos del formulario en formato `multipart/form-data`.  
Permite cargar múltiples archivos por contacto.  
Muestra la lista de las urls de los archivos adjuntos al cargar la página del formulario si el contacto ya existe.  
Guarda los nuevos archivos adjuntos y elimina todos los anteriores si el usuario los reemplaza en un contacto existente.  
Mantén los archivos adjuntos anteriores si el campo no se modifica en un contacto existente.  

## Reto de Super Saiyajin God Blue: Wizard

![ssjBlue](https://static.wikia.nocookie.net/dragonball/images/8/82/Goku_SSB_EP24.png/revision/latest/scale-to-width-down/200)

Crea un formulario de contactos dividido en pasos secuenciales.

**Organiza el formulario en dos pasos:**

*Paso 1:*  
Solicita los datos personales: `name`, `email`.

*Paso 2:*  
Solicita la información profesional: `job`, `company`.

**En cada paso:**

- Valida los campos antes de permitir avanzar al siguiente paso.
- Muestra mensajes claros de validación.
- Permite volver al paso anterior para modificar la información.

**Al completar todos los pasos:**

- Valida todos los campos antes de enviar el formulario.
- Envía todos los datos en una única solicitud.
- Envia los datos en formato `application/json`.
- Guarda los datos en el servidor.
- Devuelve una respuesta indicando si la operación fue exitosa.

**Recomendaciones:**
- Agrega una barra de progreso o un indicador visual que muestre el avance del usuario en cada paso.

**Reto adicional:**  
Al finalizar, muestra un resumen de todos los pasos con opción de editar cualquier paso desde ese resumen antes del envío final.

**Reto adicional:**  
Guarda el estado parcial del formulario (datos ingresados hasta el momento) si el usuario recarga la página o abandona y vuelve.  
Recupera automáticamente el estado guardado y continúa desde el último paso completado.  

**Reto adicional:**  
Si no existe, agrega el paso 3 de números de teléfono.  
Agrega un formulario dinámico (ver reto 4) para cargar múltiples números de teléfono asociados al contacto.  
Cada conjunto de campos debe incluir los campos `prefix` en forma de selector desplegable para el código de país y `number` para el número de teléfono.  
Si guardas el estado parcial del formulario, guarda también los números de teléfono si el usuario los carga en el paso 3.  
Si tienes el resumen final, muestra los números de teléfono en el resumen y la opción de volver a el paso 3 para editarlos.  

**Reto adicional:**  
Si no existe, agrega el paso 4 de carga de archivos.  
Agrega al paso 4 un campo opcional `avatar` para cargar una imagen asociada al contacto.  
Valida el tipo de archivo y el tamaño máximo permitido.  
Envía los datos del formulario en formato `multipart/form-data`.  
Si guardas el estado parcial del formulario, guarda también la imagen si el usuario la carga en el paso 4.  
Si tienes el resumen final, muestra la imagen en el resumen y la opción de volver a el paso 4 para editarla.

**Reto adicional:**  
Si no existe, agrega el paso 4 de carga de archivos.  
Agrega al paso 4 un campo opcional `attachments` para cargar archivos adjuntos a cada contacto en formato imagen o pdf.  
Valida el tipo de archivo y el tamaño máximo permitido.  
Permite cargar múltiples archivos adjuntos por contacto.  
Envía los datos del formulario en formato `multipart/form-data`.  
Si guardas el estado parcial del formulario, guarda también los archivos adjuntos si el usuario los carga en el paso 4.  
Si tienes el resumen final, muestra los archivos adjuntos en el resumen y la opción de volver a el paso 4 para editarlos.  

# ¡Suerte!

Si completaste cada reto y los retos adicionales con las recomendaciones de usabilidad, validaciones y seguridad,  
**¡felicitaciones!** Estás al nivel del Ultra Instinct.

![ultra](https://static.wikia.nocookie.net/dragonball/images/6/60/Ultra_Instinct_Goku_Full_Body.jpg/revision/latest/scale-to-width-down/200)
