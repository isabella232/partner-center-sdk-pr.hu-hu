---
title: Mérőműszer-használati rekord erőforrása
description: A MeterUsageRecord-erőforrás segítségével leírhatja az előfizetés mérési szintjének becsült pénzügyi költségeit az aktuális számlázási ciklusban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbc8d1bd2cd3f9a9c1a657d88f3fe4899676e9df
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274648"
---
# <a name="meter-usage-record-resource"></a>Mérőműszer-használati rekord erőforrása

**A következőkre vonatkozik:**

- Partnerközpont

A **MeterUsageRecord** -erőforrás segítségével leírhatja az előfizetés mérési szintjének becsült pénzügyi költségeit az aktuális számlázási ciklusban.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Tulajdonság         | Típus               | Leírás                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId   | sztring             | A partner Center [előfizetési erőforrás](subscription-resources.md#subscription)azonosítójának megfelelő GUID, amely egy Microsoft Azure (MS-AZR-0145P) előfizetést vagy egy Azure-csomagot jelöl. Microsoft Azure (MS-AZR-0145P) előfizetések esetén ez az érték a kereskedelmi előfizetés azonosítója. Az Azure-csomag előfizetési erőforrásai esetében ez az érték az Azure-csomag azonosítója. |
| MeterId          | sztring             | Lekérdezi vagy beállítja a mérőszám azonosítóját.                                                                                                                                                                                                                                                                                                                                                                  |
| MeterName        | sztring             | Lekérdezi vagy beállítja a mérőszám nevét.                                                                                                                                                                                                                                                                                                                                                                        |
| Kategória         | sztring             | Lekérdezi vagy beállítja az Azure-erőforrás kategóriáját.                                                                                                                                                                                                                                                                                                                                                           |
| Alkategória      | sztring             | Lekérdezi vagy beállítja az Azure-erőforrás alkategóriáját.                                                                                                                                                                                                                                                                                                                                                       |
| QuantityUsed     | tizedes tört            | Lekérdezi vagy beállítja a felhasznált Azure-erőforrás mennyiségét.                                                                                                                                                                                                                                                                                                                                               |
| Unit (Egység)             | sztring             | Lekérdezi vagy beállítja az Azure-erőforrás mértékegységét.                                                                                                                                                                                                                                                                                                                                            |
| TotalCost        | tizedes tört            | Lekérdezi vagy beállítja a becsült teljes használati díjat.                                                                                                                                                                                                                                                                                                                                                     |
| CurrencyLocale   | sztring             | Az a területi beállítás, amelyben az előfizetés használatban volt. Ez a tulajdonság határozza meg a számlán használt pénznemet. Ez a tulajdonság Microsoft Azure (MS-AZR-0145P) előfizetésekhez érhető el.                                                                                                                                                                                                      |
| CurrencyCode     | sztring             | Lekérdezi vagy beállítja a pénznemkódot. Ez a tulajdonság az Azure-csomagokhoz érhető el.                                                                                                                                                                                                                                                                                                                         |
| USDTotalCost     | tizedes tört            | Lekérdezi vagy beállítja a becsült teljes díjat USD-ben. Ez a tulajdonság az Azure-csomagokhoz érhető el.                                                                                                                                                                                                                                                                                                           |
| LastModifiedDate | sztring             | A rekord utolsó módosításának napja (dátum-idő formátumban).                                                                                                                                                                                                                                                                                                                                   |
| Attribútumok       | ResourceAttributes | Az erőforráshoz tartozó metaadat-attribútumok.                                                                                                                                                                                                                                                                                                                                              |
