---
title: Aumente el ROAS utilizando modelos algorítmicos (de similitud)
description: El poder real del modelado de similitudes de Audience Manager se produce cuando busca expandir la audiencia de línea de base con un conjunto de usuarios nuevo y de calidad a partir de fuentes de datos de segundo y tercer nivel. En este tutorial, aprenda los pasos para crear un modelo a partir de estos datos.
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
source-wordcount: '909'
ht-degree: 0%

---

# Aumente el ROAS utilizando modelos algorítmicos (de similitud) en Audience Manager {#increase-roas-by-using-algorithmic-look-alike-models-in-audience-manager}

El verdadero poder de la similitud de Audience Manager [!UICONTROL Modeling] se produce cuando intenta ampliar la audiencia de línea de base con un conjunto de usuarios de calidad y completamente nuevo a partir de fuentes de datos de segundo nivel y de terceros. En este tutorial, aprenderá los pasos necesarios para crear un modelo a partir de estos datos.

## Habilitar flujos de datos de segundo nivel o de terceros desde el Audience Marketplace {#enable-2nd-or-3rd-party-data-streams-from-the-audience-marketplace}

Para utilizar datos de segundo nivel y de terceros en un modelo de similitud, primero debemos habilitar estos datos en la interfaz de Audience Manager. Adobe tiene un gran número de proveedores de datos de segundo nivel y de terceros entre los que puede elegir. AAM Están disponibles para usted en una interfaz de autoservicio en, a través del Audience Marketplace de, y en la interfaz de usuario de, a través de. Vaya al Audience Marketplace y examine las posibilidades. El siguiente vídeo le mostrará cómo hacerlo, incluido cómo habilitar flujos de &quot;prueba antes de comprar&quot; gratuitos, para que pueda bloquear los datos que serán más útiles para su organización antes de comprometerse con los precios del proveedor de datos.

Además, para ayudarle a investigar y decidir qué proveedor de datos utilizar, un bueno recurso es el [[!DNL Adobe Audience Finder]](https://www.adobe-audience-finder.com/).

>[!VIDEO](https://video.tv.adobe.com/v/25188/?quality=12)

## Identificar o crear un rasgo o segmento de usuario (conversión) ideal {#identify-create-an-ideal-user-conversion-trait-or-segment}

¿Qué está intentando que la gente haga en su sitio? ¿Cuál es su evento de conversión? Por supuesto, hay muchas respuestas diferentes a esta pregunta, según el tipo/vertical del sitio y los objetivos de la organización. AAM En cualquier caso, es habitual en los visitantes crear un rasgo para los visitantes que cumplen con esos criterios.

En el siguiente vídeo, le mostraré cómo crear un rasgo de conversión, que querrá tener en su lugar a medida que siga con este tutorial y cree un modelo de similitud.

Además, cuando se utilizan eventos de Adobe Analytics para crear características, hay una complicación importante que debe tener en cuenta para que no recopile más usuarios de los que debería en las características. Vea el siguiente vídeo para la gran revelación. :)

>[!VIDEO](https://video.tv.adobe.com/v/23431/?quality=12)

**NOTA:** En el vídeo anterior, el ejemplo que muestro supone que tiene Adobe Analytics. Obviamente, este puede no ser el caso. Si tiene Google Analytics AAM de (GA), tenemos un módulo que puede utilizar para enviar datos a los usuarios de (consulte la sección sobre el envío de datos de ) a los que se puede acceder a través de la interfaz de usuario de (véase la página de ayuda de ). [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-modules.html)AAM ), y si GA envía a la actividad de conversión de su sitio, puede crear su rasgo de conversión a partir de ese elemento. AAM Si tiene una solución de análisis diferente (o no tiene ninguna solución de análisis), aún puede enviar datos a las soluciones a través de nuestro código de DIL y la dirección de correo electrónico de la aplicación de datos de a través de la interfaz de usuario de la aplicación de datos de. `submit` función, etc. (consulte la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html)). A continuación, cree la característica de conversión en función de los datos enviados cuando la actividad de conversión se realice en el sitio.

## Crear un modelo de similitud a partir de datos de segundo nivel o de terceros {#create-a-look-alike-model-from-2nd-or-3rd-party-data}

Después de completar los pasos anteriores, ahora estamos listos para crear un modelo algorítmico (de similitud). A medida que configuramos el modelo, utilizaremos el rasgo de conversión como nuestro rasgo base (visitantes clave que queremos duplicar) y utilizaremos el flujo de datos de terceros habilitado como nuestro grupo de personas del que extraer.

>[!VIDEO](https://video.tv.adobe.com/v/25190/?quality-12)

## Una práctica recomendada importante {#an-important-best-practice}

Al crear el modelo algorítmico en Audience Manager, obviamente queremos que el modelo sea lo más efectivo posible. Como el modelo está considerando todos los rasgos de los que forman parte los miembros de su rasgo o segmento base, no ayuda al modelo si TODAS las personas están en un rasgo o segmento. Por lo tanto, si tiene rasgos súper genéricos (como todas las personas que visitaron su sitio, o todas las personas que recibieron publicidad suya, etc.), asegúrese de que la fuente de datos a la que pertenecen NO se incluya en las fuentes de datos de su modelo. En el caso de uso de este artículo, es poco probable que lo haga, ya que nos centramos en ver los datos de terceros para nuestra nueva similitud, pero vale la pena mencionarlos de todos modos y se aplica a TODOS sus modelos algorítmicos.

## Cree un [!UICONTROL Algorithmic Trait] {#creating-an-algorithmic-trait}

A continuación, tendremos que crear una  [!UICONTROL Algorithmic Trait], para que se puedan utilizar los resultados del modelo. Sin crear un rasgo, el modelo es inútil. Por lo tanto, después de ejecutar el modelo, asegúrese de entrar en el cuadro de diálogo de características y crear una [!UICONTROL Algorithmic Trait]. El siguiente vídeo lo analiza y muestra un par de sugerencias.

>[!VIDEO](https://video.tv.adobe.com/v/25191/?quality=12)

## DSP Cree un segmento a partir de los datos del modelo y envíelo a la dirección de correo electrónico de {#creating-a-segment-from-the-model-data-and-sending-it-to-dsps}

Una vez que haya creado un [!UICONTROL Algorithmic Trait], puede crear un nuevo segmento para colocarlo en, de modo que pueda activar los datos (no puede activar una característica, sino crear un nuevo segmento de una característica con la variable [!UICONTROL Algorithmic Trait] en él, para que pueda activar (utilizar) el segmento).

Una vez que haya creado un segmento a partir de este rasgo algorítmico, tendrá una audiencia de clientes potenciales que se ven como personas que ya se han convertido en su sitio. DSP Ahora puede asignar este segmento a cualquiera de los destinos de la en Audience Manager. Podrá dirigir su marketing a esos similitudes, que son más propensos a convertir en su sitio que solo el público normal, lo que aumenta su retorno de la inversión en publicidad.
