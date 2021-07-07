---
title: Kocsierőforrások
description: A partnerek akkor rendelnek a kosárba, ha egy ügyfél egy ajánlatlistából szeretne előfizetést vásárolni.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 08085dde1b43f20b6f6bf707120dd87c48816aba
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974148"
---
# <a name="cart-resources"></a>Kocsierőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A partner akkor ad le rendelést, ha egy ügyfél egy ajánlatlistából szeretne előfizetést vásárolni.

## <a name="cart"></a>Kosár

Egy kosarat ír le.

| Tulajdonság              | Típus             | Leírás                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | A kosár sikeres létrehozása után megadott bevásárlókocsi-azonosító.                               |
| creationTimeStamp     | DateTime         | A kosár létrehozási dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.      |
| lastModifiedTimeStamp | DateTime         | A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva. |
| expirationTimeStamp (lejárat ideje)   | DateTime         | A kosár lejáratának dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.          |
| lastModifiedUser      | sztring           | Az a felhasználó, aki utoljára frissítette a kosárat. A kosár sikeres létrehozása után alkalmazva.                          |
| lineItems (sorsorok)             | Objektumok tömbje | [CartLineItem-erőforrások tömbje.](#cartlineitem)                                                   |
| status                | sztring           | A kosár állapota. Lehetséges értékek: "Aktív" (frissíthető/elküldhető) és "Megrendelve" (már elküldve). |

## <a name="cartlineitem"></a>CartLineItem

Egy kosárban található elemet képvisel.

| Tulajdonság             | Típus                             | Leírás                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sztring                           | A kosársorelem egyedi azonosítója. A kosár sikeres létrehozása után alkalmazva.                                                                   |
| catalogItemId (katalógusazonosító)        | sztring                           | A katalóguselem azonosítója.                                                                                                                          |
| friendlyName (rövid név)         | sztring                           | Választható. A partner által meghatározott elem rövid neve a egyértelműsséghez.                                                                 |
| quantity             | int                              | A licencek vagy példányok száma.                                                                                                                  |
| currencyCode         | sztring                           | A pénznemkód.                                                                                                                                    |
| billingCycle (számlázási ciklus)         | Objektum                           | Az aktuális időszakra beállított számlázási ciklus típusa.                                                                                                 |
| termDuration (kifejezés-lekértség)         | sztring                           | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: P1M (1 hónap), P1Y (1 év) és P3Y (3 év).                                |
| Résztvevők         | Objektumsring-párok listája      | PartnerAzonosító gyűjtemény a vásárláskor rekordban (MPN-azonosító).                                                                                          |
| provisioningContext  | Dictionary<string, string>       | A megvásárolt elem kiépítésekor használt további környezet. Egy adott elemhez szükséges értékek meghatározásához tekintse meg a termékváltozat provisioningVariables tulajdonságát. |
| orderGroup           | sztring                           | Egy csoport, amely jelzi, hogy mely elemek lesznek együtt elküldve ugyanabban a sorrendben.                                                                          |
| addonItems (bővítmények)           | **CartLineItem-objektumok** listája | Kosársorelemek gyűjteménye bővítményekhez. Ezeket az elemeket az alap előfizetéshez vásároljuk meg, amely a kosársori tétel vásárlását jelenti. |
| error                | Objektum                           | A kosár létrehozása után lesz alkalmazva hiba esetén.                                                                                                    |
| renewsTo             | Objektumok tömbje                 | A [RenewsTo erőforrások tömbje.](#renewsto)                                                                            |

## <a name="renewsto"></a>RenewsTo

Egy kosársorelemben található elemet képvisel.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration (kifejezés-lekértség)          | sztring           | No              | A megújítási időszak időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a **P1M (1** hónap) és a **P1Y (1** év). |

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

## <a name="carterror"></a>CartError

A kosár létrehozása után észlelt hibát jelöli.

| Tulajdonság         | Típus                                   | Leírás                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [Partnerközpont hibakódok](error-codes.md) | A kosárhiba típusa.                                                                       |
| errorDescription (hibaleíró) | sztring                                 | A hiba leírása, beleértve a támogatott értékekkel, alapértelmezett értékekkel vagy korlátokkal kapcsolatos megjegyzéseket. |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

A kosárból való kijelentkezés eredményét jelöli.

| Tulajdonság    | Típus                                              | Leírás                     |
|-------------|---------------------------------------------------|---------------------------------|
| rendelések      | Az Order [objektumok](order-resources.md#order) listája.         | A rendelések gyűjteménye.       |
| orderErrors (orderErrors) | Az [OrderError objektumok](#ordererror) listája. | A rendelési hibák gyűjteménye. |

## <a name="ordererror"></a>OrderError (Rendelési rendelés)

Olyan hibát jelez, amely a kosárból való ki- és kijelentkezés során fordul elő egy rendelés létrehozásakor.

| Tulajdonság     | Típus   | Leírás                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId (rendeléscsoport-azonosító) | sztring | A rendelési csoport azonosítója a hibával együtt. |
| code         | int    | A hibakód.                                 |
| leírás  | sztring | A hiba leírása.                   |
