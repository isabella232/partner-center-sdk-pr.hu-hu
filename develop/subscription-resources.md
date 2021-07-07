---
title: Előfizetési erőforrások
description: Az előfizetési erőforrások további információkat nyújthatnak az előfizetésekkel kapcsolatban az életciklus során, például támogatást, visszatérítéseket és Azure-jogosultságokat.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35d8c86ab061797109b3c152eff02f354b7ea23a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547453"
---
# <a name="subscription-resources"></a>Előfizetési erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az előfizetéssel az ügyfél egy bizonyos ideig használhatja a szolgáltatást. Nem minden mező vonatkozik az összes előfizetésre. Számos mező csak az életciklus bizonyos pontjain érvényes, például ha egy előfizetés fel van függesztve vagy törölve van.

## <a name="subscription"></a>Előfizetés

>[!NOTE]
>Az **Előfizetés** erőforrás sebességkorlátja bérlőazonosítónként percenként 500 kérés.

Az **Előfizetés** erőforrás az előfizetés életciklusát jelöli, és olyan tulajdonságokat tartalmaz, amelyek meghatározzák az előfizetés teljes életciklusának államát.

| Tulajdonság             | Típus                                                          | Leírás                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | sztring                                                        | Az előfizetés azonosítója.                                                                                                                                                  |
| offerId (ajánlatazonosító)              | sztring                                                        | Az ajánlat azonosítója.                                                                                                                                                         |
| entitlementId (jogosultságazonosító)        | sztring                                                        | A jogosultságazonosító (egy Azure-előfizetés azonosítója).                                                                                                                        |
| offerName (ajánlat neve)            | sztring                                                        | Az ajánlat neve.                                                                                                                                                               |
| friendlyName (rövid név)         | sztring                                                        | A partner által meghatározott előfizetés rövid neve, amely segít az egyértelműsségben.                                                                                           |
| quantity             | szám                                                        | A mennyiség. Licencalapú számlázás esetén például ez a tulajdonság a licencszámra van beállítva.                                                            |
| unitType (egységtípus)             | sztring                                                        | Az előfizetéshez mennyiséget meghatározó egységek.                                                                                                                             |
| parentSubscriptionId (parentSubscriptionId) | sztring                                                        | Lekért vagy beállítja a szülő-előfizetés azonosítóját.                                                                                                                              |
| creationDate (Létrehozás dátuma)         | sztring                                                        | Lekért vagy beállítja a létrehozás dátumát dátum-idő formátumban.                                                                                                                          |
| effectiveStartDate   | sztring UTC dátum- és időformátumban                                | Lekért vagy beállítja az előfizetés hatályba vonatkozó kezdődátumát dátum-idő formátumban. A migrált előfizetések dátumának vagy egy másik előfizetéshez való igazítására használható.                |
| commitmentEndDate (kötelezettségvállalási deddátum)    | sztring UTC dátum- és időformátumban                                | Az előfizetés kötelezettségvállalási záró dátuma, dátum-idő formátumban. A nem automatikusan megújítható előfizetések esetén ez egy távoli dátumot jelent a jövőben.       |
| status               | sztring                                                        | Az előfizetés állapota: "nincs", "aktív", "függőben", "felfüggesztve" vagy "törölve".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Lekért egy értéket, amely jelzi, hogy az előfizetés automatikusan megújul-e.                                                                                                    |
| billingType (számlázási típus)          | sztring                                                        | Az előfizetés számlázásának a megadása: "nincs", "használat" vagy "licenc".                                                                                                      |
| billingCycle         | sztring                                                        | Azt jelzi, hogy milyen gyakorisággal számlázták a partnert a rendelésért. A támogatott értékek a [**BillingCycleType**](product-resources.md#billingcycletype)típusban található tagnevek. |
| hasPurchasableAddons | boolean                                                       | Lekért vagy beállítja azt az értéket, amely jelzi, hogy az előfizetés rendelkezik-e letölthető bővítményekkel.                                                                                             |
| isTrial (isTrial)              | boolean                                                       | Egy érték, amely jelzi, hogy próbaverziós előfizetésről van-e szó.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Egy érték, amely jelzi, hogy ez egy Microsoft-termék-e.                                                                                                                       |
| publisherName        | sztring                                                        | A közzétevő neve.                                                                                                                                                           |
| műveletek              | sztringek tömbje                                              | Lekért vagy beállítja az engedélyezett műveleteket. Lehetséges értékek: "szerkesztés", "megszakítás"                                                                                                  |
| partnerazonosító            | sztring                                                        | A közvetett partnermodellben használt rekord viszonteladójának MPN-azonosítója.                                                                                                     |
| felfüggesztésReasons    | sztringek tömbje                                              | Csak olvasható. Ha az előfizetés fel lett függesztve, azt jelzi, hogy miért.                                                                                                                  |
| contractType (szerződéstípus)         | sztring                                                        | Csak olvasható. A szerződés típusa: "subscription", "productKey" vagy "redemptionCode".                                                                                           |
| refundOptions (visszatérítésilehetőségek)        | [RefundOption erőforrások tömbje](#refundoption)   | Csak olvasható. Az előfizetéshez elérhető visszatérítési lehetőségek készlete.                                                                                              |
| Linkek                | [SubscriptionLinks (Előfizetés-hivatkozás)](#subscriptionlinks)                       | Lekért vagy beállítja az előfizetési hivatkozásokat.                                                                                                                                          |
| orderId (rendelésazonosító)              | sztring                                                        | Az előfizetés megkezdéséhez lekért rendelés azonosítója.                                                                                                                |
| termDuration (kifejezés-lekértség)         | sztring                                                        | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek: **P1M (1** hónap), **P1Y (1** év) és **P3Y (3** év).                                                        |
| Attribútumok           | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Az előfizetéshez tartozó metaadat-attribútumok.                                                                                                                    |
| renewalTermDuration (megújítási időszak)  | sztring                                                        | A kifejezés időtartamának ISO 8601-es ábrázolása. A jelenleg támogatott értékek a **P1M (1** hónap) és a **P1Y (1** év).                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks (Előfizetés-hivatkozás)

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

A **SubscriptionProvisioningStatus erőforrás** információkat nyújt az előfizetések kiépítési állapotáról.

| Tulajdonság   | Típus                                                           | Leírás                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId (termékváltozatazonosító)      | sztring                                                         | Egy GUID formátumú sztring, amely azonosítja a termékváltozatot.             |
| status     | sztring                                                         | A kiépítés állapotát jelzi: "sikeres", "függőben" vagy "sikertelen". |
| quantity   | szám                                                         | A kiépítést követően az előfizetés mennyiségét biztosítja.               |
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

## <a name="registersubscription"></a>RegisterSubscription (Regisztráció regisztrálása)

A **RegisterSubscription erőforrás** egy hivatkozást ad vissza, amely egy előfizetés regisztrációs állapotának lekérdezésére használható. A regisztrációs állapotot egy, az Azure-előfizetés regisztrálására vonatkozó, sikeresen elfogadott kérés válasz törzse visszaadja.

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
