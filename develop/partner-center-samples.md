---
title: Partnerközpont – minták
description: A Partnerközpont API-k gyors igénylése érdekében biztosítunk egy C\ felügyelt kódrészleteket és REST-mintakéréseket és -válaszokat tartalmazó mintaprogramot.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 36d1c74e12ae680facef1414ce35ac2d6fb5322c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547835"
---
# <a name="partner-center-samples"></a>Partnerközpont – minták

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont API-k gyors igénylése érdekében biztosítunk egy mintaprogramot, egy C#-beli felügyelt kódrészleteket, valamint REST-mintakéréseket és -válaszokat.

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

| Sample                                                        | Részletek                                             |
|---------------------------------------------------------------|-----------------------------------------------------|
| Kódrészletek                                                 | A mutatók és a .NET-, Java- és PowerShell-kódrészletek, amelyek megmutatják, hogyan használható az Partnerközpont felügyelt API az ügyfélfiókok kezelésére, elemzések lekértére, megrendelések le rendelésére, számlázás és előfizetések kezelésére, támogatás biztosítanak, valamint fiókok és profilok kezelésére: [Forgatókönyvek.](scenarios.md)                                                                          |
| REST-minták                                                  | A mintakérések és válaszok, amelyek megmutatják, hogyan használható az Partnerközpont REST API az ügyfélfiókok kezelésére, elemzések lekérésére, megrendelések lekérésére, számlázás és előfizetések kezelésére, támogatás igénylésére és fiókok és profilok kezelésére: [Forgatókönyvek.](scenarios.md)                                                                                                       |
| [Konzolos tesztalkalmazás](console-test-app.md)                       | Ez az alkalmazás C# és Java nyelven érhető el, és kódot és hibakezelést biztosít a forgatókönyvek szakaszban felsorolt összes forgatókönyvhöz.                                                                        |
| [CSP-ügyfél – webes áruház oldala](csp-customer-web-storefront.md) | Ezen a webhelyen egy működő online áruház látható, amely segítségével az ügyfelek Microsoft-termékekre vonatkozó előfizetéseket vásárolhatnak. A CSP Customer Storefront Builder gyorsútmutatója segítségével könnyedén létrehozhat webhelyet a [vállalata számára.](csp-customer-storefront-builder-quick-start-guide-.md)                                                              |
| Webhely tárolása                                                | Ez az alkalmazás bemutatja, hogyan lehet webáruházat építeni a partnerek számára elérhető ajánlatok Felhőszolgáltató alapján. Az ügyfelek létrehozhatnak egy áruházfiókot, és szoftver-előfizetéseket rendelnek a webhelyen keresztül.<br/><br/>                  **Szerezze be a kódot:**<br/> [A mintakód letöltése](https://go.microsoft.com/fwlink/p/?LinkId=746683)<br/><br/>                                            **Mit kell konfigurálni a kiadás előtt:**<br/><br/> - Hitelesítés: Alkalmazásazonosító & titkos kód<br/> - Védjegyezés: embléma és cégnév<br/> – Üdvözlőüzenet<br/> – Ajánlatok, beleértve a leírásokat és az árakat. Az alkalmazás feltételezi, hogy a listaárai tartalmazzák a vonatkozó adókat. Másik lehetőségként további logikát is hozzáadhat az adó kiszámításához a kijelentkezés során.<br/> - Fizetési adatok: adja meg saját hitelkártya-beállításait, PayPal vagy egyéb fizetési típusokat. Mielőtt konfigurálja ezt a részt, olvassa el a fizetés nélküli, csalással vagy visszaéléssel [kapcsolatos útmutatót.](/partner-center/non-payment-fraud-misuse) |