---
title: Ügyfél-használati erőforrások
description: A használaton alapuló előfizetéseket és a havi használati költségvetést (beleértve a CustomerMonthlyUsageRecord, a CustomerUsageSummary, a PartnerUsageSummary és a SpendingBudget) használó ügyfelek erőforrásai.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ec82fcfe6c08a8ad55dd1fb48984859b954dd3c8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767736"
---
# <a name="customer-usage-resources"></a>Ügyfél-használati erőforrások

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A használati alapú előfizetéssel rendelkező ügyfelek havi használati költségkerettel rendelkezhetnek. Ez a költségkeret korlátozza az ügyfél maximális kihasználtságát, és lehetővé teszi a partner számára a használat nyomon követését az idő múlásával.

> [!NOTE]
> Az ügyfél-használati számok a becslések (nem végleges értékek), amelyeket nem szabad számlázási célra használni.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

A **CustomerMonthlyUsageRecord** az ügyfél használatának becsült pénzügyi díját mutatja az aktuális hónapban.

| Tulajdonság         | Típus               | Leírás                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Költségvetés           | SpendingBudget     | Az ügyfél számára lefoglalt költségkeret.                          |
| PercentUsed      | decimal             | A lefoglalt költségvetésből felhasznált százalék.                        |
| ResourceId       | sztring             | Az erőforrás egyedi azonosítója.                                   |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve.                                                |
| TotalCost        | decimal             | Az előfizetésben lévő erőforrások becsült teljes használati költsége.|
| CurrencyLocale   | sztring             | Az ügyfél pénznemének területi beállítása. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetésekhez.            |
| CurrencyCode     | sztring             | Lekérdezi vagy beállítja a pénznemkódot. Elérhető az Azure-csomagokhoz.           |
| USDTotalCost     | decimal             | Lekérdezi vagy beállítja a becsült teljes díjat USD-ben. Elérhető az Azure-csomagokhoz.                                         |
| IsUpgraded       | logikai             | Lekérdezi vagy beállítja azt az értéket, amely jelzi, hogy az ügyfél Azure-előfizetése frissítve van-e. Az **igaz** érték az Azure-csomaggal rendelkező ügyfeleket jelöli.                         |
| LastModifiedDate | dátum               | A használati adatok utolsó módosításának dátuma.                               |
| Attribútumok       | ResourceAttributes | A használati rekordnak megfelelő metaadat-attribútumok.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

A **CustomerUsageSummary** a teljes számlázási időszakra vonatkozó ügyfél-használat összegzését jelöli.

| Tulajdonság         | Típus               | Leírás                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Költségvetés           | SpendingBudget     | Az ügyfél számára lefoglalt költségkeret.                                                                  |
| ResourceId       | sztring             | Az erőforrás egyedi azonosítója. A CustomerMonthlyUsageRecord kontextusában ez az azonosító az ügyfél azonosítója. |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve. A CustomerMonthlyUsageRecord kontextusában ez az ügyfél neve.               |
| BillingStartDate | dátum               | Az aktuális számlázási időszak kezdő dátuma.                                                                    |
| BillingEndDate   | dátum               | Az aktuális számlázási időszak záró dátuma.                                                                      |
| TotalCost        | decimal             | Az előfizetésben lévő erőforrások becsült teljes használati költsége.                                         |
| CurrencyLocale   | sztring             | Az ügyfél pénznemének területi beállítása. Elérhető Microsoft Azure (MS-AZR-0145P) előfizetésekhez.                                         |
| CurrencyCode     | sztring             | Lekérdezi vagy beállítja a pénznemkódot. Elérhető az Azure-csomagokhoz.                                         |
| USDTotalCost     | decimal             | Lekérdezi vagy beállítja a becsült teljes díjat USD-ben. Elérhető az Azure-csomag előfizetési erőforrásaihoz.                                         |
| LastModifiedDate | dátum               | A használati adatok utolsó módosításának dátuma.                                                                       |
| Hivatkozások            | ResourceLinks      | A használati összegzésnek megfelelő erőforrás-hivatkozások.                                                           |
| Attribútumok       | ResourceAttributes | A használat összegzéséhez tartozó metaadat-attribútumok.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

A **PartnerUsageSummary** az összes ügyfélre vonatkozó használati költségkeretet jelöli.

| Tulajdonság         | Típus               | Leírás                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | sztringek tömbje   | Az értesítésekhez tartozó e-mail-címek listája.                                                                   |
| CustomerOverBudget | egész szám          | A költségvetésen felüli ügyfelek száma.                                                                    |
| CustomersTrendingOver | egész szám       | A költségvetéshez közeledő ügyfelek száma.                                                     |
| CustomersWithUsageBasedSubscriptions  | egész szám | A használati alapú előfizetéssel rendelkező ügyfelek száma.                                               |
| ResourceId       | sztring             | Az erőforrás egyedi azonosítója. A CustomerMonthlyUsageRecord kontextusában ez az azonosító az ügyfél azonosítója. |
| ResourceName nevű erőforrásáról     | sztring             | Az erőforrás neve. A CustomerMonthlyUsageRecord kontextusában ez az ügyfél neve.               |
| BillingStartDate | dátum               | Az aktuális számlázási időszak kezdő dátuma.                                                                    |
| BillingEndDate   | dátum               | Az aktuális számlázási időszak záró dátuma.                                                                      |
| TotalCost        | decimal             | Az összes ügyfél-használat becsült teljes költsége a számlázási időszak elejétől számított aktuális használat alapján.      |
| CurrencyLocale   | sztring             | A pénznem területi beállítása.                                                                                             |
| LastModifiedDate | dátum               | A használati adatok utolsó módosításának dátuma.                                                                       |
| Hivatkozások            | ResourceLinks      | A használati összegzésnek megfelelő erőforrás-hivatkozások.                                                           |
| Attribútumok       | ResourceAttributes | A használat összegzéséhez tartozó metaadat-attribútumok.                                                      |

## <a name="spendingbudget"></a>SpendingBudget

A **SpendingBudget** az ügyfélnek a használati alapú előfizetésekhez lefoglalt költségvetést jelöli.

| Tulajdonság   | Típus               | Leírás                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Összeg     | decimal             | A lefoglalt költségkeret. Ha az érték null, az ügyfél számára nincs kiosztva költségkeret. |
| Attribútumok | ResourceAttributes | A költségvetéshez tartozó metaadat-attribútumok.                                                |
