---
title: Előfizetés használati erőforrásai
description: Az előfizetés használati erőforrásai az előfizetéseket használati alapú számlázással írják le. Ezek az előfizetések napi és havi használati adatokat, valamint az egyes fizetési időszakok használati összegzését is magukban foglalják.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8e23287d80f19084860f4597754448e81c01049f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767836"
---
# <a name="subscription-usage-resources"></a>Előfizetés használati erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A következő előfizetés-használati források használatával lekérheti a használati adatokat egy adott előfizetéshez, amely használaton alapuló számlázást is biztosít. Ezek az előfizetések napi és havi használati adatokat, valamint az egyes fizetési időszakok használati összegzését is magukban foglalják.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

*A **SubscriptionDailyUsageRecord** erőforrás elavult, és pontatlan eredményeket eredményezhet. Javasoljuk, hogy frissítse alkalmazásait az Azure-ban az [ügyfél kihasználtsági rekordjainak beszerzése](get-a-customer-s-utilization-record-for-azure.md) című témakörben leírt API-k használatára, és helyette [Microsoft Azure árakat](get-prices-for-microsoft-azure.md) .*

A **SubscriptionDailyUsageRecord** -erőforrás azt írja le, hogy az előfizetés mennyit használ egy nap alatt.

| Tulajdonság         | Típus               | Leírás                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | sztring             | Az előfizetés által használt nap dátum és idő formátumban.                                 |
| ResourceId       | sztring             | GUID. Az erőforrás egyedi azonosítója.                                                          |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve.                                                                     |
| TotalCost        | decimal             | Az előfizetésben lévő erőforrások adott napon való használatának becsült teljes költsége.     |
| CurrencyLocale   | sztring             | A területi beállítás, amelyben az előfizetés használatban van, meghatározza a számlán használandó pénznemet. |
| LastModifiedDate | sztring             | A rekord utolsó módosításának napja a dátum és idő formátumban.                             |
| Attribútumok       | ResourceAttributes | Az erőforráshoz tartozó metaadat-attribútumok.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

A **SubscriptionMonthlyUsageRecord** -erőforrás azt írja le, hogy egy adott hónapban mennyi előfizetés van használatban.

| Tulajdonság         | Típus               | Leírás                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Állapot           | sztring             | Az előfizetés állapota: "None", "Active", "felfüggesztett" vagy "törölve".                  |
| PartnerOnRecord  | sztring             | "A partner MPN-azonosítója a rekordban."                                                        |
| OfferId          | sztring             | GUID. Az előfizetéshez kapcsolódó ajánlat azonosítója.                                       |
| Id               | sztring             | GUID. Az előfizetés vagy az erőforrás azonosítója.                                                 |
| Name             | sztring             | Az előfizetés vagy az erőforrás neve.                                                     |
| TotalCost        | decimal             | Az előfizetés erőforrásainak a megadott hónapban való használatának becsült teljes költsége.   |
| CurrencyLocale   | sztring             | A területi beállítás, amelyben az előfizetés használatban van, meghatározza a számlán használandó pénznemet. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetésekhez. |
| CurrencyCode     | sztring             | Lekérdezi vagy beállítja a pénznemkódot. Elérhető az Azure-csomag előfizetési erőforrásaihoz.                                         |
| USDTotalCost     | decimal             | Lekérdezi vagy beállítja a becsült teljes díjat USD-ben. Elérhető az Azure-csomagokhoz.                                         |
| LastModifiedDate | sztring             | A rekord utolsó módosításának napja a dátum és idő formátumban.                             |
| Attribútumok       | ResourceAttributes | Az erőforráshoz tartozó metaadat-attribútumok.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

A **SubscriptionUsageSummary** erőforrás azt írja le, hogy az aktuális számlázási időszakban milyen mértékben használták az adott előfizetést.

| Tulajdonság         | Típus               | Leírás                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | sztring             | GUID. Az előfizetés vagy az erőforrás azonosítója. A CustomerMonthlyUsageRecord kontextusában ez az azonosító az ügyfél azonosítója. |
| ResourceName nevű erőforrásáról     | sztring             | Az előfizetés vagy az erőforrás neve. A CustomerMonthlyUsageRecord kontextusában ez a név az ügyfél neve. |
| BillingStartDate | dátum               | Az aktuális számlázási időszak kezdő dátuma dátum és idő formátumban.                                                     |
| BillingEndDate   | dátum               | Az aktuális számlázási időszak záró dátuma dátum-idő formátumban.                                                       |
| TotalCost        | double             | Az előfizetés erőforrásainak a megadott számlázási időszakban történő használatának becsült teljes költsége.               |
| CurrencyLocale   | sztring             | A területi beállítás, amelyben az előfizetés használatban van, meghatározza a számlán használandó pénznemet. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetésekhez. |
| CurrencyCode   | sztring             | Lekérdezi vagy beállítja a pénznemkódot. Elérhető az Azure-csomagokhoz.                                         |
| USDTotalCost   | decimal             | Lekérdezi vagy beállítja a becsült teljes díjat USD-ben. Elérhető az Azure-csomag előfizetési erőforrásaihoz.                                         |
| LastModifiedDate | sztring             | A rekord utolsó módosításának napja a dátum és idő formátumban.                                                      |
| Hivatkozások            | ResourceLinks      | A SubscriptionUsageSummary megfelelő erőforrás-hivatkozások.                                                      |
| Attribútumok       | ResourceAttributes | A SubscriptionUsageSummary megfelelő metaadat-attribútumok.                                                 |
