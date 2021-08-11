---
title: Erőforrás-használati rekord erőforrásai
description: A ResourceUsageRecord erőforrással leírhatja az előfizetés erőforrásszintű használatának becsült pénzügyi költségét az aktuális számlázási ciklusban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b330c49518bc12a63f2be731eef5c57884f5b15b706ce4007bbdf1a7bb8fab0e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996937"
---
# <a name="resource-usage-record-resources"></a>Erőforrás-használati rekord erőforrásai

A **ResourceUsageRecord** erőforrással leírhatja az előfizetés erőforrásszintű használatának becsült pénzügyi költségét az aktuális számlázási ciklusban.

## <a name="resourceusagerecord"></a>ResourceUsageRecord (Erőforrás-használatrekord)

| Tulajdonság          | Típus               | Description                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | sztring             | Lekérte vagy beállítja az előfizetés azonosítóját. A Microsoft Azure (MS-AZR-0145P) előfizetések esetében ez az érték a kereskedelmi előfizetés azonosítója. Azure-csomagoknál ez az érték az Azure-csomag azonosítója). |
| ResourceUri (Erőforrás-azonosító)       | sztring             | Lekérte vagy beállítja az erőforrás URI-ét."                                                                                                                                                                            |
| ResourceType      | sztring             | Lekért vagy beállítja az erőforrás típusát.                                                                                                                                                                            |
| EntitlementId (Jogosultságazonosító)     | sztring             | Lekért vagy beállítja a jogosultságazonosítót (az Azure-előfizetés azonosítóját).                                                                                                                               |
| EntitlementName (Jogosultság neve)   | sztring             | Lekért vagy beállítja a jogosultság nevét.                                                                                                                                                                         |
| ResourceGroupName | double             | Lekérte vagy beállítja az erőforráscsoport nevét.                                                                                                                                                                      |
| Name              | sztring             | Az erőforrás neve.                                                                                                                                                                                  |
| ResourceName nevű erőforrásáról      | sztring             | Lekérte vagy beállítja az erőforrás nevét.                                                                                                                                                                     |
| TotalCost (Teljes költség)         | tizedes tört            | Lekért vagy beállítja a becsült teljes költséghasználatot.                                                                                                                                                               |
| CurrencyCode      | sztring             | Lekért vagy beállítja a pénznemkódot.                                                                                                                                                                            |
| USDTotalCost      | tizedes tört            | Lekért vagy beállítja a becsült teljes költséget USD-ben.                                                                                                                                                              |
| LastModifiedDate  | sztring             | Az a nap (dátum-idő formátumban), amikor a rekordot utoljára módosították.                                                                                                                                          |
| Attribútumok        | ResourceAttributes (Erőforrás-attribútumok) | Az erőforrásnak megfelelő metaadat-attribútumok.                                                                                                                                                     |
