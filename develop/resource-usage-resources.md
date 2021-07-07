---
title: Erőforrás-használati rekord erőforrásai
description: A ResourceUsageRecord erőforrással leírhatja az előfizetés erőforrásszintű használatának becsült pénzbeli költségét az aktuális számlázási ciklusban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eb626b9d4cb4c57a07f45bcf7b914f534e62ab68
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446581"
---
# <a name="resource-usage-record-resources"></a>Erőforrás-használati rekord erőforrásai

A **ResourceUsageRecord** erőforrással leírhatja az előfizetés erőforrásszint-használatának becsült pénzbeli költségét az aktuális számlázási ciklusban.

## <a name="resourceusagerecord"></a>ResourceUsageRecord (Erőforrás-használatrekord)

| Tulajdonság          | Típus               | Leírás                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | sztring             | Lekért vagy beállítja az előfizetés azonosítóját. A Microsoft Azure (MS-AZR-0145P) előfizetések esetében ez az érték a kereskedelmi előfizetés azonosítója. Azure-csomagoknál ez az érték az Azure-csomag azonosítója). |
| ResourceUri (Erőforrás-azonosító)       | sztring             | Lekérte vagy beállítja az erőforrás URI-ét."                                                                                                                                                                            |
| ResourceType      | sztring             | Lekért vagy beállítja az erőforrás típusát.                                                                                                                                                                            |
| EntitlementId (Jogosultságazonosító)     | sztring             | Lekért vagy beállítja a jogosultságazonosítót (az Azure-előfizetés azonosítóját).                                                                                                                               |
| EntitlementName (Jogosultság neve)   | sztring             | Lekért vagy beállítja a jogosultság nevét.                                                                                                                                                                         |
| ResourceGroupName | double             | Lekért vagy beállítja az erőforráscsoport nevét.                                                                                                                                                                      |
| Name              | sztring             | Az erőforrás neve.                                                                                                                                                                                  |
| ResourceName nevű erőforrásáról      | sztring             | Lekért vagy beállítja az erőforrás nevét.                                                                                                                                                                     |
| TotalCost (Teljes költség)         | tizedes tört            | Lekért vagy beállítja a becsült teljes költséghasználatot.                                                                                                                                                               |
| CurrencyCode      | sztring             | Lekért vagy beállítja a pénznemkódot.                                                                                                                                                                            |
| USDTotalCost (UsdTotalCost)      | tizedes tört            | Lekért vagy beállítja a becsült teljes költséget USD-ben.                                                                                                                                                              |
| LastModifiedDate  | sztring             | A rekord utolsó módosításának napja (dátum-idő formátumban).                                                                                                                                          |
| Attribútumok        | ResourceAttributes (Erőforrás-attribútumok) | Az erőforrásnak megfelelő metaadat-attribútumok.                                                                                                                                                     |
