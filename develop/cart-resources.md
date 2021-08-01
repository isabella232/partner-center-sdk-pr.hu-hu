---
title: Kocsierőforrások
description: A partnerek akkor rendelnek a kosárba, ha egy ügyfél egy ajánlatlistából szeretne előfizetést vásárolni.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ebe6e628d5bb3b66186d5c4f428f69e46415892b
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009144"
---
# <a name="cart-resources"></a>Kocsierőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A partner akkor ad le rendelést, ha egy ügyfél egy ajánlatlistából szeretne előfizetést vásárolni.

## <a name="cart"></a>Kosár

Egy kosarat ír le.

| Tulajdonság              | Típus             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | sztring           | A kosár sikeres létrehozása után megadott bevásárlókocsi-azonosító.                               |
| creationTimeStamp     | DateTime         | A kosár létrehozási dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva.      |
| lastModifiedTimeStamp | DateTime         | A kosár legutóbbi frissítésének dátuma, dátum-idő formátumban. A kosár sikeres létrehozása után alkalmazva. |
| expirationTimeStamp (lejárat/időstamp)   | DateTime         | A kosár lejáratának dátuma, dátum és idő formátumban. A kosár sikeres létrehozása után alkalmazva.          |
| lastModifiedUser      | sztring           | Az a felhasználó, aki utoljára frissítette a kosárat. A kosár sikeres létrehozása után alkalmazva.                          |
| lineItems (sorsorok)             | Objektumok tömbje | [CartLineItem-erőforrások tömbje.](#cartlineitem)                                                   |
| status                | sztring           | A kosár állapota. Lehetséges értékek: "Aktív" (frissíthető/elküldhető) és "Megrendelve" (már elküldve). |

## <a name="cartlineitem"></a>CartLineItem

Egy kosárban található elemet képvisel.

| Tulajdonság             | Típus                             | Description                                                                                                                                           |
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
| orderGroup           | sztring                           | Egy csoport, amely jelzi, hogy mely elemek együtt, ugyanabban a sorrendben elküldve.                                                                          |
| addonItems (bővítmények)           | **CartLineItem-objektumok** listája | Kosaras sorelemek gyűjteménye bővítményekhez. Ezeket az elemeket az alap előfizetéshez vásároljuk meg, amely a kosársori tétel vásárlásának eredménye. |
| error                | Objektum                           | A kosár létrehozása után lesz alkalmazva hiba esetén.                                                                                                    |
| renewsTo             | Objektumok tömbje                 | A [RenewsTo erőforrások tömbje.](#renewsto)                                                                            |
| AttestationAccepted (AttestationAccepted)             | logikai                 | Az ajánlati vagy termékváltozat-feltételekre vonatkozó szerződést jelzi. Csak olyan ajánlatokhoz vagy termékváltozatokhoz szükséges, ahol a SkuAttestationProperties vagy az OfferAttestationProperties enforceAttestation true (Igaz) érték.                                                                            |

## <a name="renewsto"></a>RenewsTo

Egy kosársorelemben található elemet képvisel.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration (kifejezés-lekértség)          | sztring           | No              | A megújítási időtartam ISO 8601-es ábrázolása. A jelenleg támogatott értékek a **P1M (1** hónap) és a **P1Y (1** év). |

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

## <a name="carterror"></a>CartError

Egy kosár létrehozása után jelentkező hibát jelez.

| Tulajdonság         | Típus                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CareErrorCode](#carterrorcode) | A kosárhiba típusa.                                                                       |
| errorDescription (hibaleíró) | sztring                                 | A hiba leírása, beleértve a támogatott értékekkel, alapértelmezett értékekkel vagy korlátokkal kapcsolatos megjegyzéseket. |


## <a name="carterrorcode"></a>CartErrorCode

A kosárhibák típusai.

| Name                             | ErrorCode   | Description
|----------------------------------|-------------|-----------------------------------------------------------------------------------------------|
| CurrencyIsNotSupported           | 10000   | A pénznem nem támogatott az adott piacon  |
| CatalogItemIdIsNotValid (CatalogItemIdIsNotValid)          | 10001   | A katalóguselem azonosítója érvénytelen  |
| QuotaNotAvailable (Kvóta nem érhető el)                | 10002   | Nem áll rendelkezésre elég kvóta  |
| InventoryNotAvailable (Leltár nem érhető el)            | 10003   | Az Inventory nem érhető el a kiválasztott ajánlathoz  |
| ParticipantsIsNotSupportedForPartner  | 10004   | A résztvevők beállítása nem támogatott a Partnerhez  |
| UnableToProcessCartLineItem      | 10006   | A kocsisorelem feldolgozása nem sikerült.  |
| SubscriptionIsNotValid (SubscriptionIsNotValid)           | 10007   | Az előfizetés érvénytelen.  |
| SubscriptionIsNotEnabledForRI    | 10008   | Az előfizetés nem engedélyezett a RI-vásárláshoz.  |
| SandboxLimitExceeded             | 10009   | Túllépte a védőfal korlátját.  |
| InvalidInput (Érvénytelen átviteli sebesség)                     | 10010   | Az általános bemenet érvénytelen.  |
| SubscriptionNotRegistered        | 10011   | Az előfizetés érvénytelen.  |
| AttestationNotAccepted           | 10012   | Az igazolás nem lett elfogadva.  |
| Ismeretlen                          | 0   | Alapértelmezett érték   |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

A kosárból való ki- és kijelentkezés eredményét jelöli.

| Tulajdonság    | Típus                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| rendelések      | Az Order [objektumok](order-resources.md#order) listája.         | A rendelések gyűjteménye.       |
| orderErrors | Az [OrderError objektumok](#ordererror) listája. | A rendelési hibák gyűjteménye. |

## <a name="ordererror"></a>OrderError

Olyan hibát jelez, amely a kosárból való ki- és kijelentkezés során fordul elő egy rendelés létrehozásakor.

| Tulajdonság     | Típus   | Description                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId (rendeléscsoport-azonosító) | sztring | A rendelési csoport azonosítója a hibával együtt. |
| code         | int    | A hibakód.                                 |
| leírás  | sztring | A hiba leírása.                   |
