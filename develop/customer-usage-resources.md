---
title: Ügyfélhasználati erőforrások
description: Használatalapú előfizetéssel és havi használati költségvetéssel (például CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary és SpendingBudget) kapcsolatos erőforrások.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eae516e2f759dfc2e8f80e946a835d70760c5c9e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973043"
---
# <a name="customer-usage-resources"></a>Ügyfélhasználati erőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A használatalapú előfizetéssel az ügyfelek havi használati költségkeretet használhatnak. Ez a költségkeret beállítja az ügyfél maximális használati korlátját, és lehetővé teszi, hogy a partner nyomon kövesse a használatot az idő során.

> [!NOTE]
> Az ügyfélhasználati számok becslések (nem végleges értékek), amelyek nem használhatók számlázási célokra.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord (ÜgyfélmonthlyUsageRecord)

**A CustomerMonthlyUsageRecord** az ügyfél aktuális havi használatának becsült pénzügyi költségét jelöli.

| Tulajdonság         | Típus               | Leírás                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Költségvetés           | SpendingBudget     | Az ügyfél számára lefoglalt költségkeret.                          |
| PercentUsed (Százalékos arány)      | tizedes tört             | A lefoglalt költségvetésből felhasznált százalékos arány.                        |
| ResourceId       | sztring             | Az erőforrás egyedi azonosítója.                                   |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve.                                                |
| TotalCost (Teljes költség)        | tizedes tört             | Az előfizetésben található erőforrások becsült teljes használati költsége.|
| CurrencyLocale   | sztring             | Az ügyfél pénznemének területi területi stb. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetéshez.            |
| CurrencyCode     | sztring             | Lekért vagy beállítja a pénznemkódot. Elérhető Azure-csomagokhoz.           |
| USDTotalCost (UsdTotalCost)     | tizedes tört             | Lekért vagy beállítja a becsült teljes költséget USD-ben. Elérhető Azure-csomagokhoz.                                         |
| IsUpgraded (Új)       | logikai             | Lekért vagy beállítja azt az értéket, amely jelzi, hogy az ügyfél Azure-előfizetése frissítve van-e. Az igaz **érték azokat** az ügyfeleket jelöli, akik Azure-csomagokkal vannak.                         |
| LastModifiedDate | dátum               | A használati adatok utolsó módosításának dátuma.                               |
| Attribútumok       | ResourceAttributes (Erőforrás-attribútumok) | A használati rekordnak megfelelő metaadat-attribútumok.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**A CustomerUsageSummary** az ügyfél teljes számlázási időszakra vonatkozó használati adatokat összegzi.

| Tulajdonság         | Típus               | Leírás                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Költségvetés           | SpendingBudget     | Az ügyfél számára lefoglalt költségkeret.                                                                  |
| ResourceId       | sztring             | Az erőforrás egyedi azonosítója. A CustomerMonthlyUsageRecord kontextusában ez az azonosító az ügyfél azonosítója. |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve. A CustomerMonthlyUsageRecord kontextusában ez az ügyfél neve.               |
| BillingStartDate (Számlázási kezdő dátum) | dátum               | Az aktuális számlázási időszak kezdő dátuma.                                                                    |
| BillingEndDate (Számlázási dátum)   | dátum               | Az aktuális számlázási időszak záró dátuma.                                                                      |
| TotalCost (Teljes költség)        | tizedes tört             | Az előfizetésben található erőforrások becsült teljes használati költsége.                                         |
| CurrencyLocale   | sztring             | Az ügyfél pénznemének területi területi stb. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetéshez.                                         |
| CurrencyCode     | sztring             | Lekért vagy beállítja a pénznemkódot. Elérhető Azure-csomagokhoz.                                         |
| USDTotalCost (UsdTotalCost)     | tizedes tört             | Lekért vagy beállítja a becsült teljes költséget USD-ben. Elérhető az Azure-csomag előfizetési erőforrásaihoz.                                         |
| LastModifiedDate | dátum               | A használati adatok utolsó módosításának dátuma.                                                                       |
| Hivatkozások            | ResourceLinks (Erőforrás-hivatkozás)      | A használati összegzésnek megfelelő erőforrás-hivatkozások.                                                           |
| Attribútumok       | ResourceAttributes (Erőforrás-attribútumok) | A használat összegzésének megfelelő metaadat-attribútumok.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**A PartnerUsageSummary** az összes ügyfél használati költségvetésének partnerszintű összegzését jelenti.

| Tulajdonság         | Típus               | Leírás                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | sztringek tömbje   | Az értesítések e-mail-címének listája.                                                                   |
| CustomerOverBudget (CustomerOverBudget) | egész szám          | A költségkereten túli ügyfelek száma.                                                                    |
| CustomersTrendingOver | egész szám       | Azon ügyfelek száma, akik közel állnak a költségvetés túleső egymáshoz.                                                     |
| CustomersWithUsageBasedSubscriptions  | egész szám | A használatalapú előfizetéssel kapcsolatos ügyfelek száma.                                               |
| ResourceId       | sztring             | Az erőforrás egyedi azonosítója. A CustomerMonthlyUsageRecord környezetben ez az azonosító az ügyfél azonosítója. |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve. A CustomerMonthlyUsageRecord kontextusában ez az ügyfél neve.               |
| BillingStartDate (Számlázási kezdő dátum) | dátum               | Az aktuális számlázási időszak kezdő dátuma.                                                                    |
| BillingEndDate (Számlázási dátum)   | dátum               | Az aktuális számlázási időszak záró dátuma.                                                                      |
| TotalCost (Teljes költség)        | tizedes tört             | Az összes ügyfélhasználat becsült teljes költsége a számlázási időszak kezdettől számított aktuális használat alapján.      |
| CurrencyLocale   | sztring             | A pénznem területi stb.                                                                                             |
| LastModifiedDate | dátum               | A használati adatok utolsó módosításának dátuma.                                                                       |
| Hivatkozások            | ResourceLinks (Erőforrás-hivatkozás)      | A használat összegzésének megfelelő erőforrás-hivatkozások.                                                           |
| Attribútumok       | ResourceAttributes (Erőforrás-attribútumok) | A használat összegzésének megfelelő metaadat-attribútumok.                                                      |

## <a name="spendingbudget"></a>SpendingBudget (Kiadások hibakeresése)

**A SpendingBudget az** ügyfél számára a használatalapú előfizetések számára lefoglalt költségvetést jelöli.

| Tulajdonság   | Típus               | Leírás                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Összeg     | tizedes tört             | A lefoglalt költségvetés. Ha az érték null, nincs hozzárendelve költségkeret ehhez az ügyfélhez. |
| Attribútumok | ResourceAttributes (Erőforrás-attribútumok) | A költségvetésnek megfelelő metaadat-attribútumok.                                                |
