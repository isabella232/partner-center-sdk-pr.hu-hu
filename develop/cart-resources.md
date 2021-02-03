---
title: Kosár erőforrásai
description: Egy partner megrendelést helyez el egy kosárban, ha az ügyfél egy előfizetést szeretne megvásárolni az ajánlatok listájából.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3aea428064654077ae67974132ec05918edfee65
ms.sourcegitcommit: a8fe6268fed2162843e7c92dca41c3919b25647d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/26/2020
ms.locfileid: "97768016"
---
# <a name="cart-resources"></a>Kosár erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partnerek megrendelést végeznek, amikor egy ügyfél előfizetést szeretne vásárolni az ajánlatok listájáról.

## <a name="cart"></a>Kosár

Útmutató a kosárhoz.

| Tulajdonság              | Típus             | Leírás                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | A kosár sikeres létrehozásához megadott cart-azonosító.                               |
| creationTimeStamp     | DateTime         | A kosár létrehozásának dátuma dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazható.      |
| lastModifiedTimeStamp | DateTime         | A kosár utolsó frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazható. |
| expirationTimeStamp   | DateTime         | A kosár lejáratának dátuma dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazható.          |
| lastModifiedUser      | sztring           | A kosár utolsó frissítését végző felhasználó. A kosár sikeres létrehozása után alkalmazható.                          |
| Listaelemek             | Objektumok tömbje | [CartLineItem](#cartlineitem) -erőforrások tömbje.                                                   |
| status                | sztring           | A kosár állapota. A lehetséges értékek: "Active" (frissíthető/elküldhető) és "rendezett" (már elküldve). |

## <a name="cartlineitem"></a>CartLineItem

Egy kosárban található egy elem.

| Tulajdonság             | Típus                             | Leírás                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sztring                           | Egy cart-sor egyedi azonosítója. A kosár sikeres létrehozása után alkalmazható.                                                                   |
| catalogItemId        | sztring                           | A katalógus-elemek azonosítója.                                                                                                                          |
| friendlyName         | sztring                           | Választható. A partner által a egyértelműsítse segítségére meghatározott rövid név.                                                                 |
| quantity             | int                              | A licencek vagy példányok száma.                                                                                                                  |
| currencyCode         | sztring                           | A Pénznemkód.                                                                                                                                    |
| billingCycle         | Objektum                           | Az aktuális időszakban beállított számlázási ciklus típusa.                                                                                                 |
| termDuration         | sztring                           | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: P1M (1 hónap), P1Y (1 év) és P3Y (3 év).                                |
| résztvevők         | Az Object string párok listája      | A PartnerId on Record (MPNID) gyűjteménye a vásárláson.                                                                                          |
| provisioningContext  | Szótár<karakterlánc, karakterlánc>       | A megvásárolt tétel kiépítés során használt további környezet. Az adott elemhez szükséges értékek meghatározásához tekintse meg az SKU provisioningVariables tulajdonságát. |
| orderGroup           | sztring                           | Egy csoport, amely jelzi, hogy mely elemek lesznek elküldve ugyanabban a sorrendben.                                                                          |
| addonItems           | **CartLineItem** -objektumok listája | A bővítményekhez készült cart-elemek gyűjteménye. Ezeket az elemeket a rendszer az alapszintű, a legfelső szintű cart-elem megvásárlásakor megvásárolt alapelőfizetés felé vásárolja meg. |
| error                | Objektum                           | Ha hiba történt, a kosár létrehozása után alkalmazza a rendszer.                                                                                                    |
| renewsTo             | Objektumok tömbje                 | [RenewsTo](#renewsto) -erőforrások tömbje.                                                                            |

## <a name="renewsto"></a>RenewsTo

Egy olyan elem, amely egy cart-sorban található.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | sztring           | No              | A megújítási időszak érvényességének ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: **P1M** (1 hónap) és **P1Y** (1 év). |

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

## <a name="carterror"></a>CartError

Egy olyan hibát jelöl, amely a kosár létrehozása után következik be.

| Tulajdonság         | Típus                                   | Leírás                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [A partner Center hibakódai](error-codes.md) | A kosár típusú hiba.                                                                       |
| errorDescription | sztring                                 | A hiba leírása, beleértve a támogatott értékekkel, az alapértelmezett értékekkel vagy a korlátozásokkal kapcsolatos megjegyzéseket is. |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Egy kosár-pénztár eredményét jelöli.

| Tulajdonság    | Típus                                              | Leírás                     |
|-------------|---------------------------------------------------|---------------------------------|
| rendelések      | [Megrendelési](order-resources.md#order) objektumok listája.         | A megrendelések gyűjteménye.       |
| orderErrors | [OrderError](#ordererror) -objektumok listája. | A sorrendi hibák gyűjteménye. |

## <a name="ordererror"></a>OrderError

Olyan hibát jelöl, amely egy rendelés létrehozásakor a kosár-pénztárban történik.

| Tulajdonság     | Típus   | Leírás                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | sztring | A megrendelési csoport azonosítója a hibával. |
| code         | int    | A hibakód.                                 |
| leírás  | sztring | A hiba leírása.                   |
