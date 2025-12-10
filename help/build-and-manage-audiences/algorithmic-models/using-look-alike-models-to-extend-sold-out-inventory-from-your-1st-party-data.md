---
title: Utilice modelos de similitud para ampliar el inventario agotado de datos de origen
description: En este tutorial, explicamos los pasos que debe seguir para configurar y utilizar modelos de similitud, de modo que pueda crear nuevas audiencias de similitud y venderlas como una extensión para su segmento de conversión.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 23523.jpg
kt: 1688
role: User, Developer, Admin, Leader
level: Intermediate
exl-id: 6820528e-3211-4a1d-be05-50f1292179d2
source-git-commit: d47848370e7bf7617f2b706041c911161a6479cd
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Utilice modelos de similitud para ampliar el inventario agotado de datos de origen {#using-look-alike-models-to-extend-sold-out-inventory-from-your-st-party-data}

En este tutorial, explicaremos los pasos que debe seguir para configurar y utilizar la similitud de [!UICONTROL Models] con el fin de crear nuevas audiencias de similitud y venderlas como una extensión para el segmento de conversión.

## Detalles del caso de uso {#use-case-details}

Es editor de contenido. Si ya ha agotado el inventario de convertidores en su sitio, es posible que piense que su oportunidad termina allí. Especifique la similitud de AAM [!UICONTROL Models]. Al utilizar esta función, puede ampliar aún más el inventario de productos agotados y también vender audiencias de personas que quizá aún no se hayan convertido, pero que se ven o actúan como personas que se han convertido. Este segmento de audiencia generalmente se vendería por menos que los convertidores reales, pero sin embargo le permite agregar a sus resultados finales al proporcionar una opción de audiencia adicional para anunciantes que deseen colocar anuncios en su sitio. La ventaja adicional de este caso de uso es que no le cuesta nada ejecutar este modelo en los datos de origen.

Los pasos de este tutorial son los siguientes:

1. Identificar/crear un rasgo o segmento de usuario (conversión) ideal
1. Crear un modelo utilizando este rasgo o segmento de conversión como elemento base
1. Elija [!UICONTROL First party] fuentes de datos en el modelo y ejecute el modelo
1. Crear un [!UICONTROL Algorithmic Trait] a partir de los resultados del modelo y agregar la característica a un segmento
1. Ofrezca el segmento a los anunciantes interesados para ampliar las ventas del segmento de conversión

## Identificar o crear un rasgo o segmento de usuario (conversión) ideal {#identify-create-an-ideal-user-conversion-trait-or-segment}

¿Qué está intentando que la gente haga en su sitio? ¿Cuál es su evento de conversión? Por supuesto, hay muchas respuestas diferentes a esta pregunta, según el tipo/vertical del sitio y los objetivos de la organización. En cualquier caso, es común en AAM crear un rasgo para los visitantes que han cumplido con esos criterios.

En este caso de uso, esto ya se supone, porque ha vendido el inventario para las personas que son convertidores. Sin embargo, a los efectos de este tutorial, es bueno analizarlo como referencia para el resto del caso de uso.

Además, cuando se utilizan eventos para crear características, hay una clave importante que debe tenerse en cuenta para que no se recopilen más usuarios de los que deberían en la característica. Vea el siguiente vídeo para la gran revelación. :)

>[!VIDEO](https://video.tv.adobe.com/v/328096/?captions=spa&quality=12)

**NOTA:** En el vídeo anterior, el ejemplo que se muestra supone que tiene Adobe Analytics. Obviamente, este puede no ser el caso. Si tienes Google Analytics (GA), tenemos un módulo que puedes usar para enviar datos a AAM (consulta la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=es)), y si tu actividad de conversión en tu sitio se envía a AAM por GA, puedes crear tu rasgo de conversión a partir de eso. Si tiene una solución de análisis diferente (o no tiene ninguna solución de análisis), aún puede enviar datos a AAM a través de nuestro código DIL y la función `submit`, etc. (consulte la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html?lang=es)). A continuación, vuelva a crear la característica de conversión en función de los datos enviados cuando la actividad de conversión se realiza en el sitio.

## Crear un modelo de similitud a partir de datos de origen {#creating-a-look-alike-model-from-first-party-data}

En este paso, vamos a crear un modelo de similitud de [!UICONTROL First Party]. Esto significa que no solo vamos a utilizar un rasgo o segmento de conversión de origen para nuestro rasgo o segmento base (esto sería normal para la mayoría de los modelos de todos modos), sino que también vamos a buscar en el conjunto de datos de origen de más personas que se parecen a los convertidores. No se buscan datos de segundo nivel o de terceros.

En este caso de uso, esto es importante, ya que estamos intentando crear un segmento de usuarios en nuestro sitio que se parecen a los convertidores, pero que aún no se han convertido, de modo que podamos vender este segmento de similitud a anunciantes interesados.

>[!VIDEO](https://video.tv.adobe.com/v/328111/?captions=spa&quality-12)

## Crear un rasgo algorítmico {#creating-an-algorithmic-trait}

A continuación, tendremos que crear un [!UICONTROL Algorithmic Trait] para poder usar los resultados del modelo. Sin crear un rasgo, el modelo es inútil. Así que después de ejecutar el modelo, asegúrese de ir al cuadro de diálogo de características y crear un [!UICONTROL Algorithmic Trait]. El siguiente vídeo lo analiza y muestra un par de sugerencias.

>[!VIDEO](https://video.tv.adobe.com/v/30107/?captions=spa&quality=12)

## Ofrecer [!UICONTROL Algorithmic Segment] a los anunciantes {#offering-the-algorithmic-segment-to-advertisers}

Una vez que haya creado un [!UICONTROL Algorithmic Trait], puede crear un nuevo segmento para ponerlo en él, de modo que pueda activar los datos (no puede activar un rasgo, sino crear un nuevo segmento de un rasgo con el [!UICONTROL Algorithmic Trait] en él, de modo que pueda activar (usar) el segmento.

Una vez que haya creado un segmento de visitantes de origen con una puntuación alta en el modelo de similitud (es decir, que parecen convertidores pero aún no se han convertido), puede ofrecer este segmento a los anunciantes del sitio, incluso después de haber vendido todo el inventario de convertidores reales del sitio. Esta es una excelente manera de ampliar esta audiencia y seguir viendo ingresos adicionales al usar la similitud [!UICONTROL Models] en Audience Manager.
