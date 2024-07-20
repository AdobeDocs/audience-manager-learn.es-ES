---
title: Actualización a Adobe Audience Manager DIL versión 8.0 (o posterior)
description: En este artículo se explican los pasos y recomendaciones para actualizar el código de Data Integration Library (DIL) de Adobe Audience Manager AAM () a la versión 8.0 o posterior. Esto hace referencia a la implementación de DIL del lado del cliente, no al reenvío de datos de Adobe Analytics del lado del servidor, y cubre DTM, Launch by Adobe e implementaciones sin la solución de administrador de etiquetas de Adobe.
feature: DIL Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
role: Developer, Data Engineer
level: Intermediate
exl-id: 8c1e6ed5-0f21-427b-a681-0ecb020a0e60
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Actualización a la versión 8.0 (o superior) de DIL de Adobe Audience Manager {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

Este artículo contiene instrucciones para actualizar el código de Adobe Audience Manager AAM () [!DNL Data Integration Library] (DIL) a la versión 8.0 o posterior. Esto hace referencia a la implementación de DIL del lado del cliente, no al reenvío de datos de Adobe Analytics del lado del servidor, y cubre DTM, Launch by Adobe e implementaciones sin la solución de administrador de etiquetas de Adobe.

## Información general {#overview}

El código [!DNL Data Integration Library] (DIL AAM) del Audience Manager le permite implementar el código en su sitio web*. Al implementar versiones anteriores de DIL, no era necesario tener implementado también el servicio de ID de Experience Cloud (ECID) de Adobe (aunque era una muy buena idea). A partir de la versión 8.0 de DIL, existe una dependencia estricta de la versión 3.3 o posterior de ECID. Si implementa DIL 8.0 o posterior sin ECID 3.3 o con una versión anterior, obtendrá un error y no funcionará. AAM Dado que hay varias formas de implementar la aplicación, hemos creado esta página para darle algunos pasos que debe seguir, así como algunas recomendaciones. A continuación, se muestran estos pasos y recomendaciones desglosados por plataforma o método de implementación. Encontrará más información sobre el DIL en la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=en).

* Como se indica en la descripción de esta página, esto solo cubre las implementaciones de DIL AAM del lado del cliente, utilizadas por clientes que no tienen Adobe Analytics y que no son de la misma manera que se utilizan en el lado del cliente. Si tiene Adobe Analytics AAM, debe utilizar el método de reenvío del lado del servidor para implementar la implementación de la función de reenvío de la parte del servidor de la interfaz de usuario de la aplicación de. Este método se describe en la [documentación](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html).

## Elementos y métodos duplicados y obsoletos {#duplicate-and-deprecated-elements-and-methods}

En versiones anteriores de DIL y ECID, había métodos duplicados (métodos que realizan la misma función tanto en DIL como en ECID), lo que causaba confusión sobre cuál usar. Normalmente, necesitaba utilizar ambos y hacerlos coincidir, y ese mensaje no se comunicaba bien a nuestros clientes. A partir de DIL 8.0, estos métodos y elementos duplicados han quedado obsoletos en DIL y se recomienda utilizar la versión de ECID.

Por ejemplo:

* Al utilizar [!DNL DIL.create], algunos elementos han quedado obsoletos y debe utilizar los elementos ECID en su lugar. Estos elementos se llaman en la [[!DNL DIL.create] documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html).
* El método de nivel de instancia [!DNL idSync] también ha quedado obsoleto, como se llama en la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-instance-methods.html) del método.

## Sincronización de ID con un ID de cliente {#id-syncing-with-a-customer-id}

AAM En, puede sincronizar su UUID (ID único de usuario anónimo) en el equipo con un ID de cliente, de modo que pueda cargar datos sin conexión sobre ese cliente y vincularlos con su comportamiento en línea para comprender mejor a sus clientes. En el pasado, esto se ha hecho de una de las dos maneras siguientes:

* El método de instancia [!DNL idSync]
* El elemento [!DNL declaredId] de [!DNL DIL.create]

Si ha estado utilizando cualquiera de estos métodos antiguos para sincronizarse con un ID de cliente, se recomienda encarecidamente que actualice a mediante el método [!DNL setCustomerIDs], que forma parte del servicio ECID. Encontrará más información sobre [!DNL setCustomerIDs] en la [documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) del método.

