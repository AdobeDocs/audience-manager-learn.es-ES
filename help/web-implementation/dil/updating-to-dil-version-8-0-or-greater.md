---
title: Actualización a Adobe Audience Manager DIL versión 8.0 (o posterior)
description: Este artículo le explica cómo actualizar el código de Adobe Audience Manager (AAM) Data Integration Library (DIL) a la versión 8.0 o posterior. Esto hace referencia a la implementación de DIL "del lado del cliente", no al reenvío de datos de Adobe Analytics del lado del servidor, y cubre DTM, Launch by Adobe e implementaciones sin la solución de administrador de etiquetas de Adobe.
feature: DIL Implementation
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1841
role: Developer
level: Intermediate
exl-id: 8c1e6ed5-0f21-427b-a681-0ecb020a0e60
source-git-commit: d47848370e7bf7617f2b706041c911161a6479cd
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Actualización a DIL versión 8.0 de Adobe Audience Manager (o superior) {#updating-to-adobe-audience-manager-s-dil-version-or-greater}

Este artículo contiene instrucciones para actualizar el código de Adobe Audience Manager (AAM) [!DNL Data Integration Library] (DIL) a la versión 8.0 o posterior. Esto hace referencia a la implementación de DIL &quot;del lado del cliente&quot;, no al reenvío de datos de Adobe Analytics del lado del servidor, y cubre DTM, Launch by Adobe e implementaciones sin la solución de administrador de etiquetas de Adobe.

## Información general {#overview}

El código [!DNL Data Integration Library] (DIL) de Audience Manager le permite implementar AAM en su sitio web*. Al implementar versiones anteriores de DIL, no era necesario tener implementado también el servicio Experience Cloud ID de Adobe (ECID) (aunque era una muy buena idea). A partir de la versión 8.0 de DIL, existe una dependencia estricta de la versión 3.3 o posterior de ECID. Si implementa DIL 8.0 o posterior sin ECID 3.3 o con una versión anterior, obtendrá un error y no funcionará. Dado que hay varias formas de implementar AAM, hemos creado esta página para darle algunos pasos que debe seguir, así como algunas recomendaciones. A continuación, se muestran estos pasos y recomendaciones desglosados por plataforma o método de implementación. Encontrará más información sobre DIL en la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=es).

* Como se indica en la descripción de esta página, esto solo cubre las implementaciones de DIL del lado del cliente, utilizadas por los clientes de AAM que no tienen Adobe Analytics. Si tiene Adobe Analytics, debe utilizar el método de reenvío del lado del servidor para implementar AAM. Este método se describe en la [documentación](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=es).

## Elementos y métodos duplicados y obsoletos {#duplicate-and-deprecated-elements-and-methods}

En versiones anteriores de DIL y ECID, había métodos duplicados (métodos que realizan la misma función tanto en DIL como en ECID), lo que causaba confusión sobre cuál usar. Normalmente, necesitaba utilizar ambos y hacerlos coincidir, y ese mensaje no se comunicaba bien a nuestros clientes. A partir de DIL 8.0, estos métodos y elementos duplicados han quedado obsoletos en DIL y se recomienda utilizar la versión de ECID.

Por ejemplo:

* Al utilizar [!DNL DIL.create], algunos elementos han quedado obsoletos y debe utilizar los elementos ECID en su lugar. Estos elementos se llaman en la [[!DNL DIL.create] documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html?lang=es).
* El método de nivel de instancia [!DNL idSync] también ha quedado obsoleto, como se llama en la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-instance-methods.html?lang=es) del método.

## Sincronización de ID con un ID de cliente {#id-syncing-with-a-customer-id}

En AAM, puede sincronizar su UUID (ID único de usuario anónimo) en el equipo con un ID de cliente, de modo que pueda cargar datos sin conexión sobre ese cliente y vincularlos con su comportamiento en línea para comprender mejor a sus clientes. En el pasado, esto se ha hecho de una de las dos maneras siguientes:

* El método de instancia [!DNL idSync]
* El elemento [!DNL declaredId] de [!DNL DIL.create]

Si ha estado utilizando cualquiera de estos métodos antiguos para sincronizarse con un ID de cliente, se recomienda encarecidamente que actualice a mediante el método [!DNL setCustomerIDs], que forma parte del servicio ECID. Encontrará más información sobre [!DNL setCustomerIDs] en la [documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=es) del método.

