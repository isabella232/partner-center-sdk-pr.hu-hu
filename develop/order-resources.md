---
title: Erőforrások megrendelése
description: A partnerek megrendelést végeznek, amikor egy ügyfél előfizetést szeretne vásárolni az ajánlatok listájáról.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9db07337a98214b4aaa93e2c8b43b84702249b77
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768028"
---
# <a name="order-resources"></a>Erőforrások megrendelése

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partnerek megrendelést végeznek, amikor egy ügyfél előfizetést szeretne vásárolni az ajánlatok listájáról.

>[!NOTE]
>A rendelési erőforrás legfeljebb 500 kérést tartalmaz a bérlői azonosítók percenkénti száma alapján.

## <a name="order"></a>Sorrend

A partner sorrendjét ismerteti.

| Tulajdonság           | Típus                                               | Leírás                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | sztring                                             | A megrendelés sikeres létrehozásakor megadott rendelési azonosító.                                   |
| alternateId        | sztring                                             | A rendelés felhasználóbarát azonosítója.                                                                          |
|referenceCustomerId | sztring                                             | Az ügyfél-azonosító. |
| billingCycle       | sztring                                             | Azt jelzi, hogy milyen gyakorisággal történik a partner számlázása ebben a sorrendben. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)található tagok nevei. Az alapértelmezett érték a "havonta" vagy az "egykori" a megrendelés létrehozásakor. Ez a mező a megrendelés sikeres létrehozásakor lesz alkalmazva. |
| transactionType    | sztring                                             | Csak olvasható. A rendelés tranzakciós típusa A támogatott értékek a következők: "UserPurchase", "SystemPurchase" vagy "SystemBilling". |
| Listaelemek          | [OrderLineItem](#orderlineitem) -erőforrások tömbje | Az ügyfél által megvásárolt ajánlatok részletezett listája, beleértve a mennyiséget is.        |
| currencyCode       | sztring                                             | Csak olvasható. A megrendelés elhelyezésekor használt pénznem. A megrendelés sikeres létrehozása után alkalmazható.           |
| currencySymbol     | sztring                                             | Csak olvasható. A pénznemkóddal társított pénznem szimbóluma. |
| creationDate       | dátum/idő                                           | Csak olvasható. A rendelés létrehozásának dátuma dátum-idő formátumban. A megrendelés sikeres létrehozása után alkalmazható.                                   |
| status             | sztring                                             | Csak olvasható. A megrendelés állapota.  A támogatott értékek a [**OrderStatus**](#orderstatus)található tagok nevei.        |
| linkek              | [OrderLinks](utility-resources.md#resourcelinks)           | A rendelésnek megfelelő erőforrás-hivatkozások.            |
| attribútumok         | [ResourceAttributes](utility-resources.md#resourceattributes) | A sorrendnek megfelelő metaadat-attribútumok.       |

## <a name="orderlineitem"></a>OrderLineItem

A sorrend az ajánlatok részletezett listáját tartalmazza, és az egyes elemek OrderLineItem jelennek meg.

| Tulajdonság             | Típus                                      | Leírás                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | A gyűjtemény minden egyes sora egy egyedi sorszámot kap, amely a 0 és Count-1 közötti számlálást eredményezi.                                                                                                                                                 |
| offerId              | sztring                                    | Az ajánlat azonosítója.                                                                                                                                                                                                                       |
| subscriptionId       | sztring                                    | Az előfizetés azonosítója.                                                                                                                                                                                                                |
| parentSubscriptionId | sztring                                    | Választható. A szülő-előfizetés azonosítója egy kiegészítő ajánlatban. Csak a JAVÍTÁSra vonatkozik.                                                                                                                                                     |
| friendlyName         | sztring                                    | Választható. A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse.                                                                                                                                              |
| quantity             | int                                       | A licencek vagy példányok száma.                                                                                                                                                                                |
| termDuration         | sztring                                    | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: **P1M** (1 hónap), **P1Y** (1 év) és **P3Y** (3 év).                               |
| transactionType      | sztring                                    | Csak olvasható. A sorhoz tartozó tranzakció típusa A támogatott értékek: "New", "renew", "addQuantity", "removeQuantity", "Cancel", "Convert" vagy "customerCredit". |
| partnerIdOnRecord    | sztring                                    | Ha egy közvetett szolgáltató egy megrendelést helyez el egy közvetett viszonteladó nevében, töltse ki ezt a mezőt a **közvetett viszonteladóhoz** tartozó MPN-azonosítóval (soha nem a közvetett szolgáltató azonosítója). Ez biztosítja az ösztönzők megfelelő könyvelését. |
| provisioningContext  | Szótár<karakterlánc, karakterlánc>            | A katalógus egyes elemeinek kiépítési feladataihoz szükséges információk. Az SKU provisioningVariables tulajdonsága azt jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.                                                                                                                                               |
| linkek                | [OrderLineItemLinks](#orderlineitemlinks) | Csak olvasható. A rendelési sorhoz tartozó erőforrás-hivatkozások.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Megújítás időtartama – részletek.                                                                           |

## <a name="renewsto"></a>RenewsTo

A megújítási időtartam részleteit jelöli.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sztring           | No              | A megújítási időszak érvényességének ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: **P1M** (1 hónap) és **P1Y** (1 év). |

## <a name="orderlinks"></a>OrderLinks

A sorrendnek megfelelő erőforrás-hivatkozásokat jelöli.

| Tulajdonság           | Típus                                         | Leírás                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Hivatkozás](utility-resources.md#link)            | Feltöltéskor a rendelés kiépítési állapotának lekérésére szolgáló hivatkozás.       |
| önálló               | [Hivatkozás](utility-resources.md#link)            | A megrendelés erőforrásának beolvasására szolgáló hivatkozás.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

A rendeléshez társított teljes előfizetést jelöli.

| Tulajdonság           | Típus                                         | Leírás                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Hivatkozás](utility-resources.md#link)            | A kitöltéskor a sor elem [kiépítési állapotának](#orderlineitemprovisioningstatus) lekérésére szolgáló hivatkozás.       |
| SKU                | [Hivatkozás](utility-resources.md#link)            | A vásárolt katalógus-elem SKU-adatainak lekérésére szolgáló hivatkozás.                    |
| előfizetést       | [Hivatkozás](utility-resources.md#link)            | Feltöltéskor a teljes előfizetési adatokra mutató hivatkozás.                       |
| activationLinks    | [Hivatkozás](utility-resources.md#link)            | A kitöltéskor az erőforrás beolvasása hivatkozásra kattintva aktiválhatja az előfizetést.             |

## <a name="orderstatus"></a>OrderStatus

Egy [Enum/DotNet/API/System. Enum) olyan értékekkel, amelyek jelzik a sorrend állapotát.

| Érték              | Pozíció     | Leírás                                     |
|--------------------|--------------|-------------------------------------------------|
| ismeretlen            | 0            | Enum inicializáló.                               |
| befejeződött          | 1            | Azt jelzi, hogy a rendelés befejeződött.          |
| függőben            | 2            | Azt jelzi, hogy a rendelés még függőben van.      |
| megszakítva          | 3            | Azt jelzi, hogy a rendelés meg lett szakítva.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Egy [OrderLineItem](#orderlineitem)kiépítési állapotát jelöli.

| Tulajdonság                        | Típus                                | Leírás                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | A rendelési sor tételének egyedi sorszáma Az értékek 0 és Count között vannak.             |
| status                          | sztring                              | A rendelési sor eleme kiépítési állapota. Az értékek többek között az alábbiak lehetnek:</br>"Teljesítve": a megrendelés teljesítése sikeresen befejeződött, és a felhasználó használhatja a foglalásokat</br>"Nem teljesített": megszakítás miatt nem teljesül</br>"PrefulfillmentPending": a kérelem feldolgozása még folyamatban van, a teljesítés még nem fejeződött be |
| quantityProvisioningInformation | <[QuantityProvisioningStatus](#quantityprovisioningstatus) listázása> | A mennyiségi kiépítési állapotra vonatkozó információk listája a rendelési sorhoz tartozó tételnél. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

A kiépítési állapotot a mennyiség szerint jelöli.

| Tulajdonság                           | Típus                                         | Leírás                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Az elemek száma.                                 |
| status                             | sztring                                       | Az elemek számának állapota.                   |
