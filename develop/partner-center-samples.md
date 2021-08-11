---
title: Partnerközpont – minták
description: A Partnerközpont API-k gyors igénylése érdekében biztosítunk egy mintaprogramot, egy C\ felügyelt kódrészleteket, valamint REST-mintakéréseket és -válaszokat.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 34e269b1a0e711f82144898441c75d731b8613f70512517e12b6705990b35622
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997600"
---
# <a name="partner-center-samples"></a>Partnerközpont – minták

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont API-k gyors igénylése érdekében biztosítunk egy mintaprogramot, egy C#-beli felügyelt kódrészleteket, valamint REST-mintakéréseket és -válaszokat.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Sample                                                        | Részletek                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kódrészletek                                                 | Olyan mutatók és .NET-, Java- és PowerShell-kódrészletek, amelyek megmutatják, hogyan használható a Partnerközpont felügyelt API az ügyfélfiókok kezelésére, elemzések lekértére, megrendelések le rendelésére, számlázás és előfizetések kezelésére, támogatás biztosítanak, valamint fiókok és profilok kezelésére: [Forgatókönyvek.](scenarios.md)                                                                          |
| REST-minták                                                  | A mintakérések és válaszok, amelyek azt mutatják be, hogyan használható az Partnerközpont REST API az ügyfélfiókok kezelésére, elemzések lekérésére, megrendelések lekérésére, számlázás és előfizetések kezelésére, támogatás igénylésére és fiókok és profilok kezelésére: [Forgatókönyvek.](scenarios.md)                                                                                                       |
| [Konzolos tesztalkalmazás](console-test-app.md)                       | Ez az alkalmazás C# és Java nyelven érhető el, és a forgatókönyvek szakaszban felsorolt összes forgatókönyvhöz biztosít kódot és hibakezelést.                                                                        |
| [CSP-ügyfél – webes áruház oldala](csp-customer-web-storefront.md) | Ezen a webhelyen egy működő online áruház látható, amely segítségével az ügyfelek Microsoft-termékekre vonatkozó előfizetéseket vásárolhatnak. A CSP Customer Storefront Builder gyorsútmutatója segítségével egyszerűen hozhat létre webhelyet a [vállalata számára.](csp-customer-storefront-builder-quick-start-guide-.md)                                                              |
| Webhely tárolása                                                | Ez az alkalmazás bemutatja, hogyan lehet webáruházat építeni a partnerek számára elérhető ajánlatok Felhőszolgáltató alapján. Az ügyfelek létrehozhatnak egy áruházfiókot, és szoftver-előfizetéseket rendelnek a webhelyen keresztül.<br/><br/>                  **Szerezze be a kódot:**<br/> [A mintakód letöltése](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Mit kell konfigurálni a kiadás előtt:**<br/><br/> - Hitelesítés: Alkalmazásazonosító & titkos kód<br/> - Védjegyezés: embléma és cégnév<br/> – Üdvözlőüzenet<br/> – Ajánlatok, beleértve a leírásokat és az árakat. Az alkalmazás feltételezi, hogy a listaárai tartalmazzák a vonatkozó adókat. Másik lehetőségként további logikát is hozzáadhat az adó kiszámításához a kijelentkezés során.<br/> - Fizetési adatok: adja meg saját hitelkártya-beállításait, PayPal vagy egyéb fizetési típusokat. Mielőtt konfigurálja ezt a részt, olvassa el a fizetés nélküli, csalási vagy [visszaéléssel kapcsolatos útmutatót.](/partner-center/non-payment-fraud-misuse) |