**Sugerencia rápida:** Al usar cualquiera de los métodos anteriores, hizo referencia a la AAM [!UICONTROL Data Source] con el ID [!UICONTROL Data Source] (también conocido como &quot;DPID&quot;). Al actualizar a [!DNL setCustomerIDs], tendrá que usar el &quot;[!UICONTROL Data Source]&quot; de AAM [!UICONTROL Integration Code] en su lugar. Sigue apuntando al mismo(a) [!UICONTROL Data Source], pero es solo un identificador diferente. Esto se muestra en el siguiente vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/33684/?captions=spa&quality=12)

En las siguientes secciones se enumeran los pasos y recomendaciones para actualizar a DIL 8.0 según el método de implementación:

## Actualización a DIL 8.0 en Adobe Experience Platform tags {#updating-to-dil-in-experience-platform-launch}

Pasos básicos para actualizar a DIL 8.0

1. Si utiliza DIL anterior a la versión 8.0, antes de actualizar, vaya a la configuración de DIL en la extensión de AAM y tome nota de las opciones avanzadas que esté utilizando (que se utilizarán en un paso posterior).
1. Actualice la extensión de AAM a la versión 8.0 o superior.
1. Compruebe que la extensión del servicio de Experience Cloud ID sea de la versión 3.3.0 o superior.
1. Habilite los métodos y elementos ECID en la extensión ECID para cualquier método o elemento obsoleto (como `disableIDSyncs`) que estuviera en la extensión AAM anterior a la 8.0 o en el código personalizado para DIL.

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`
   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`
   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `dSyncSSLUseAkamai`
   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

1. Publique los cambios.

>[!VIDEO](https://video.tv.adobe.com/v/33685/?captions=spa&quality=12)

## Actualización a DIL 8.0 en Adobe DTM {#updating-to-dil-in-adobe-dtm}

1. Actualice la herramienta AAM a la versión 8.0 o superior. Esta configuración de versión se encuentra en la sección &quot;General&quot; de la herramienta AAM.
1. Para cualquier método o elemento obsoleto (como `disableIDSyncs`) que estuviera en el código personalizado de la herramienta AAM anterior a la versión 8.0 para DIL, anótelo (para que pueda agregarlo a la herramienta ECID) y luego elimínelo de la herramienta personalizada [!DNL DIL code] en la herramienta AAM.
1. Actualice la extensión del servicio de Experience Cloud ID a la versión 3.3.0 o superior
1. Agregue las opciones avanzadas a la herramienta ECID que eliminó del código personalizado de la herramienta AAM.
1. Publicación de los cambios

## Actualización a DIL 8.0 sin la solución Adobe Tag Management {#additional-resources}

Si actualiza el código directamente en la página, puede reemplazar los elementos más antiguos por elementos más nuevos, excepto cuando necesite mover métodos/elementos de DIL a ECID, como se ha indicado anteriormente. En ese caso, simplemente reemplazará el método/elemento antiguo en la ubicación de DIL con el método/elemento ECID en la ubicación ECID.

Lo mismo ocurre con los administradores de etiquetas que no son de Adobe. Siempre que tenga las versiones antiguas en esa solución de administración de etiquetas, sustitúyalo por el código nuevo tal como se describe en los pasos siguientes.

1. Actualice la biblioteca de DIL a la última versión (8.0 o posterior): deberá obtener el código DIL más reciente de Adobe Consulting o del Servicio de atención al cliente de Adobe, ya que actualmente no está disponible en una ubicación pública. A continuación, simplemente reemplace el código de biblioteca antiguo de DIL por el nuevo código de biblioteca DIL y continúe con el siguiente paso (no se detenga ahora o tendrá problemas, ha).
1. Instale [!DNL ECID Service] o actualice su versión existente a la 3.3.0 o superior. Puede descargar la versión más reciente del servicio de Experience Cloud ID [desde nuestra página de GitHub](https://github.com/Adobe-Marketing-Cloud/id-service/releases). Si necesita ayuda con esto, consulte la [documentación](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=es) o hable con un consultor de Adobe.

1. Compruebe que todos los métodos o elementos obsoletos del código personalizado de DIL se muevan a los métodos ECID:

   1. (DIL) `disableDestinationPublishingIframe` -> (ECID) `disableIdSyncs`

      [Documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html?lang=es)

   1. (DIL) `disableIDSyncs` -> (ECID) `disableIdSyncs`

      [Documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/disableidsync.html?lang=es)

   1. (DIL) `iframeAkamaiHTTPS` -> (ECID) `idSyncSSLUseAkamai`

      [Documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html?lang=es)

   1. (DIL) `declaredId` -> (ECID) `setCustomerIDs`

      [Documentación](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html?lang=es)
