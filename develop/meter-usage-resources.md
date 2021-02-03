---
title: Mérőműszer-használati rekord erőforrása
description: A MeterUsageRecord-erőforrás segítségével leírhatja az előfizetés mérési szintjének becsült pénzügyi költségeit az aktuális számlázási ciklusban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c02c859d1d8ba3edd236d83d3056cb82533f7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767779"
---
# <a name="meter-usage-record-resource"></a>Mérőműszer-használati rekord erőforrása

**A következőkre vonatkozik:**

- Partnerközpont

A **MeterUsageRecord** -erőforrás segítségével leírhatja az előfizetés mérési szintjének becsült pénzügyi költségeit az aktuális számlázási ciklusban.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Tulajdonság         | Típus               | Leírás                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | sztring             | A partner Center [előfizetési erőforrás](subscription-resources.md#subscription)azonosítójának megfelelő GUID, amely egy Microsoft Azure (MS-AZR-0145P) előfizetést vagy egy Azure-csomagot jelöl. Microsoft Azure (MS-AZR-0145P) előfizetések esetén ez az érték a kereskedelmi előfizetés azonosítója. Az Azure-csomag előfizetési erőforrásai esetében ez az érték az Azure-csomag azonosítója.                  |
| MeterId  | sztring             | Lekérdezi vagy beállítja a mérőszám azonosítóját.                                                        |
| MeterName          | sztring             | Lekérdezi vagy beállítja a mérőszám nevét.                                       |
| Kategória               | sztring             | Lekérdezi vagy beállítja az Azure-erőforrás kategóriáját.                                                 |
| Alkategória             | sztring             |  Lekérdezi vagy beállítja az Azure-erőforrás alkategóriáját.                                                     |
| QuantityUsed        | decimal             | Lekérdezi vagy beállítja a felhasznált Azure-erőforrás mennyiségét.   |
| Unit (Egység)   | sztring             | Lekérdezi vagy beállítja az Azure-erőforrás mértékegységét. |
| TotalCost   | decimal             | Lekérdezi vagy beállítja a becsült teljes használati díjat. |
| CurrencyLocale   | sztring             | Az a területi beállítás, amelyben az előfizetés használatban volt. Ez a tulajdonság határozza meg a számlán használt pénznemet. Ez a tulajdonság Microsoft Azure (MS-AZR-0145P) előfizetésekhez érhető el. |
| CurrencyCode   | sztring             | Lekérdezi vagy beállítja a pénznemkódot. Ez a tulajdonság az Azure-csomagokhoz érhető el.                                         |
| USDTotalCost   | decimal             | Lekérdezi vagy beállítja a becsült teljes díjat USD-ben. Ez a tulajdonság az Azure-csomagokhoz érhető el.                                         |
| LastModifiedDate | sztring             | A rekord utolsó módosításának napja (dátum-idő formátumban).                             |
| Attribútumok       | ResourceAttributes | Az erőforráshoz tartozó metaadat-attribútumok.                                        |                                           |
