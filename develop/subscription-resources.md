---
title: Előfizetés erőforrásai
description: Az előfizetések erőforrásai további információkat biztosíthatnak az előfizetésekről a életciklus során, például a támogatás, a visszatérítések, az Azure-jogosultságok.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd835e46e99b1fcb1e0b0e694ad73b1dca1240c9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767851"
---
# <a name="subscription-resources"></a>Előfizetés erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az előfizetés lehetővé teszi, hogy az ügyfelek bizonyos ideig használják a szolgáltatást. Nem minden mező fog vonatkozni az összes előfizetésre. Számos mező csak a életciklus bizonyos pontjain érvényes, például ha egy előfizetés fel van függesztve vagy meg lett szakítva.

## <a name="subscription"></a>Előfizetés

>[!NOTE]
>Az **előfizetési** erőforráshoz a bérlői azonosítók száma percenként 500 kérelem.

Az **előfizetési** erőforrás az előfizetés életciklusát jelöli, és olyan tulajdonságokat tartalmaz, amelyek meghatározzák az állapotokat az előfizetési életciklusa során.

| Tulajdonság             | Típus                                                          | Leírás                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sztring                                                        | Az előfizetés azonosítója.                                                                                                                                                  |
| offerId              | sztring                                                        | Az ajánlat azonosítója.                                                                                                                                                         |
| entitlementId        | sztring                                                        | A jogosultsági azonosító (egy Azure-előfizetési azonosító).                                                                                                                        |
| offerName            | sztring                                                        | Az ajánlat neve.                                                                                                                                                               |
| friendlyName         | sztring                                                        | A partner által az előfizetéshez megadott rövid név, amely segít a egyértelműsítse.                                                                                           |
| quantity             | szám                                                        | A mennyiség. Licenc alapú számlázás esetén például ez a tulajdonság a licencek száma értékre van állítva.                                                            |
| unitType             | sztring                                                        | Az előfizetés mennyiségét meghatározó egység.                                                                                                                             |
| parentSubscriptionId | sztring                                                        | Lekérdezi vagy beállítja a szülő-előfizetés azonosítóját.                                                                                                                              |
| creationDate         | sztring                                                        | Lekérdezi vagy beállítja a létrehozási dátumot dátum és idő formátumban.                                                                                                                          |
| effectiveStartDate   | karakterlánc UTC-dátum időformátuma                                | Lekérdezi vagy beállítja az előfizetés érvényes kezdő dátumát a dátum-idő formátumban. A rendszer az áttelepített előfizetés dátumának vagy egy másikkal való igazításának időpontját használja.                |
| commitmentEndDate    | karakterlánc UTC-dátum időformátuma                                | Az előfizetéshez tartozó kötelezettségvállalási befejezési dátum dátum-idő formátumban. A nem automatikus megújítható előfizetések esetében ez a dátum a jövőben jóval távolabbi.       |
| status               | sztring                                                        | Az előfizetés állapota: "None", "Active", "függőben", "Felfüggesztve" vagy "törölve".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Egy érték beolvasása, amely azt jelzi, hogy az előfizetés automatikusan megújul-e.                                                                                                    |
| billingType          | sztring                                                        | Megadja az előfizetés számlázásának módját: "None", "használat" vagy "licenc".                                                                                                      |
| billingCycle         | sztring                                                        | Azt jelzi, hogy milyen gyakorisággal történik a partner számlázása ebben a sorrendben. A támogatott értékek a [**BillingCycleType**](product-resources.md#billingcycletype)található tagok nevei. |
| hasPurchasableAddons | boolean                                                       | Lekérdezi vagy beállítja azt a értéket, amely azt jelzi, hogy az előfizetés tartalmaz-e megvásárolható bővítményeket.                                                                                             |
| Isztriai              | boolean                                                       | Egy érték, amely azt jelzi, hogy a próbaverziós előfizetés.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Egy érték, amely azt jelzi, hogy ez egy Microsoft-termék.                                                                                                                       |
| publisherName        | sztring                                                        | A közzétevő neve.                                                                                                                                                           |
| műveletek              | sztringek tömbje                                              | Lekérdezi vagy beállítja az engedélyezett műveleteket. Lehetséges értékek: "szerkesztés", "Mégse"                                                                                                  |
| partnerId            | sztring                                                        | A közvetett partner modelljében használt rekord-viszonteladó MPN-azonosítója.                                                                                                     |
| suspensionReasons    | sztringek tömbje                                              | Csak olvasható. Ha az előfizetés fel lett függesztve, az azt jelzi, hogy miért.                                                                                                                  |
| contractType         | sztring                                                        | Csak olvasható. A szerződés típusa: "előfizetés", "termék" vagy "redemptionCode".                                                                                           |
| refundOptions        | [RefundOption](#refundoption) -erőforrások tömbje   | Csak olvasható. Az előfizetéshez elérhető visszatérítési lehetőségek készlete.                                                                                              |
| linkek                | [SubscriptionLinks](#subscriptionlinks)                       | Lekérdezi vagy beállítja az előfizetés hivatkozásait.                                                                                                                                          |
| Rendeléskód              | sztring                                                        | Az előfizetés megkezdéséhez elhelyezett sorrend azonosítója.                                                                                                                |
| termDuration         | sztring                                                        | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: **P1M** (1 hónap), **P1Y** (1 év) és **P3Y** (3 év).                                                        |
| attribútumok           | [ResourceAttributes](utility-resources.md#resourceattributes) | Az előfizetéshez tartozó metaadat-attribútumok.                                                                                                                    |
| renewalTermDuration  | sztring                                                        | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a következők: **P1M** (1 hónap) és **P1Y** (1 év).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

A **SubscriptionLinks** erőforrás ismerteti az előfizetési erőforrásokhoz csatolt hivatkozások gyűjteményét.

| Tulajdonság           | Típus                               | Leírás                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Hivatkozás](utility-resources.md#link) | Lekérdezi vagy beállítja az ajánlatot.               |
| parentSubscription | [Hivatkozás](utility-resources.md#link) | Lekérdezi vagy beállítja a szülő-előfizetést. |
| product            | [Hivatkozás](utility-resources.md#link) | Az előfizetéshez társított termék beolvasása. |
| SKU                | [Hivatkozás](utility-resources.md#link) | Az előfizetéshez társított termék SKU beolvasása. |
| availability       | [Hivatkozás](utility-resources.md#link) | Az előfizetéshez társított termék SKU-elérhetőségének beolvasása. |
| activationLinks    | [Hivatkozás](utility-resources.md#link) | Az előfizetéshez társított aktiválási hivatkozások listájának beolvasása. |
| önálló               | [Hivatkozás](utility-resources.md#link) | A saját URI-ja.                         |
| következő               | [Hivatkozás](utility-resources.md#link) | Az elemek következő lapja.               |
| korábbi           | [Hivatkozás](utility-resources.md#link) | Az elemek előző lapja.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

A **SubscriptionProvisioningStatus** -erőforrás információt nyújt az előfizetés kiépítési állapotáról.

| Tulajdonság   | Típus                                                           | Leírás                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | sztring                                                         | Egy GUID formátumú karakterlánc, amely a termék SKU azonosítóját azonosítja.             |
| status     | sztring                                                         | A kiépítési állapotot jelzi: "sikeres", "függőben" vagy "sikertelen". |
| quantity   | szám                                                         | Az előfizetés mennyiségét adja meg a kiépítés után.               |
| endDate    | karakterlánc UTC-dátum időformátuma                                 | Az előfizetés befejező dátuma.                                    |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

A **SubscriptionRegistrationStatus** erőforrás ismerteti az előfizetési erőforrásokhoz csatolt hivatkozások gyűjteményét.

| Tulajdonság           | Típus                               | Leírás                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | sztring                             | Az előfizetés azonosítója.                                                          |
| status             | sztring                             | A regisztrációs állapotot jelzi: "Registered", "Registering" vagy "notregistered".    |

## <a name="supportcontact"></a>SupportContact

A **SupportContact** -erőforrás az ügyfél előfizetésének támogatási kapcsolattartóját jelöli.

| Tulajdonság        | Típus                                                           | Leírás                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | sztring                                                         | Egy GUID formátumú karakterlánc, amely a támogatási partner bérlői azonosítóját jelzi. |
| supportMpnId    | sztring                                                         | A partner Microsoft Partner Network (MPN) azonosítója.                       |
| name            | sztring                                                         | A támogatási kapcsolattartó neve.                                                |
| linkek           | [ResourceLinks](utility-resources.md#resourcelinks)            | A támogatási partnerekkel kapcsolatos hivatkozások.                                              |
| attribútumok      | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai. A "objektumtípus": "SupportContact" kifejezést tartalmazza.              |

## <a name="registersubscription"></a>RegisterSubscription

A **RegisterSubscription** erőforrás egy hivatkozást ad vissza, amely az előfizetés regisztrációs állapotának lekérdezésére használható. Az Azure-előfizetések regisztrálására vonatkozó kérelem sikeres elfogadása esetén a rendszer a regisztrációs állapotot adja vissza.

| Tulajdonság                | Típus                               | Leírás                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Az "elfogadva" HTTP-202 állapotkódot adja vissza, amely egy, a regisztrációs állapot lekérdezésére szolgáló hivatkozást tartalmazó Location fejlécet tartalmaz. Például: `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

A **RefundOption** erőforrás az előfizetés lehetséges visszatérítési lehetőségét jelöli.

| Tulajdonság          | Típus | Leírás                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| típus | sztring | A visszatérítés típusa. A támogatott értékek a következők: "részleges" és "teljes" |
| expiresAfter      | karakterlánc UTC-dátum időformátuma | A beállítás lejárati időbélyege. Null érték esetén ez azt jelenti, hogy nincs lejárata. |

## <a name="azureentitlement"></a>AzureEntitlement

A **AzureEntitlement** erőforrás az előfizetés Azure-jogosultságait jelöli.

| Tulajdonság          | Típus | Leírás                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | sztring | A jogosultsági azonosító |
| friendlyName      | sztring | A jogosultság rövid neve. |
| status | sztring | A jogosultság állapota. |
| subscriptionId | sztring | A jogosultsághoz tartozó előfizetés-azonosító. |
