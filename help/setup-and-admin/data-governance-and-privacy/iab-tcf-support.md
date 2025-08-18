---
title: Compatibilidad con IAB TCF 2.2
description: Obtenga información acerca del complemento de Audience Manager para el TCF de IAB y cómo funciona con el objeto de inclusión de Adobe y su proveedor de administración de consentimiento (CMP).
feature: Data Governance & Privacy
thumbnail: 26434.jpg
kt: 5027
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 04b4e786-0457-4dcc-bcf9-a79eda67bb2e
source-git-commit: f9708e705d95b43084ff11e342dc54ff11d6326c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# Compatibilidad con IAB TCF 2.2 en Audience Manager {#iab-tcf-support-in-audience-manager}

Adobe le proporciona los medios para administrar y comunicar las opciones de privacidad de los usuarios a través de la funcionalidad de inclusión y a través del complemento de Audience Manager a la asistencia de IAB Transparency and Consent Framework 2.2 (TCF 2.2). Este artículo trabaja junto con la documentación para ayudarle a comprender el complemento de Audience Manager para IAB TCF y cómo funciona junto con el objeto de inclusión de Adobe y su proveedor de administración de consentimiento (CMP). Para obtener más información sobre IAB, visite su sitio web en [https://www.iabeurope.eu/](https://www.iabeurope.eu/).

## Primer paso: Comprender la inclusión de Experience Cloud ID {#first-step-understand-ecid-s-opt-in}

Para comprender cómo se trabaja con el TCF de IAB, primero debe comprender la funcionalidad [!DNL Opt-in], que forma parte de la biblioteca del servicio Experience Cloud ID (ECID). Si no está familiarizado con el funcionamiento de la inclusión, vea [este útil artículo](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html?lang=es) primero. También debería revisar la [documentación](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=es) de Opt-in. Una vez que haya pasado por esos recursos, vuelva a esta página y continúe.

## El complemento de Audience Manager para el TCF de IAB {#the-audience-manager-plug-in-for-iab-tcf}

Ahora que tiene al menos una comprensión básica del funcionamiento del servicio de inclusión (Opt-in), Audience Manager puede incluir en él la compatibilidad con [!DNL IAB Transparency and Consent Framework (TCF)], que se realiza mediante un complemento en el objeto de inclusión.

El complemento Audience Manager para el TCF de IAB amplía la funcionalidad de inclusión y permite a los clientes de AAM evaluar, cumplir y reenviar las opciones de privacidad del usuario a socios de flujo descendente de acuerdo con el TCF de IAB. Proporciona un estándar que los controladores de datos (ese es usted como cliente de Adobe) y los proveedores (DMP, DSP, SSP, servidores de publicidad, etc.) pueden utilizar para comprender el consentimiento en todo el panorama de consentimientos.

## Habilitar TCF de IAB {#enabling-iab-tcf}

Activar el complemento de Audience Manager para el TCF de IAB es fácil si utiliza Adobe Experience Platform Launch, ya que es una casilla de verificación sencilla, como se muestra en el breve vídeo siguiente:

>[!VIDEO](https://video.tv.adobe.com/v/38264/?quality=12&captions=spa)

Alternativamente, si no está utilizando Launch, puede utilizar `isIabContext=true` para habilitarlo al crear una instancia del visitante de Experience Cloud. Esto inicia el flujo TCF de IAB, es decir, añade otro paso a la recopilación de consentimiento, utilizando el TCF de IAB para consultar la cadena IAB TC y la devuelve al servicio de inclusión, que a su vez se comunica con las soluciones de Experience Cloud.

## Cadena IAB TC {#iab-tcf-consent-string}

Uno de los estándares que proporciona IAB es una &quot;cadena de consentimiento&quot; (también conocida como &quot;DaisyBit&quot;), que en realidad son dos listas juntas:

1. Propósitos: **Qué** se está dando el consentimiento para hacer?
1. Proveedores: **A quién** se le está dando consentimiento?

### Finalidades {#purposes}

Con IAB TCF 2.2, hay diez &quot;fines&quot; para los que recopilar el consentimiento (lo que los proveedores pueden hacer con los datos del visitante). Adobe Audience Manager no requiere los diez, sino que solo requiere consentimiento para los siguientes fines, además del consentimiento del proveedor:

* **Propósito 1:** Almacenar o tener acceso a información en un dispositivo;
* **Objetivo 10:** Desarrollar y mejorar productos;
* **Propósito especial 1:** Garantizar la seguridad, evitar el fraude y depurar.

Esta es la primera parte de la cadena IAB TC y se registra como 1 y 0, dictando si se aprueba o no ese propósito/actividad.

>[!NOTE]
>
>Según las regulaciones de la IAB, el propósito especial 1 (garantizar la seguridad, evitar el fraude y depurar) siempre cuenta con el consentimiento y los usuarios no pueden oponerse a él.

### Proveedores {#vendors}

Otra parte de la cadena IAB TC es una larga lista de varios cientos de proveedores, de modo que los visitantes pueden obtener una lista de los proveedores aplicables que tienen etiquetas en el sitio y pueden elegir qué proveedores utilizar. Los proveedores mantienen su lugar en la lista. Por ejemplo, el número de proveedor de Adobe Audience Manager en esta lista es 565. Si ese número de la lista tiene un &quot;1&quot;, Audience Manager puede llevar a cabo los propósitos aprobados desde el principio de la lista. Si el spot de AAM tiene un &quot;0&quot;, no puede hacer nada con los datos.

**Para que Audience Manager proporcione una interfaz de usuario para que los clientes utilicen el TCF de IAB para elegir estos propósitos y proveedores, o para aprobar o desaprobar toda actividad, debe utilizar un socio de CMP registrado con el TCF de IAB o generar uno que admita el TCF de IAB y esté registrado con el TCF de IAB.**

## Inclusión: traducción entre aplicaciones IAB y Adobe {#opt-in-translating-between-iab-and-adobe-solutions}

Una de las ventajas de utilizar el TCF de IAB es que los objetivos estándar enumerados anteriormente probablemente den al usuario final más idea de lo que está aprobando que una lista de soluciones de Adobe. Es posible que los usuarios finales no sepan lo que significa &quot;aprobar&quot; Audience Manager o [!DNL Target], pero &quot;Almacenar o acceder a información en un dispositivo&quot; o &quot;Desarrollar y mejorar productos&quot; probablemente les resulte más fácil de entender y consentir.

Para que se apruebe Audience Manager (es decir, Para que la traducción de los propósitos de IAB para la inclusión dé a AAM un &quot;sí&quot; (voto), los propósitos 1 y 10, enumerados arriba, deben recibir el consentimiento del usuario final. Si alguno de estos elementos no está aprobado, o si un vendedor no está aprobado, AAM no ejecutará activaciones de píxeles ni establecerá cookies. También es bueno saber que muchos clientes simplemente eligen proporcionar al usuario final una IU de &quot;todo o nada&quot;, lo que, por supuesto, permitiría o no permitir el uso de Audience Manager (y las otras soluciones de Experience Cloud).

Hay información interesante en la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=es) sobre cómo se aplica el flujo de TCF del complemento de Audience Manager para IAB a los casos de uso de Publicador y Anunciante.

## IAB: Envío del consentimiento descendente {#iab-sending-consent-downstream}

Cuando se utiliza el complemento de Audience Manager para el TCF de IAB, las opciones de consentimiento del usuario también se envían a las sincronizaciones de ID a nivel de plataforma (de terceros) para los socios que están presentes en la Lista global de proveedores, de modo que el socio tenga la información de consentimiento del usuario y pueda actuar en consecuencia también. Esta información se envía en dos variables:

* rgpd = 1
* gdpr_permission = [cadena de consentimiento codificada]

La advertencia es que si el usuario está en el contexto de IAB y no da su consentimiento (o da su consentimiento negativo), Audience Manager no recopila la cadena IAB TC y, como tal, descarta las llamadas. Así que, en ese caso... no se pasa el consentimiento corriente abajo.

## Demostración {#demo}

En el siguiente vídeo, vea cómo las cookies y las señalizaciones de ECID y las soluciones se ven afectadas por las selecciones de opción de usuario de IAB.

>[!VIDEO](https://video.tv.adobe.com/v/38249/?quality=12&captions=spa)

Para obtener información más detallada sobre el complemento de Audience Manager para IAB TCF 2.2, incluido cómo implementar y probar, casos de uso y flujo de trabajo, consulte la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=es).
