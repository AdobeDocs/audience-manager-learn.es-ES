---
title: Validación de ID de dispositivo global
description: Obtenga información sobre la validación de los ID de dispositivo enviados a las fuentes de datos globales para obtener un formato adecuado y sobre los mensajes de error cuando los ID tienen un formato incorrecto.
feature: Data Governance & Privacy
topics: mobile
activity: implement
doc-type: article
team: Technical Marketing
kt: 2977
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 0ff3f123-efb3-4124-bdf9-deac523ef8c9
source-git-commit: 2094d3bcf658913171afa848e4228653c71c41de
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Validación de ID de dispositivo global {#global-device-id-validation}

Los identificadores publicitarios de dispositivos (es decir, iDFA, GAID, Roku ID) tienen estándares de formato que deben cumplirse para poder utilizarse en el ecosistema de la publicidad digital. Hoy en día, los clientes y socios pueden cargar ID en nuestras fuentes de datos globales en cualquier formato sin recibir notificación de si el ID tiene el formato correcto. Esta función introduce la validación de los ID de dispositivo enviados a las fuentes de datos globales para un formato adecuado y proporciona mensajes de error cuando los ID tienen un formato incorrecto. Se admitirá la validación para [!DNL iDFA], [!DNL Google Advertising] y [!DNL Roku IDs] en el lanzamiento.

## Descripción general de los estándares de formato {#overview-of-format-standards}

AAM A continuación, se muestran los grupos globales de ID de publicidad de dispositivos que actualmente reconoce y admite el servicio de campañas de publicidad de dispositivos de la siguiente manera Se implementan como compartidos [!UICONTROL Data Sources] que puede utilizar cualquier cliente o socio de datos que trabaje con datos vinculados a usuarios de estas plataformas.

<table>
  <tr>
   <td>Plataforma </td>
   <td>AAM ID de origen de datos </td>
   <td>Formato de ID </td>
   <td>AAM ID de PID </td>
   <td>Notas </td>
  </tr>
  <tr>
   <td>Google Android (GAID)</td>
   <td>20914</td>
   <td>32 números hexadecimales, generalmente presentados como 8-4-4-4-12<em>por ejemplo, 97987bca-ae59-4c7d-94ba-ee4f19ab8c21<br/> </em> </td>
   <td>1352</td>
   <td>Este ID debe recopilarse en un formulario sin procesar/sin hash/sin modificar Referencia - <a href="https://play.google.com/about/monetization-ads/ads/ad-id/">https://play.google.com/about/monetization-ads/ads/ad-id/</a></td>
  </tr>
  <tr>
   <td>Apple iOS (IDFA)</td>
   <td>20915</td>
   <td>32 números hexadecimales, generalmente presentados como 8-4-4-4-12 <em>por ejemplo, 6D92078A-8246-4BA4-AE5B-76104861E7DC<br /> </em> </td>
   <td>3560</td>
   <td>Este ID debe recopilarse en un formulario sin procesar/sin hash/sin modificar Referencia - <a href="https://support.apple.com/en-us/HT205223">https://support.apple.com/en-us/HT205223</a></td>
  </tr>
  <tr>
   <td>Roku (RIDA)</td>
   <td>121963</td>
   <td>32 números hexadecimales, generalmente presentados como 8-4-4-4-12 <em>ejemplo,</em> <em>fcb2a29c-315a-5e6b-bcfd-d889ba19aada</em></td>
   <td>11536</td>
   <td>Este ID debe recopilarse en un formulario sin procesar/sin hash/sin modificar Referencia - <a href="https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework">https://sdkdocs.roku.com/display/sdkdoc/Roku+Advertising+Framework</a> </td>
  </tr>
  <tr>
   <td>ID de publicidad de Microsoft (MAID)</td>
   <td>389146</td>
   <td>Cadena numérica alfa</td>
   <td>14593</td>
   <td>Este ID debe recopilarse en un formulario sin procesar/sin hash/sin modificar Referencia - <a href="https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid">https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid</a><br/><a href="https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx">https://msdn.microsoft.com/en-us/library/windows/apps/windows.system.userprofile.advertisingmanager.advertisingid.aspx</a></td>
  </tr>
  <tr>
   <td>Samsung DUID</td>
   <td>404660</td>
   <td>Ejemplo de cadena numérica alfa, 7XCBNROQJQPYW</td>
   <td>15950</td>
   <td>Este ID debe recopilarse en un formulario sin procesar/sin hash/sin modificar Referencia - <a href="https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api">https://developer.samsung.com/tv/develop/api-references/samsung-product-api-references/productinfo-api</a> </td>
  </tr>
</table>

## Configurar un identificador de publicidad en la aplicación {#setting-an-advertising-identifier-in-the-app}

La configuración del ID del anunciante en la aplicación es un proceso de dos pasos: primero, recuperar el ID del anunciante y, a continuación, enviarlo al Experience Cloud. A continuación, se encuentran vínculos para realizar estos pasos.

1. Recuperación del ID
   1. [!DNL Apple] información acerca de [!DNL advertising ID] se puede encontrar [AQUÍ](https://developer.apple.com/documentation/adsupport/asidentifiermanager).
   1. Información sobre la configuración de [!DNL advertiser ID] para [!DNL Android] se pueden encontrar desarrolladores de [AQUÍ](http://android.cn-mirrors.com/google/play-services/id.html).
1. Enviarlo al Experience Cloud mediante la variable [!DNL setAdvertisingIdentifier] en el SDK
   1. Información para utilizar `setAdvertisingIdentifier` está en [documentación](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-an-advertising-identifier) para ambos [!DNL iOS] y [!DNL Android].

`// iOS (Swift) example for using setAdvertisingIdentifier:`
`ACPCore.setAdvertisingIdentifier([AdvertisingId]) // ...where [AdvertisingId] is replaced by the actual advertising ID`

## Mensajería de error de DCS para ID incorrectos  {#dcs-error-messaging-for-incorrect-ids}

Cuando se envía un ID de dispositivo global incorrecto (IDFA, GAID, etc.) en tiempo real al Audience Manager, se devuelve un código de error en la visita. A continuación se muestra un ejemplo de un error devuelto porque el ID se envía como un [!DNL Apple IDFA], que solo debe contener letras mayúsculas y, sin embargo, el ID tiene una &quot;x&quot; en minúsculas.

![imagen de error](assets/image_4_.png)

Consulte la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-error-codes.html?lang=en#api-and-sdk-code) para obtener la lista de códigos de error.

## Incorporación de ID de dispositivo globales {#onboarding-global-device-ids}

Además del envío en tiempo real de los ID de dispositivos globales, también puede hacer lo siguiente:[!DNL onboard]&quot; (cargar) datos también con los ID. Este proceso es el mismo que cuando se incorporan datos con los ID de cliente (normalmente a través de pares clave/valor), pero simplemente se usan los ID de fuente de datos adecuados para que los datos se asignen al ID de dispositivo global. La documentación sobre el proceso de incorporación se encuentra en [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/sending-audience-data/batch-data-transfer-process/batch-data-transfer-overview.html?lang=en#implementation-integration-guides). Recuerde utilizar el ID de fuente de datos global en función de la plataforma que utilice.

Si se envían ID de dispositivo globales incorrectos a través del proceso de incorporación, los errores se muestran en la [[!DNL Onboarding Status Report]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reporting/onboarding-status-report.html?lang=en#reporting).

A continuación se muestra un ejemplo de un error que llegaría a través de ese informe:

![imagen de error](assets/image_5_.png)
