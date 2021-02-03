---
title: Erőforrás-használati rekordok erőforrásai
description: A ResourceUsageRecord-erőforrás segítségével leírhatja az előfizetés erőforrás-szintjének becsült pénzügyi költségeit az aktuális számlázási ciklusban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a293818cf4a6545dc705bf30fae6753f2e7eaf1
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767875"
---
# <a name="resource-usage-record-resources"></a>Erőforrás-használati rekordok erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont

A **ResourceUsageRecord** -erőforrás segítségével leírhatja az előfizetés erőforrás-szintjének becsült pénzügyi költségeit az aktuális számlázási ciklusban.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Tulajdonság         | Típus               | Leírás                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | sztring             | Lekérdezi vagy beállítja az előfizetés azonosítóját. Microsoft Azure (MS-AZR-0145P) előfizetések esetén ez az érték a kereskedelmi előfizetés azonosítója. Az Azure-csomagok esetében ez az érték az Azure-csomag azonosítója.                  |
| ResourceUri  | sztring             | Lekérdezi vagy beállítja az erőforrás URI azonosítóját. "                                                        |
| ResourceType          | sztring             | Lekérdezi vagy beállítja az erőforrás típusát.                                       |
| EntitlementId               | sztring             | Lekérdezi vagy beállítja a jogosultsági azonosítót (az Azure-előfizetés azonosítóját).                                                 |
| EntitlementName             | sztring             | Lekérdezi vagy beállítja a jogosultság nevét.                                                     |
| ResourceGroupName        | double             | Lekérdezi vagy beállítja az erőforráscsoport nevét.   |
| Name   | sztring             | Az erőforrás neve. |
| ResourceName nevű erőforrásáról   | sztring             | Lekérdezi vagy beállítja az erőforrás nevét. |
| TotalCost   | decimal             | Lekérdezi vagy beállítja a becsült teljes használati díjat. |
| CurrencyCode   | sztring             | Lekérdezi vagy beállítja a pénznemkódot.                                          |
| USDTotalCost   | decimal             | Lekérdezi vagy beállítja a becsült teljes díjat USD-ben.                                         |
| LastModifiedDate | sztring             | A rekord utolsó módosításának napja (dátum-idő formátumban).                             |
| Attribútumok       | ResourceAttributes | Az erőforráshoz tartozó metaadat-attribútumok.                                        |                                           |
