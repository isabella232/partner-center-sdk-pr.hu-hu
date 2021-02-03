---
title: Partnerközpont – minták
description: Ha segítségre van szüksége a partner Center API-k gyors üzembe helyezéséhez, biztosítunk egy minta programot, C \ felügyelt kódrészleteket és REST-példákat és válaszokat.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2098544e8607eabc4d25d90dcd7cad41510778a9
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768204"
---
# <a name="partner-center-samples"></a>Partnerközpont – minták

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ha segítségre van szüksége a partner Center API-k gyors üzembe helyezéséhez, a rendszer a C# által felügyelt kódrészleteket és a REST-példákat és a válaszokat is biztosítjuk.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Sample                                                        | Részletek                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kódrészletek                                                 | Az olyan mutatók és .NET-, Java-és PowerShell-kódrészletek esetében, amelyek bemutatják, hogyan használhatja a partner Center felügyelt API-t az ügyfelek fiókjainak kezeléséhez, az elemzések elvégzéséhez, a megrendelések kezeléséhez [](scenarios.md), a számlázás és az előfizetések felügyeletéhez, valamint a fiókok és profilok kezeléséhez,                                                                          |
| REST-minták                                                  | Azokról a példákról, amelyek bemutatják, hogyan használható a partner Center REST API a vevői fiókok kezeléséhez, az elemzéshez, a megrendelések megrendeléséhez, a számlázás és az előfizetések kezeléséhez, támogatás biztosításához és fiókok és profilok kezeléséhez, lásd: [forgatókönyvek](scenarios.md)                                                                                                       |
| [Konzolos tesztalkalmazás](console-test-app.md)                       | Ez az alkalmazás a C#-ban és a Java-ban is elérhető, és a forgatókönyvek szakaszban felsorolt összes forgatókönyv esetében kódot és valamilyen hibát tartalmaz.                                                                        |
| [CSP-ügyfél – webes áruház oldala](csp-customer-web-storefront.md) | Ez a webhely egy működő online áruházat mutat be, amelyet az ügyfelek használhatnak a Microsoft-termékek előfizetésének megvásárlásához. Egyszerűen létrehozhat egy webhelyet a vállalat számára a [CSP Customer kirakat-készítő útmutatójának](csp-customer-storefront-builder-quick-start-guide-.md)használatával.                                                              |
| Webhely tárolása                                                | Ez az alkalmazás bemutatja, hogyan hozhat létre webáruházat a Cloud Solution Provider-partnerek számára elérhető ajánlatok katalógusa alapján. Az ügyfelek létrehozhatnak egy áruházbeli fiókot, és megrendelhetik a webhelyén a szoftverek előfizetéseit.<br/><br/>                  **A kód beszerzése:**<br/> [A mintakód letöltése](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **A kiadás előtti konfigurálás:**<br/><br/> -Hitelesítés: alkalmazás-azonosító & titkos kulcs<br/> -Branding: embléma és cég neve<br/> – Üdvözlő üzenet<br/> -Ajánlatok, beleértve a leírásokat és az árakat. Az alkalmazás feltételezi, hogy a lista díjszabása tartalmazza a vonatkozó adókat. Alternatív megoldásként további logikát is hozzáadhat az adó kiszámításához a pénztárban.<br/> – Fizetési információk: saját bankkártya-beállítások, PayPal vagy más fizetési típusok megadása. Mielőtt konfigurálja ezt a részt, olvassa el a [nem fizetéssel, csalással vagy visszaéléssel](/partner-center/non-payment-fraud-misuse)kapcsolatos útmutatót. |