AAM **Sugerencia rápida:** Al usar anteriormente cualquiera de los métodos anteriores, hizo referencia a la [!UICONTROL Data Source] con el ID de [!UICONTROL Data Source] (también conocido como &quot;DPID&quot;). AAM Al actualizar a [!DNL setCustomerIDs], tendrá que usar el &quot;[!UICONTROL Integration Code]&quot; del [!UICONTROL Data Source] de la en su lugar. Sigue apuntando al mismo(a) [!UICONTROL Data Source], pero es solo un identificador diferente. Esto se muestra en el siguiente vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/23873/?quality=12)

En las siguientes secciones se enumeran los pasos y recomendaciones para actualizar a DIL 8.0 según el método de implementación:

## Actualización a DIL 8.0 en Adobe Experience Platform tags {#updating-to-dil-in-experience-platform-launch}

Pasos básicos para actualizar a DIL 8.0

1. Si está utilizando un DIL anterior a 8.0, antes de actualizar, vaya a la configuración del DIL AAM en la extensión de la extensión de la extensión y tome nota de cualquier opción avanzada que esté utilizando (para utilizar en un paso posterior).
1. AAM Actualice la extensión de la a la versión 8.0 o superior.
1. Compruebe que la extensión del servicio de ID de Experience Cloud sea de la versión 3.3.0 o superior.
1. AAM Habilite los métodos y elementos ECID en la extensión ECID para cualquier método o elemento obsoleto (como `disableIDSyncs`) que se encuentre en la extensión anterior a la versión 8.0 o en el código personalizado para DIL.

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`
   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`
   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `dSyncSSLUseAkamai`
   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

1. Publish los cambios.

>[!VIDEO](https://video.tv.adobe.com/v/23874/?quality=12)

## Actualización a DIL 8.0 en Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. AAM Actualice la herramienta de a la versión 8.0 o superior. AAM Esta configuración de versión se encuentra en la sección &quot;General&quot; de la herramienta de.
1. AAM Para cualquier método o elemento obsoleto (como `disableIDSyncs`) que estuviera en el código personalizado de la herramienta anterior a la versión 8.0 de para DIL AAM, anótelos (para que pueda agregarlos a la herramienta ECID) y, a continuación, elimínelos de la herramienta personalizada [!DNL DIL code] en la herramienta de.
1. Actualice la extensión del servicio de ID de Experience Cloud a la versión 3.3.0 o superior
1. AAM Añada las opciones avanzadas a la herramienta ECID que ha eliminado del código personalizado de la herramienta de.
1. Publish los cambios

## Actualización a DIL 8.0 sin solución de Adobe de Tag Management {#additional-resources}

Si actualiza el código directamente en la página, puede reemplazar los elementos más antiguos por elementos más nuevos, excepto cuando necesite mover métodos/elementos de DIL a ECID, como se ha indicado anteriormente. En ese caso, simplemente reemplazará el método/elemento antiguo en la ubicación del DIL con el método/elemento ECID en la ubicación ECID.

Lo mismo ocurre con los administradores de etiquetas que no son de Adobe. Siempre que tenga las versiones antiguas en esa solución de administración de etiquetas, sustitúyalo por el código nuevo tal como se describe en los pasos siguientes.

1. Actualice la biblioteca del DIL a la última versión (8.0 o posterior): deberá obtener el código del DIL más reciente de Adobe Consulting o del Servicio de atención al cliente de Adobe, ya que actualmente no está disponible en una ubicación pública. A continuación, simplemente sustituya el código antiguo de la biblioteca de DIL por el nuevo código de la biblioteca de DIL y continúe con el siguiente paso (no se detenga ahora o tendrá problemas, ha).
1. Instale [!DNL ECID Service] o actualice su versión existente a la 3.3.0 o superior. Puede descargar la versión más reciente del servicio de ID de Experience Cloud [desde nuestra página de GitHub](https://github.com/Adobe-Marketing-Cloud/id-service/releases). Si necesita ayuda con esto, consulte la [documentación](https://experienceleague.adobe.com/docs/id-service/using/home.html) o hable con un consultor de Adobe.

1. Compruebe que todos los métodos o elementos obsoletos del código personalizado de DIL se muevan a los métodos ECID:

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`

      [Documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html)

   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`

      [Documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html)

   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `idSyncSSLUseAkamai`

      [Documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html)

   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

      [Documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html)
