---
layout: page
title: Habilitar la Plataforma OJS para Preservación en LOCKSS o CLOCKSS
---

Una vez que se llega a un acuerdo con respecto a la preservación, 
los ajustes dentro de la interfaz administrativa de OJS hacen posible la 
recopilación y preservación a través de la Red LOCKSS Global (GLN) o la Red CLOCKSS. 
Para obtener más información, contáctenos en: <a href="https://www.lockss.org/contact">https://www.lockss.org/contact</a>

## OJS 3.X

Recomendamos utilizar una versión estable reciente de OJS 3.X, 
OJS 3.1.3 como mínimo. Para obtener más información, 
consulte <a href="https://pkp.sfu.ca/ojs/ojs_download/">https://pkp.sfu.ca/ojs/ojs_download/</a>.

### Problemas Conocidos

#### OJS 3.1.2.1

Esta versión de OJS tiene una declaración de permisos incorrecta para GLN. 
Por favor, actualice a una versión más reciente, OJS 3.1.3 o superior. 
Si eso no es una opción, puede ser posible corregir manualmente la declaración 
de permisos. La declaración de permisos correcta para GLN 
es: LOCKSS system has permission to collect, preserve, and serve this Archival Unit.

#### OJS 3.1.1.X y anteriores

Estas versiones de OJS 3.X no están habilitadas para la preservación en CLOCKSS 
o GLN. Por favor, actualice a una versión más reciente, OJS 3.1.3 o superior, 
o aplique un parche antes de habilitar la preservación en CLOCKSS y/o LOCKSS. 
Un posible parche se puede encontrar en: <a href="https://github.com/pkp/ojs/pull/2215/commits/22f1d220">https://github.com/pkp/ojs/pull/2215/commits/22f1d220</a>.

### Configuración de contenido OJS 3.X para preservación GLN/CLOCKSS:

1. Vea la sección de <a href="https://docs.pkp.sfu.ca/learning-ojs/en/settings-distribution">Distribution Settings</a> de la interfaz administrativa.
2. En la pestaña de <a href="https://docs.pkp.sfu.ca/learning-ojs/en/settings-distribution#archiving">Archiving</a>, marque las casillas para "Enable LOCKSS" y/o "Enable CLOCKSS" según sea necesario.
3. Para revisar la página de manifiesto, haga clic en "Publisher Manifest" junto a las casillas de verificación. La página resultante debería mostrar una lista de los problemas de su revista.

###Configuración del contenido de OJS 3.X para la Red de Preservación de PKP (PN):

Las instrucciones para configurar OJS para la PN se encuentran en: <a href="https://docs.pkp.sfu.ca/pkp-pn/en/">https://docs.pkp.sfu.ca/pkp-pn/en/</a>.


## OJS 2.X

OJS 2.X está retirado y no se recomienda para uso continuo. Por favor, actualícese a OJS 3.X. Para obtener más información, consulte <a href="https://pkp.sfu.ca/ojs/ojs_download/">https://pkp.sfu.ca/ojs/ojs_download/</a>.

### Configuración de contenido OJS 2.X para preservación GLN/CLOCKSS:

1. Vaya a la pantalla de Journal Management para cada revista y haga clic en "Journal Setup".
2. Seleccione el segundo ítem, "Policies".
3. Desplácese hacia abajo hasta la sección 2.6, "Journal Archiving".
4. Marque la casilla "Enable LOCKSS..." para activar la función LOCKSS.
5. En el cuadro de texto debajo, escriba la siguiente oración exactamente como está escrita: CLOCKSS system has permission to ingest, preserve, and serve this Archival Unit.
6. Guarde los cambios.
7. Verifique los cambios yendo a la página principal de su(s) revista(s) en su navegador:
8. Edite la URL en la barra de direcciones de su navegador (si es aplicable, elimine la palabra 'index' al final de la URL) para que termine con /gateway/lockss. (Si se redirige de nuevo a la página principal, los cambios de configuración no se guardaron correctamente. De lo contrario, verá una página relacionada con LOCKSS con el logotipo de LOCKSS).
9. Verifica CLOCKSS yendo a la página "Acerca de" y luego a la sección de "Políticas Editoriales". Busca la declaración de permisos de CLOCKSS, la cual debería aparecer hacia la parte inferior de la página.

