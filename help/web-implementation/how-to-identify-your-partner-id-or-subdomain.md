---
title: Cómo identificar el ID o subdominio de socio
description: Obtenga información sobre cómo identificar su ID de socio o subdominio al implementar algunas funciones de Experience Cloud y acerca de dos lugares en los que puede obtener este ID en la interfaz de usuario de Audience Manager.
feature: Implementation Basics
topics: null
activity: implement
doc-type: technical video
team: Technical Marketing
kt: 2359
role: Developer
level: Intermediate
exl-id: d3f4a12d-acc5-47b7-a38a-a6a14152bf3a
source-git-commit: d47848370e7bf7617f2b706041c911161a6479cd
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Cómo identificar el subdominio de Audience Manager {#how-to-identify-your-audience-manager-partner-id-or-subdomain}

Al implementar algunas características de Experience Cloud, necesita saber cuál es su Audience Manager `Subdomain` (también conocido como su `client ID` o `Partner ID`). En este vídeo, le mostraremos dos lugares en los que puede obtener esta información en la interfaz de usuario de Audience Manager.

## Regalando el final... {#giving-away-the-ending}

En caso de que prefiera saltar y encontrarlo sin ver este breve vídeo, puede encontrar su `Partner Subdomain` en dos lugares de la interfaz de usuario:

1. Si ya ha creado un rasgo de [!UICONTROL rule-based], haga clic en **[!UICONTROL Get Trait URL]**
   [!UICONTROL Get Trait URL] está junto al rasgo en la lista de rasgos de esa carpeta, y la URL incluirá su subdominio en la URL.
1. Si va a la interfaz **[!UICONTROL Tools]** > **[!UICONTROL Tags]** y hace clic en **[!UICONTROL Get code]** para el contenedor, el subdominio se encuentra hacia el final de la línea Akamai

Si no puede encontrarlo rápidamente con esas referencias rápidas, el vídeo es una asignación de tiempo breve. :)

>[!VIDEO](https://video.tv.adobe.com/v/25922/?quality=12)

>[!IMPORTANT]
>
>Hay un ID numérico asignado a cada cliente de Adobe Experience Cloud, y este suele conocerse como el &quot;PID&quot; o ID de socio. Este no es el ID del que hablamos en este artículo y vídeo. En su lugar, el &quot;subdominio de socio&quot;, que a veces se denomina ID de socio, suele ser una versión del nombre del cliente y es el subdominio del servidor al que se envían los datos. Por ejemplo, si su empresa es &quot;Bob&#39;s Knobs&quot; (todos los pomos de las puertas, por supuesto, jaja), es probable que su subdominio de socio sea &quot;bobsknobs&quot;, mientras que el &quot;PID&quot; sería algo más como &quot;12345&quot;. No suele ser necesario conocer el PID, pero es importante conocer el subdominio para poder configurar la implementación de Audience Manager.
>
