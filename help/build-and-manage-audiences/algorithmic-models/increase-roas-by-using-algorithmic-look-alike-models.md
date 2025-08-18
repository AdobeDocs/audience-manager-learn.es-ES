---
title: Aumente el ROAS utilizando modelos algorítmicos (de similitud)
description: El verdadero poder del modelado de similitudes de Audience Manager se obtiene cuando busca expandir la audiencia de línea de base con un conjunto de usuarios nuevo y de calidad a partir de fuentes de datos de segundo y tercer nivel. En este tutorial, aprenda los pasos para crear un modelo a partir de estos datos.
feature: Algorithmic Models
topics: null
activity: use
doc-type: feature video
team: Technical Marketing
thumbnail: 25188.jpg
kt: 1849
role: User, Developer, Data Engineer, Architect, Data Architect, Admin, Leader
level: Intermediate
exl-id: 6626ae11-8709-4302-9e03-0d55878d2409
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Aumente el ROAS utilizando modelos algorítmicos (de similitud) en Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

El verdadero poder de la similitud [!UICONTROL Modeling] de Audience Manager se obtiene cuando se busca expandir la audiencia de línea de base con un conjunto de usuarios nuevo y de calidad a partir de fuentes de datos de segundo nivel y de terceros. En este tutorial, aprenderá los pasos necesarios para crear un modelo a partir de estos datos.

## Habilitar flujos de datos de segundo nivel o de terceros desde Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Para utilizar datos de segundo nivel y de terceros en un modelo de similitud, primero debemos habilitar estos datos en la interfaz de Audience Manager. Adobe tiene un gran número de proveedores de datos de segundo nivel y de terceros entre los que puede elegir. Están disponibles en una interfaz de autoservicio en AAM, a través de Audience Marketplace. Vaya a Audience Marketplace y examine las diferentes opciones. El siguiente vídeo le mostrará cómo hacerlo, incluido cómo habilitar flujos de &quot;prueba antes de comprar&quot; gratuitos, para que pueda bloquear los datos que serán más útiles para su organización antes de comprometerse con los precios del proveedor de datos.

Además, para ayudarle a investigar y decidir qué proveedor de datos utilizar, un buen recurso es [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/30106/?quality=12&captions=spa)

## Identificar o crear un rasgo o segmento de usuario (conversión) ideal {#identify-create-an-ideal-user-conversion-trait-or-segment}

¿Qué está intentando que la gente haga en su sitio? ¿Cuál es su evento de conversión? Por supuesto, hay muchas respuestas diferentes a esta pregunta, según el tipo/vertical del sitio y los objetivos de la organización. En cualquier caso, es común en AAM crear un rasgo para los visitantes que han cumplido con esos criterios.

En el siguiente vídeo, le mostraré cómo crear un rasgo de conversión, que querrá tener en su lugar a medida que siga con este tutorial y cree un modelo de similitud.

Además, cuando se utilizan eventos de Adobe Analytics para crear características, hay una complicación importante que debe tener en cuenta para que no recopile más usuarios de los que debería en las características. Vea el siguiente vídeo para la gran revelación. :)

>[!VIDEO](https://video.tv.adobe.com/v/328096/?quality=12&captions=spa)

**NOTA:** En el vídeo anterior, el ejemplo que se muestra supone que tiene Adobe Analytics. Obviamente, este puede no ser el caso. Si tienes Google Analytics (GA), tenemos un módulo que puedes usar para enviar datos a AAM (consulta la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html?lang=es)), y si tu actividad de conversión en tu sitio se envía a AAM por GA, puedes crear tu rasgo de conversión a partir de eso. Si tiene una solución de análisis diferente (o no tiene ninguna solución de análisis), aún puede enviar datos a AAM a través de nuestro código DIL y la función `submit`, etc. (consulte la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=es)). A continuación, cree la característica de conversión en función de los datos enviados cuando la actividad de conversión se realice en el sitio.

## Crear un modelo de similitud a partir de datos de segundo nivel o de terceros {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Después de completar los pasos anteriores, ahora estamos listos para crear un modelo algorítmico (de similitud). A medida que configuramos el modelo, utilizaremos el rasgo de conversión como nuestro rasgo base (visitantes clave que queremos duplicar) y utilizaremos el flujo de datos de terceros habilitado como nuestro grupo de personas del que extraer.

>[!VIDEO](https://video.tv.adobe.com/v/30105/?quality-12&captions=spa)

## Una práctica recomendada importante {#an-important-best-practice}

Al crear el modelo algorítmico en Audience Manager, obviamente queremos que el modelo sea lo más efectivo posible. Como el modelo está considerando todos los rasgos de los que forman parte los miembros de su rasgo o segmento base, no ayuda al modelo si TODAS las personas están en un rasgo o segmento. Por lo tanto, si tiene rasgos súper genéricos (como todas las personas que visitaron su sitio, o todas las personas que recibieron publicidad suya, etc.), asegúrese de que la fuente de datos a la que pertenecen NO se incluya en las fuentes de datos de su modelo. En el caso de uso de este artículo, es poco probable que lo haga, ya que nos centramos en ver los datos de terceros para nuestra nueva similitud, pero vale la pena mencionarlos de todos modos y se aplica a TODOS sus modelos algorítmicos.

## Crear un(a) [!UICONTROL Algorithmic Trait] {#creating-an-algorithmic-trait}

A continuación, tendremos que crear un [!UICONTROL Algorithmic Trait] para poder utilizar los resultados del modelo. Sin crear un rasgo, el modelo es inútil. Por lo tanto, después de ejecutar el modelo, asegúrese de entrar en el cuadro de diálogo de características y crear un [!UICONTROL Algorithmic Trait]. El siguiente vídeo lo analiza y muestra un par de sugerencias.

>[!VIDEO](https://video.tv.adobe.com/v/30104/?quality=12&captions=spa)

## Cree un segmento a partir de los datos del modelo y envíelo a DSP {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Una vez que haya creado un [!UICONTROL Algorithmic Trait], puede crear un nuevo segmento para ponerlo en él, de modo que pueda activar los datos (no puede activar un rasgo, sino crear un nuevo segmento de un rasgo con el [!UICONTROL Algorithmic Trait] en él, de modo que pueda activar (usar) el segmento).

Una vez que haya creado un segmento a partir de este rasgo algorítmico, tendrá una audiencia de clientes potenciales que se ven como personas que ya se han convertido en su sitio. Ahora puede asignar este segmento a cualquiera de sus destinos de DSP en Audience Manager. Podrá dirigir su marketing a esos similitudes, que son más propensos a convertir en su sitio que solo el público normal, lo que aumenta su retorno de la inversión en publicidad.
