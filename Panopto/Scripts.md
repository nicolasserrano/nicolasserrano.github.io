# Scripts para gestionar los videos de Panopto

Estos scritps permiten facilitar la gestión de los videos de Panopto, pero no son imprescindibles para su gestión.

## Script para lista de videos de una carpeta de Panopto
Para obtener la lista de videos de una carpeta de Panopto, se pude ejecutar el siguiente código en la consola del navegador:

```
as=document.querySelectorAll("a.detail-title")
res = "";
for (i=0;i<as.length;i++) {
  if (as[i].href != ''){
    res += "Video <a href='" + as[i].href + "' target='_blank'>" + as[i].innerText + "</a><BR>\n"
  }
}
console.log(res);
```

## Script para obtener la transcripción de los subtítulos
En el modo edición, en Subtítulos, seleccionar "Importar subtítulos" -> "Importar subtítulos automáticos".
En la consola ejectuar:

```
as=document.querySelectorAll("div.index-event-row")
res = "";
for (i=0;i<as.length;i++) {
  el = as[i].querySelector("textarea")
  if (el != null){
    res += as[i].querySelector("div.event-time").innerText + "\t" + el.dataset.init + "<BR>\n"
  }
}
console.log(res);
```

Para obtener solo el texto sin salto de párrafo, ni indicación de tiempo:

```
as=document.querySelectorAll("div.index-event-row")
res = "";
for (i=0;i<as.length;i++) {
  el = as[i].querySelector("textarea")
  if (el != null){
    res += el.dataset.init + " "
  }
}
console.log(res);
```
## Script para obtener la tabla de contenidos de un video
En el modo vista (en edición los tiempos son incluyendo las secuencias ocultas), hacer clic en Contenido.
En la consola ejectuar:

```
// Content of a Panopto video
tc=document.querySelectorAll("div.index-event")
res = "";
for (i=0;i<tc.length;i++) {
  el = tc[i].querySelector("div.event-text").querySelector("span")
  if (el != null){
    res += el.innerText + "\t" + tc[i].querySelector("div.event-time").innerText + "\n"
  }
}
console.log(res);
```

## Best Practices for Adding Captions to Your Panopto Videos
[Link a la página de University of Pittsburgh](https://www.etskb-fac.cidde.pitt.edu/panopto/best-practices-for-adding-captions-to-your-panopto-videos/)

## Mostrar los videos como vínculo o incrustado
Para mostrar los videos como vínculo (link) o incrustado (embedded), se recomienda poner los vínculos, por ejemplo,
los obtenidos con el script anterior e incluir los siguientes vínculos.

```
<script type="text/javascript" src="https://www.nicolasserrano.com/tools/libraries/setIframesForPanopto.js"></script>
<link rel="stylesheet" type="text/css" href="https://www.nicolasserrano.com/tools/libraries/material.css" />
```

Y el luggar en el que se quiera mostrar el link:
```
<a onclick="setVideoIcons(this)" href="javascript:void(0);">Mostrar vista previa de videos</a><select id="iframeSize" name="ifsize" size="1">
<option value="100">100</option>
<option value="200">200</option>
<option value="400" selected="selected">400</option>
<option value="600">600</option>
<option value="800">800</option>
<option value="1080">1080</option>
</select>
```

## Backup de videos
Se puede realizar el backup de todos los videos de una página, si en la consola 
se define la variable download=1; y después se hace clic en 'Mostrar vista previa de videos' o se ejecuta el script setIframes(null, 0)
Se descargan todos los ficheros en formato mp4, tras aceptar el aviso del navegador de que se van a descargar varios ficheros.
