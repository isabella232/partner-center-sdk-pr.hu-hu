---
title: Előfizetés használati erőforrásai
description: Az előfizetés használati erőforrásai a használatalapú számlázással kapcsolatos előfizetéseket írják le. Ezek az előfizetések napi és havi használati rekordokkal, valamint az egyes fizetési időszakra vonatkozó használati adatok összegzésével vannak.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8af4e9b8a4660b5bc9d287ece258dca9aa9ba7a749cfdc89e9c9b47e4af61b1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990273"
---
# <a name="subscription-usage-resources"></a>Előfizetés használati erőforrásai

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A következő előfizetési használati erőforrások használatával lekért használati adatokat kaphat egy adott, használatalapú számlázással kapcsolatos előfizetéshez. Ezek az előfizetések napi és havi használati rekordokkal, valamint az egyes fizetési időszakra vonatkozó használati adatok összegzésével vannak.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*A **SubscriptionDailyUsageRecord** erőforrás elavult, és pontatlan eredményeket eredményezhet. Javasoljuk, hogy frissítse az alkalmazásait úgy, hogy azok az ügyfél Azure-beli kihasználtsági rekordjainak lekért és a szolgáltatásért Microsoft Azure [API-kat](get-prices-for-microsoft-azure.md) használják. [](get-a-customer-s-utilization-record-for-azure.md)*

A **SubscriptionDailyUsageRecord** erőforrás azt írja le, hogy egy adott nap mennyi előfizetést használ fel.

| Tulajdonság         | Típus               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed (Dátum)         | sztring             | A nap, dátum-idő formátumban, amikor az előfizetést használták.                                 |
| ResourceId       | sztring             | Guid. Az erőforrás egyedi azonosítója.                                                          |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve.                                                                     |
| TotalCost (Teljes költség)        | tizedes tört             | Az előfizetésben található erőforrások használatának becsült teljes költsége a megadott napon.     |
| CurrencyLocale   | sztring             | A területi beállítás, amelyben az előfizetést használták, meghatározza a számlán használni szükséges pénznemet. |
| LastModifiedDate | sztring             | A dátum és idő formátumban a rekord utolsó módosításának napja.                             |
| Attribútumok       | ResourceAttributes (Erőforrás-attribútumok) | Az erőforrásnak megfelelő metaadat-attribútumok.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

A **SubscriptionMonthlyUsageRecord** erőforrás azt írja le, hogy egy adott hónapban mennyi előfizetést használtak fel.

| Tulajdonság         | Típus               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Állapot           | sztring             | Az előfizetés állapota: "nincs", "aktív", "felfüggesztve" vagy "törölve".                  |
| PartnerOnRecord  | sztring             | "A rekordban van a partner MPN-azonosítója."                                                        |
| OfferId (Ajánlatazonosító)          | sztring             | Guid. Az előfizetéshez kapcsolódó ajánlat azonosítója.                                       |
| Id               | sztring             | Guid. Az előfizetés vagy erőforrás azonosítója.                                                 |
| Name             | sztring             | Az előfizetés vagy erőforrás neve.                                                     |
| TotalCost (Teljes költség)        | tizedes tört             | Az előfizetésben található erőforrások használatának becsült teljes költsége a megadott hónapban.   |
| CurrencyLocale   | sztring             | A területi beállítás, amelyben az előfizetést használták, meghatározza a számlán használni szükséges pénznemet. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetéshez. |
| CurrencyCode     | sztring             | Lekért vagy beállítja a pénznemkódot. Elérhető az Azure-csomag előfizetési erőforrásaihoz.                                         |
| USDTotalCost (UsdTotalCost)     | tizedes tört             | Lekért vagy beállítja a becsült teljes költséget USD-ben. Elérhető Azure-csomagokhoz.                                         |
| LastModifiedDate | sztring             | A dátum és idő formátumban a rekord utolsó módosításának napja.                             |
| Attribútumok       | ResourceAttributes (Erőforrás-attribútumok) | Az erőforrásnak megfelelő metaadat-attribútumok.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

A **SubscriptionUsageSummary** erőforrás azt írja le, hogy mennyi előfizetés volt használatban az aktuális számlázási időszakban.

| Tulajdonság         | Típus               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | sztring             | Guid. Az előfizetés vagy erőforrás azonosítója. A CustomerMonthlyUsageRecord környezetben ez az azonosító az ügyfél azonosítója. |
| ResourceName nevű erőforrásáról     | sztring             | Az előfizetés vagy erőforrás neve. A CustomerMonthlyUsageRecord kontextusában ez az ügyfél neve. |
| BillingStartDate (Számlázási kezdő dátum) | dátum               | Az aktuális számlázási időszak kezdő dátuma, dátum-idő formátumban.                                                     |
| BillingEndDate (Számlázási dátum)   | dátum               | Az aktuális számlázási időszak záró dátuma, dátum-idő formátumban.                                                       |
| TotalCost (Teljes költség)        | double             | Az előfizetésben található erőforrások használatának becsült teljes költsége a megadott számlázási időszakban.               |
| CurrencyLocale   | sztring             | Az előfizetés használatának területi beállítása határozza meg a számlán használni szükséges pénznemet. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetéshez. |
| CurrencyCode   | sztring             | Lekért vagy beállítja a pénznemkódot. Elérhető Azure-csomagokhoz.                                         |
| USDTotalCost   | tizedes tört             | Lekért vagy beállítja a becsült teljes költséget USD-ben. Elérhető az Azure-csomag előfizetési erőforrásaihoz.                                         |
| LastModifiedDate | sztring             | A rekord utolsó módosításának dátuma és ideje formátumban.                                                      |
| Hivatkozások            | ResourceLinks (Erőforrás-hivatkozás)      | A SubscriptionUsageSummary erőforrás-hivatkozásai.                                                      |
| Attribútumok       | ResourceAttributes (Erőforrás-attribútumok) | A SubscriptionUsageSummary attribútumnak megfelelő metaadat-attribútumok.                                                 |
