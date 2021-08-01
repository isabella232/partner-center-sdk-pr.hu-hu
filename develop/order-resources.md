---
title: Erőforrások megrendelése
description: Egy partner akkor ad le rendelést, ha egy ügyfél egy ajánlatlistából szeretne előfizetést vásárolni.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 128c9e041cacc1c15f6187c4d99690d5c5fa4183
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009169"
---
# <a name="order-resources"></a>Erőforrások megrendelése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Egy partner akkor ad le rendelést, ha egy ügyfél egy ajánlatlistából szeretne előfizetést vásárolni.

>[!NOTE]
>Az Order erőforrás bérlőazonosítónként 500 kérés percenkénti sebességkorláttal rendelkezik.

## <a name="order"></a>Sorrend

Egy partner megrendelését írja le.

| Tulajdonság           | Típus                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| id                 | sztring                                             | A rendelés sikeres létrehozása után megadott rendelésazonosító.                                   |
| alternateId (alternatívazonosító)        | sztring                                             | A rendelés rövid azonosítója.                                                                          |
|referenceCustomerId | sztring                                             | Az ügyfél azonosítója. |
| billingCycle       | sztring                                             | Azt jelzi, hogy milyen gyakorisággal számlázták a partnert a rendelésért. A támogatott értékek a [BillingCycleType](product-resources.md#billingcycletype)típusban található tagnevek. Az alapértelmezett érték a "Havi" vagy a "OneTime" a rendelés létrehozásakor. Ez a mező a rendelés sikeres létrehozásakor lesz alkalmazva. |
| transactionType (tranzakciótípus)    | sztring                                             | Csak olvasható. A rendelés tranzakciótípusa. Támogatott értékek: UserPurchase, SystemPurchase vagy SystemBilling |
| lineItems (sorsorok)          | [OrderLineItem erőforrások tömbje](#orderlineitem) | Az ügyfél által megvásárolt ajánlatok elemi listája a mennyiséggel együtt.        |
| currencyCode       | sztring                                             | Csak olvasható. A rendelés leadáskor használt pénznem. A rendelés sikeres létrehozása után alkalmazva.           |
| currencySymbol     | sztring                                             | Csak olvasható. A pénznemkódhoz társított pénznemszimbólum. |
| creationDate (Létrehozás dátuma)       | dátum/idő                                           | Csak olvasható. A rendelés létrehozási dátuma, dátum-idő formátumban. A rendelés sikeres létrehozása után alkalmazva.                                   |
| status             | sztring                                             | Csak olvasható. A rendelés állapota.  A támogatott értékek az [**OrderStatus**](#orderstatus)oszlopban található tagnevek.        |
| Linkek              | [OrderLinks](utility-resources.md#resourcelinks)           | Az Order (Rendelés) erőforrás-hivatkozások.            |
| Attribútumok         | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Az Order attribútumnak megfelelő metaadat-attribútumok.       |

## <a name="orderlineitem"></a>OrderLineItem (Megrendelési vonal)

A rendelés az ajánlatok elemezett listáját tartalmazza, és minden elem OrderLineItemként van ábrázolva.

| Tulajdonság             | Típus                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber (sor száma)       | int                                       | A gyűjtemény minden soreleme egyedi sorszámot kap, amely 0-tól count-1-ig számol.                                                                                                                                                 |
| offerId (ajánlatazonosító)              | sztring                                    | Az ajánlat azonosítója.                                                                                                                                                                                                                       |
| subscriptionId       | sztring                                    | Az előfizetés azonosítója.                                                                                                                                                                                                                |
| parentSubscriptionId (parentSubscriptionId) | sztring                                    | Választható. A szülő-előfizetés azonosítója egy bővítményajánlatban. Csak a PATCH-re vonatkozik.                                                                                                                                                     |
| friendlyName (rövid név)         | sztring                                    | Választható. A partner által meghatározott előfizetés rövid neve a egyértelműséghez.                                                                                                                                              |
| quantity             | int                                       | A licencek vagy példányok száma.                                                                                                                                                                                |
| termDuration (kifejezés-lekértség)         | sztring                                    | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: **P1M (1** hónap), **P1Y (1** év) és **P3Y (3** év).                               |
| transactionType (tranzakciótípus)      | sztring                                    | Csak olvasható. A sortétel tranzakciótípusa. A támogatott értékek: "new", "renew", "addQuantity", "removeQuantity", "cancel", "convert" vagy "customerCredit". |
| partnerIdOnRecord    | sztring                                    | Ha egy közvetett szolgáltató egy közvetett viszonteladó nevében ad ki rendelést, akkor ezt a mezőt csak a közvetett viszonteladó MPN-azonosítójával **töltse** fel (soha ne a közvetett szolgáltató azonosítójával). Ez biztosítja az ösztönzők megfelelő elszámolását. |
| provisioningContext  | Szótár<sztring, sztring>            | A katalógus egyes elemeinek kiépítéséhez szükséges információk. A termékváltozat provisioningVariables tulajdonsága jelzi, hogy mely tulajdonságok szükségesek a katalógus adott elemeihez.                                                                                                                                               |
| Linkek                | [OrderLineItemLinks](#orderlineitemlinks) | Csak olvasható. A rendeléssor tételének megfelelő erőforrás-hivatkozások.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Megújítási időtartam részletei.                                                                           |
| AttestationAccepted             | logikai                 | Az ajánlatra vagy termékváltozatra vonatkozó feltételeket jelzi. Csak olyan ajánlatok vagy termékváltozatok esetén szükséges, ahol a SkuAttestationProperties vagy az OfferAttestationProperties enforceAttestation true (Igaz) érték.                                                                            |

## <a name="renewsto"></a>RenewsTo

A megújítási időszak időtartamának részleteit jelöli.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration (kifejezés-lekértség)          | sztring           | No              | A megújítási időszak időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a **P1M (1** hónap) és **a P1Y (1** év). |

## <a name="orderlinks"></a>OrderLinks

A rendelésnek megfelelő erőforrás-hivatkozásokat jelöli.

| Tulajdonság           | Típus                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Link](utility-resources.md#link)            | Ha ki van töltve, a rendelés kiépítési állapotának lekéréséhez szükséges hivatkozás.       |
| Önálló               | [Link](utility-resources.md#link)            | A rendelési erőforrás lekérését mutató hivatkozás.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

A rendeléshez társított teljes előfizetést jelöli.

| Tulajdonság           | Típus                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Link](utility-resources.md#link)            | Ha ki van töltve, [](#orderlineitemprovisioningstatus) a sorelem kiépítési állapotának lekéréséhez szükséges hivatkozás.       |
| Sku                | [Link](utility-resources.md#link)            | A megvásárolt katalóguselem termékváltozat-információinak lekérését mutató hivatkozás.                    |
| előfizetést       | [Link](utility-resources.md#link)            | Ha ki van töltve, a teljes előfizetési információra mutató hivatkozás.                       |
| activationLinks (aktiválási hivatkozás)    | [Link](utility-resources.md#link)            | A feltöltést az előfizetés aktiválásához szükséges hivatkozások GET erőforrása adja meg.             |

## <a name="orderstatus"></a>OrderStatus (Megrendelésiállapot)

Egy [Enum/dotnet/api/system.enum) értékekkel, amelyek a rendelés állapotát jelzik.

| Érték              | Pozíció     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| Ismeretlen            | 0            | Felsorolási inicializáló.                               |
| Befejezett          | 1            | Azt jelzi, hogy a rendelés befejeződött.          |
| függőben            | 2            | Azt jelzi, hogy a rendelés még függőben van.      |
| Törölt          | 3            | Azt jelzi, hogy a rendelés törölve lett.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

Egy [OrderLineItem kiépítési állapotát jelöli.](#orderlineitem)

| Tulajdonság                        | Típus                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber (sor száma)                  | int                                 | A rendeléssorelem egyedi sorszáma. Az értékek 0 és count-1 között vannak.             |
| status                          | sztring                              | A rendeléssorelem kiépítési állapota. Az értékek többek között az alábbiak lehetnek:</br>**Teljesítve:** A rendelés teljesítése sikeresen befejeződött, és a felhasználó használhatja a foglalásokat</br>**Nem teljesített:** A lemondás miatt nem teljesítve</br>**PrefulfillmentPending**: A kérés feldolgozása még folyamatban van, a teljesítés még nem fejeződött be |
| quantityProvisioningInformation | List<[QuantityProvisioningStatus](#quantityprovisioningstatus)> | A rendeléssorelemhez a mennyiség kiépítési állapotinformációinak listája. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

A kiépítési állapotot jelöli mennyiség szerint.

| Tulajdonság                           | Típus                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| quantity                           | int                                          | Az elemek száma.                                 |
| status                             | sztring                                       | Az elemek számának állapota.                   |
