---
title: Előfizetési erőforrások
description: Az előfizetési erőforrások további információkat nyújthatnak az előfizetésekkel kapcsolatban az életciklus során, például támogatást, visszatérítéseket és Azure-jogosultságokat.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 461df9cdb909fc44be9069cb7eb4b41fa2a5f170
ms.sourcegitcommit: 3ee00d9fe9da6b9df0fb7027ae506e2abe722770
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/04/2021
ms.locfileid: "129417287"
---
# <a name="subscription-resources"></a>Előfizetési erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az előfizetéssel az ügyfél egy bizonyos ideig használhatja a szolgáltatást. Nem minden mező vonatkozik az összes előfizetésre. Számos mező csak az életciklus bizonyos pontjain érvényes, például ha egy előfizetés fel van függesztve vagy törölve van.

## <a name="subscription"></a>Előfizetés

>[!NOTE]
>Az **Előfizetés** erőforrás sebességkorlátja bérlőazonosítónként percenként 500 kérés.

Az **Előfizetés** erőforrás az előfizetés életciklusát jelöli, és olyan tulajdonságokat tartalmaz, amelyek meghatározzák az előfizetés életciklusának államát.

| Tulajdonság             | Típus                                                          | Leírás                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sztring                                                        | Az előfizetés azonosítója.                                                                                                                                                  |
| offerId (ajánlatazonosító)              | sztring                                                        | Az ajánlat azonosítója.                                                                                                                                                         |
| entitlementId (jogosultságazonosító)        | sztring                                                        | A jogosultságazonosító (egy Azure-előfizetés azonosítója).                                                                                                                        |
| offerName (ajánlat neve)            | sztring                                                        | Az ajánlat neve.                                                                                                                                                               |
| friendlyName (rövid név)         | sztring                                                        | A partner által meghatározott előfizetés rövid neve, amely segít egyértelműsedni.                                                                                           |
| quantity             | szám                                                        | A mennyiség. Licencalapú számlázás esetén például ez a tulajdonság a licencszámra van beállítva.                                                            |
| unitType (egységtípus)             | sztring                                                        | Az előfizetéshez mennyiséget meghatározó egységek.                                                                                                                             |
| parentSubscriptionId (parentSubscriptionId) | sztring                                                        | Lekért vagy beállítja a szülő-előfizetés azonosítóját.                                                                                                                              |
| creationDate (Létrehozás dátuma)         | sztring                                                        | Lekért vagy beállítja a létrehozás dátumát dátum-idő formátumban.                                                                                                                          |
| effectiveStartDate   | sztring UTC dátum- és időformátumban                                | Lekért vagy beállítja az előfizetés hatályba vonatkozó kezdődátumát dátum-idő formátumban. A migrált előfizetések dátumának vagy egy másik előfizetéshez való igazítására használható.                |
| commitmentEndDate (kötelezettségvállalási deddátum)    | sztring UTC dátum- és időformátumban                                | Az előfizetés kötelezettségvállalási záró dátuma dátum-idő formátumban. A nem automatikusan megújítható előfizetések esetén ez egy távoli, távoli dátumot jelent a jövőben.       |
| status               | sztring                                                        | Az előfizetés állapota: "nincs", "aktív", "függő", "felfüggesztve", "lejárt" vagy "törölve".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Lekért egy értéket, amely jelzi, hogy az előfizetés automatikusan megújul-e.                                                                                                    |
| billingType (számlázási típus)          | sztring                                                        | Azt adja meg, hogy az előfizetés hogyan számlázható: "nincs", "használat" vagy "licenc".                                                                                                      |
| billingCycle (számlázási ciklus)         | sztring                                                        | Azt jelzi, hogy milyen gyakorisággal számlázták a partnert a rendelésért. A támogatott értékek a [**BillingCycleType**](product-resources.md#billingcycletype)típusban található tagnevek. |
| hasPurchasableAddons | boolean                                                       | Lekért vagy beállítja azt az értéket, amely jelzi, hogy az előfizetés rendelkezik-e letölthető bővítményekkel.                                                                                             |
| isTrial (isTrial)              | boolean                                                       | Egy érték, amely jelzi, hogy próbaverziós előfizetésről van-e szó.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Egy érték, amely jelzi, hogy ez egy Microsoft-termék-e.                                                                                                                       |
| publisherName        | sztring                                                        | A közzétevő neve.                                                                                                                                                           |
| műveletek              | sztringek tömbje                                              | Lekérte vagy beállítja az engedélyezett műveleteket. Lehetséges értékek: "szerkesztés", "megszakítás"                                                                                                  |
| partnerazonosító            | sztring                                                        | A közvetett partnermodellben használt rekord viszonteladójának MPN-azonosítója.                                                                                                     |
| felfüggesztésReasons    | sztringek tömbje                                              | Csak olvasható. Ha az előfizetés fel lett függesztve, azt jelzi, hogy miért.                                                                                                                  |
| contractType (szerződéstípus)         | sztring                                                        | Csak olvasható. A szerződés típusa: "subscription", "productKey" vagy "redemptionCode".                                                                                           |
| refundOptions (visszatérítésilehetőségek)        | [RefundOption erőforrások tömbje](#refundoption)   | Csak olvasható. Az előfizetéshez elérhető visszatérítési lehetőségek készlete.                                                                                              |
| Linkek                | [SubscriptionLinks (Előfizetési hivatkozás)](#subscriptionlinks)                       | Lekérte vagy beállítja az előfizetési hivatkozásokat.                                                                                                                                          |
| orderId (rendelésazonosító)              | sztring                                                        | Az előfizetés megkezdéséhez lekért rendelés azonosítója.                                                                                                                |
| termDuration (kifejezés-lekértség)         | sztring                                                        | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: **P1M (1** hónap), **P1Y (1** év) és **P3Y (3** év).                                                        |
| Attribútumok           | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Az előfizetéshez tartozó metaadat-attribútumok.                                                                                                                    |
| renewalTermDuration (megújítási időszak)  | sztring                                                        | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a **P1M (1** hónap) és a **P1Y (1** év).                                                        |
| ProductType (Terméktípus)  | [Itemtype](product-resources.md#itemtype)                             | Csak olvasható. Az előfizetésben érintett termék típusa.     |
| consumptionType (felhasználási típus)  | [túlóra-erőforrások tömbje](subscription-resources.md#overage)   | Lekért vagy beállítja egy adott ügyfél túlóra-beállítását.     |

## <a name="subscriptionlinks"></a>SubscriptionLinks (Előfizetési hivatkozás)

A **SubscriptionLinks erőforrás** az előfizetési erőforráshoz csatolt hivatkozások gyűjteményét ismerteti.

| Tulajdonság           | Típus                               | Leírás                           |
|--------------------|------------------------------------|---------------------------------------|
| offer              | [Link](utility-resources.md#link) | Lekérte vagy beállítja az ajánlatot.               |
| parentSubscription (parentSubscription) | [Link](utility-resources.md#link) | Lekérte vagy beállítja a szülő-előfizetést. |
| product            | [Link](utility-resources.md#link) | Lekérte az előfizetéshez társított terméket. |
| Sku                | [Link](utility-resources.md#link) | Lekérte az előfizetéshez társított termékváltozatot. |
| availability       | [Link](utility-resources.md#link) | Lekérte az előfizetéshez társított termékváltozat rendelkezésre állását. |
| activationLinks (aktiválási hivatkozás)    | [Link](utility-resources.md#link) | Lekérte az előfizetéshez társított aktiválási hivatkozások listáját. |
| Önálló               | [Link](utility-resources.md#link) | Az ön-URI.                         |
| Következő               | [Link](utility-resources.md#link) | Az elemek következő oldala.               |
| Előző           | [Link](utility-resources.md#link) | Az elemek előző oldala.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

A **SubscriptionProvisioningStatus erőforrás** az előfizetés kiépítési állapotával kapcsolatos információkat biztosít.

| Tulajdonság   | Típus                                                           | Leírás                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId (termékváltozatazonosító)      | sztring                                                         | Egy GUID formátumú sztring, amely azonosítja a termékváltozatot.             |
| status     | sztring                                                         | A kiépítés állapotát jelzi: "sikeres", "függőben" vagy "sikertelen". |
| quantity   | szám                                                         | A kiépítést követően az előfizetési mennyiséget biztosítja.               |
| endDate (záródátum)    | sztring UTC dátum- és időformátumban                                 | Az előfizetés záró dátuma.                                    |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

A **SubscriptionRegistrationStatus** erőforrás az előfizetési erőforráshoz csatolt hivatkozások gyűjteményét ismerteti.

| Tulajdonság           | Típus                               | Leírás                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | sztring                             | Az előfizetés azonosítója.                                                          |
| status             | sztring                             | A regisztráció állapotát jelzi: "registered", "registering" vagy "notregistered".    |

## <a name="supportcontact"></a>Támogatásicontact

A **SupportContact** erőforrás egy támogatási kapcsolattartót jelent az ügyfél előfizetéséhez.

| Tulajdonság        | Típus                                                           | Leírás                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | sztring                                                         | Egy GUID formátumú sztring, amely a támogatási kapcsolattartó bérlőazonosítóját jelzi. |
| supportMpnId    | sztring                                                         | A kapcsolattartó Microsoft Partner Network (MPN) azonosítója.                       |
| name            | sztring                                                         | A támogatási kapcsolattartó neve.                                                |
| Linkek           | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)            | A támogatási kapcsolattartóval kapcsolatos hivatkozások.                                              |
| Attribútumok      | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok. Tartalmazza az "objectType": " SupportContact" adatokat.              |

## <a name="overage"></a>Overage (Kereten túli díjak)

A **túlóra-erőforrás** azt jelenti, hogy a használaton keresztüli előfizetés-túlfelhasználás hozzárendelhető, függetlenül attól, hogy az előfizetés hozzá van-e rendelve, és a Viszonteladóhoz van-e rendelve.

| Tulajdonság        | Típus               | Leírás                                                                     |
|-----------------|--------------------|---------------------------------------------------------------------------------|
| azureEntitlementId | sztring       | Egy GUID formátumú sztring, amely használat alapján megadott előfizetés-azonosítót jelez. |
| partnerazonosító    | sztring            | Az Microsoft Partner Network előfizetéshez társított viszonteladó Microsoft Partner Network (MPN) azonosítóját.        |
| típus    | sztring       | A túlóra típusa lehet "PhoneServices"       |
| túl sok            | boolean      | Egy érték, amely jelzi, hogy engedélyezve van-e a túlóra.       |
| Linkek           | [ResourceLinks (Erőforrás-hivatkozás)](utility-resources.md#resourcelinks)            | A túl sok idővel kapcsolatos hivatkozások.                          |
| Attribútumok      | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok. Tartalmazza az "objectType": "Overage" (Túl sok) tulajdonságot.  |



## <a name="registersubscription"></a>RegisterSubscription (Regisztráció regisztrálása)

A **RegisterSubscription erőforrás** egy hivatkozást ad vissza, amely egy előfizetés regisztrációs állapotának lekérdezésére használható. A regisztrációs állapotot a rendszer visszaadja egy Azure-előfizetés regisztrálására vonatkozó, sikeresen elfogadott kérelem válasz törzsében.

| Tulajdonság                | Típus                               | Leírás                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | A 202 -es "Elfogadva" HTTP-állapotkódot adja vissza, a regisztrációs állapot lekérdezésére mutató hivatkozást tartalmazó Location fejléccel. Például: `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption (Visszatérítési beállítás)

A **RefundOption** erőforrás egy lehetséges visszatérítési lehetőséget jelent az előfizetéshez.

| Tulajdonság          | Típus | Leírás                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| típus | sztring | A visszatérítés típusa. A támogatott értékek a "Partial" (Részleges) és a "Full" (Teljes) |
| expiresAfter      | sztring UTC dátum-idő formátumban | A beállítás lejáratának időbélyege. Ha null értékű, az azt jelenti, hogy nincs lejárati ideje. |

## <a name="azureentitlement"></a>AzureEntitlement

Az **AzureEntitlement erőforrás** az előfizetésHez szükséges Azure-jogosultságokat jelöli.

| Tulajdonság          | Típus | Leírás                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | sztring | A jogosultságazonosító |
| friendlyName (rövid név)      | sztring | A jogosultság rövid neve. |
| status | sztring | A jogosultság állapota. |
| subscriptionId | sztring | Az előfizetés azonosítója, amelyhez a jogosultság tartozik. |
