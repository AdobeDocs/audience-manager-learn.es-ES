---
title: Migración del servidor de seguimiento al reenvío del lado de servidor en el nivel de grupo de informes
description: Obtenga información sobre cómo habilitar el reenvío de datos de Adobe Analytics del lado del servidor al Audience Manager en el nivel de grupo de informes en lugar de en el nivel de servidor de seguimiento.
product: audience manager
feature: Adobe Analytics Integration
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 1776
role: Developer, Data Engineer
level: Intermediate
exl-id: 08b81e52-a28a-43e4-a284-df2460a43016
source-git-commit: 4adaade180545bcf5f911b7453a7e9939e2ed178
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Migración del servidor de seguimiento al reenvío del lado de servidor en el nivel de grupo de informes {#migrating-from-tracking-server-to-report-suite-level-server-side-forwarding}

Este artículo y vídeo le mostrarán cómo habilitar el reenvío de datos de [!DNL Analytics] del lado del servidor al Audience Manager en un nivel [!UICONTROL report suite] en lugar de en un nivel [!UICONTROL tracking server].

## Introducción {#introduction}

Si tiene Adobe Audience Manager AND Adobe Analytics, puede implementar el reenvío del lado del servidor de los datos de [!DNL Analytics] al Audience Manager. Esto significa que, en lugar de que la página envíe dos visitas (una a [!DNL Analytics] y otra al Audience Manager), puede enviar una visita a [!DNL Analytics] y [!DNL Analytics] reenviará esos datos al Audience Manager.

Si ya lo tiene en funcionamiento y lo tenía habilitado o implementado antes de octubre de 2017, el reenvío del lado del servidor podría basarse en [!UICONTROL Tracking Server], que tenía que habilitar el Servicio de atención al cliente de Adobe o Adobe Consulting. Desde octubre de 2017, ahora puede configurar el reenvío del lado del servidor por su cuenta y hacerlo en el nivel de grupo de informes (reenvío por grupo de informes). Hay beneficios significativos en esto, que se discuten más adelante.

## reenvío de [!UICONTROL Tracking server] {#tracking-server-forwarding}

Su [!UICONTROL tracking server] es la ubicación a la que está enviando sus datos de [!DNL Analytics], así como el dominio donde se escriben la cookie y la solicitud de imagen. Debe configurarse en DTM o [!DNL Experience Platform Launch], o en el archivo [!DNL AppMeasurement.js], y normalmente tendrá este aspecto, con el nombre de su sitio o empresa reemplazando &quot;misitio&quot;:

`s.trackingServer = "mysite.sc.omtrdc.net";`

Si el reenvío del lado del servidor está configurado para el reenvío en el nivel [!UICONTROL tracking server], cualquier visita que se envíe a este [!UICONTROL tracking server] (SI el servicio de ID de Experience Cloud también está habilitado) se reenviará al Audience Manager. Esto tenía que habilitarlo el Servicio de atención al cliente de Adobe o Adobe Consulting. También son ellos los que pueden deshabilitarlo, DESPUÉS de haber cambiado al reenvío de [!UICONTROL report suite], como se describe a continuación.

Si no está seguro de si [!DNL tracking server forwarding] está habilitado para usted, póngase en contacto con el Servicio de atención al cliente de Adobe o con Adobe Consulting para que se lo indiquen.

## Reenvío del lado del servidor de nivel [!UICONTROL Report-suite] {#report-suite-level-server-side-forwarding}

Una de las mayores ventajas de pasar al reenvío de [!UICONTROL report suite] desde el reenvío de [!UICONTROL tracking server] es que ahora podrá usar &quot;Audience Analytics&quot;, que es la capacidad de reenviar al Audience Manager [!UICONTROL segments] de nuevo a Adobe Analytics para un análisis detallado del segmento. Esta excelente característica NO se admite si sigue reenviando [!UICONTROL tracking server] y no [!UICONTROL report suite]. Vea más información sobre el Audience Analytics en [documentation](https://experienceleague.adobe.com/docs/analytics/integration/audience-analytics/mc-audiences-aam.html).

>[!VIDEO](https://video.tv.adobe.com/v/23701/?quality=12)

## Sugerencia importante {#additional-resources}

Como se indica en el vídeo anterior, una vez que haya configurado todo el [!UICONTROL report suites] para el reenvío que desea reenviar al Audience Manager, debe ponerse en contacto con el Servicio de atención al cliente de Adobe o con Adobe Consulting y hacer que deshabiliten el reenvío de [!UICONTROL tracking server]. No es una emergencia que haga esto, ya que tener tanto el reenvío de [!UICONTROL tracking server] como el de [!UICONTROL report suite] no resultan en visitas duplicadas. Sin embargo, es recomendable tener solamente [!UICONTROL report suite] reenvíos activados.

Si deja activado el reenvío de [!UICONTROL tracking server], no solo podría reenviar datos de [!UICONTROL report suites] que no desea reenviar, sino que en el futuro, después de que usted (y todos los usuarios de su compañía) hayan olvidado que el reenvío de [!UICONTROL tracking server] está activado, podría pensar que no se están reenviando datos de un [!UICONTROL report suite] específico. Esto se debe a que no está activado en el nivel de grupo de informes, pero los datos se siguen reenviando de todos modos debido al [!UICONTROL tracking server]. AAM Entonces perderá tiempo y dinero averiguando por qué reenvía y también pagando por llamadas al servidor que no esperaba. Por lo tanto, es aconsejable deshabilitar el reenvío de [!UICONTROL tracking server] en cuanto tenga todos los [!UICONTROL report suites] configurados para el reenvío que sean adecuados para sus necesidades comerciales.
