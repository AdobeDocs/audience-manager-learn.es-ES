---
title: Compatibilidad con IAB TCF 2.0
description: Obtenga información sobre el complemento Audience Manager a IAB TCF y cómo funciona con el objeto de inclusión de Adobe y su proveedor de administración de consentimiento (CMP).
feature: Data Governance & Privacy
activity: implement
doc-type: technical video
team: Technical Marketing
thumbnail: 26434.jpg
kt: 5027
role: Developer, Data Engineer, Architect
level: Experienced
exl-id: 04b4e786-0457-4dcc-bcf9-a79eda67bb2e
source-git-commit: 62b43b5627dabf754cf821f974a56c60989ef7ef
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---

# Compatibilidad con IAB TCF 2.0 en Audience Manager {#iab-tcf-support-in-audience-manager}

Adobe le proporciona los medios para administrar y comunicar las opciones de privacidad de los usuarios a través de la funcionalidad de inclusión y a través del complemento Audience Manager a la compatibilidad con Transparencia IAB y Consentimiento Framework 2.0 (TCF 2.0). Este artículo funciona junto con la documentación para ayudarle a comprender el complemento Audience Manager para IAB TCF y cómo funciona junto con el objeto Opt-in de Adobe y su proveedor de administración de consentimiento (CMP). Para obtener más información sobre la IAB, consulte su sitio web en [https://www.iabeurope.eu/](https://www.iabeurope.eu/).

## Primer paso: Comprensión de la inclusión del ID de Experience Cloud {#first-step-understand-ecid-s-opt-in}

Para comprender cómo trabajar con el TCF de IAB, primero debe comprender [!DNL Opt-in] , que forma parte de la biblioteca del servicio de ID de Experience Cloud (ECID). Si no está familiarizado con el funcionamiento de la inclusión, consulte [este artículo útil](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/id-service/use-opt-in-to-control-experience-cloud-activities-based-on-user-consent.html) primero. También debe revisar el servicio de inclusión (Opt-in) [documentación](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html). Una vez que haya pasado por esos recursos, vuelva a esta página y continúe.

## El complemento Audience Manager para el TCF de IAB {#the-audience-manager-plug-in-for-iab-tcf}

Ahora que tiene al menos una comprensión básica de cómo funciona el servicio de inclusión (Opt-in), el Audience Manager puede colocarlo en él [!DNL IAB Transparency and Consent Framework (TCF)] compatibilidad, que se realiza mediante un complemento en el objeto Opt-in.

El complemento Audience Manager para el TCF de IAB amplía la funcionalidad de inclusión y permite a los clientes de AAM evaluar, cumplir y reenviar las opciones de privacidad de los usuarios a los socios descendentes de acuerdo con el TCF de IAB. Proporciona un estándar que los controladores de datos (es decir, usted como cliente de Adobe) y los proveedores (DMP, DSP, SSP, servidores de publicidad, etc.) se puede utilizar para comprender el consentimiento en todo el entorno de consentimiento.

## Habilitar TCF de IAB {#enabling-iab-tcf}

Habilitar el complemento de Audience Manager para el TCF de IAB es fácil si utiliza Adobe Experience Platform Launch, ya que es una casilla de verificación sencilla, como se muestra en el breve vídeo siguiente:

>[!VIDEO](https://video.tv.adobe.com/v/26433/?quality=12)

Como alternativa, si no utiliza Launch, puede utilizar `isIabContext=true` para habilitarlo cuando cree una instancia del visitante Experience Cloud. Esto inicia el flujo TCF de IAB, es decir, añade otro paso a la recopilación de consentimiento, utilizando el TCF de IAB para consultar la cadena TC de IAB y la devuelve a Opt-in, que a su vez se comunica con las soluciones de Experience Cloud.

## Cadena TC de IAB {#iab-tcf-consent-string}

Uno de los estándares que ofrece la IAB es una &quot;cadena de consentimiento&quot; (también conocida como &quot;DaisyBit&quot;), que en realidad es dos listas juntas:

1. Finalidades: **Qué** ¿se da el consentimiento para ello?
1. Proveedores: **Quién** ¿se da el consentimiento a?

### Finalidades {#purposes}

Con IAB TCF 2.0, existen diez &quot;propósitos&quot; para los que recabar el consentimiento (qué pueden hacer los proveedores con los datos del visitante). Adobe Audience Manager no requiere los diez, sino que solo requiere consentimiento para los siguientes fines, además del consentimiento del proveedor:

* **Objetivo 1:** Almacenar o acceder a información en un dispositivo;
* **Objetivo 10:** Desarrollar y mejorar los productos;
* **Objetivo especial 1:** Asegúrese de la seguridad, evite el fraude y depure.

Esta es la primera parte de la cadena TC de IAB y se registra como 1 y 0, lo que dicta si se aprueba o no ese propósito o actividad.

>[!NOTE]
>
>De acuerdo con las regulaciones de la IAB, el Objetivo especial 1 (garantizar la seguridad, evitar el fraude y depurar) siempre está aceptado y los usuarios no pueden oponerse a él.

### Proveedores {#vendors}

Otra parte de la cadena TC de la IAB es una larga lista de varios cientos de proveedores, de modo que se pueda presentar a los visitantes una lista de proveedores aplicables que tengan etiquetas en el sitio y puedan elegir qué proveedores utilizar. Los proveedores mantienen su punto en la lista. Por ejemplo, el número de proveedor de Adobe Audience Manager en esta lista es 565. Si ese número de la lista tiene un &quot;1&quot;, el Audience Manager puede realizar los propósitos aprobados desde el principio de la lista. Si el punto de AAM tiene un &quot;0&quot;, no puede hacer nada con los datos.

**Para que el Audience Manager proporcione una interfaz de usuario para que los clientes utilicen el TCF de IAB para elegir estos fines y proveedores, o para aprobar o desaprobar toda actividad, debe utilizar un socio de CMP registrado con el TCF de IAB o crear uno que admita el TCF de IAB y esté registrado con el TCF de IAB.**

## Inclusión: Traducción entre IAB y aplicaciones de Adobe {#opt-in-translating-between-iab-and-adobe-solutions}

Una de las ventajas de utilizar el TCF de la IAB es que los propósitos estándar enumerados anteriormente probablemente dan al usuario final más idea de lo que está aprobando que una lista de soluciones de Adobe. Es posible que los usuarios finales no sepan qué significa &quot;aprobar&quot; el Audience Manager o [!DNL Target], pero &quot;Almacenar y/o acceder a información en un dispositivo&quot; o &quot;Desarrollar y mejorar productos&quot; es probablemente más fácil para que ellos entiendan y consientan.

Para que el Audience Manager sea aprobado (es decir, para que la traducción de los objetivos de la IAB para la inclusión AAM un voto afirmativo), los objetivos 1 y 10, enumerados anteriormente, deben ser aprobados por el usuario final. Si alguno de estos no está aprobado, o si un vendedor no está aprobado, no AAM ejecutar activaciones de píxeles ni establecer cookies. También es bueno saber que muchos clientes simplemente eligen proporcionar al usuario final una interfaz de usuario &quot;todo o nada&quot;, que, por supuesto, permitiría o no el uso de Audience Manager (y las otras soluciones de Experience Cloud).

Hay información buena en la variable [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=en) acerca de cómo se aplica el flujo del complemento Audience Manager para TCF de IAB a los casos de uso de Publisher y del anunciante.

## IAB: Envío de consentimiento descendente {#iab-sending-consent-downstream}

Cuando se utiliza el complemento de Audience Manager para IAB TCF, las opciones de consentimiento del usuario también se envían a las sincronizaciones de ID de nivel de plataforma (de terceros) para socios que están presentes en la lista de proveedores globales, de modo que el socio tenga la información de consentimiento del usuario y también pueda actuar en consecuencia. Esta información se envía en dos variables:

* rgpd = 1
* gdpr_permission = [cadena de consentimiento codificada]

La advertencia es que si el usuario está en contexto IAB y no da su consentimiento (o proporciona un consentimiento negativo), entonces el Audience Manager no recopila la cadena IAB TC y, como tal, elimina las llamadas. Así que, en ese caso... no pasar el consentimiento a través del flujo descendente.

## Demostración {#demo}

En el siguiente vídeo, vea cómo las cookies y las señalizaciones de ECID y las soluciones se ven afectadas por las selecciones de elección de usuario de IAB.

>[!VIDEO](https://video.tv.adobe.com/v/26434/?quality=12)

Para obtener información más detallada sobre el complemento de Audience Manager para IAB TCF 2.0, incluido cómo implementar y probar, casos de uso y flujo de trabajo, consulte la [documentación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).
