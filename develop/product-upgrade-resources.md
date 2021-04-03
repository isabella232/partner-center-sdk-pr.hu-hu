---
title: Termék frissítési erőforrásai
description: A partner Center-termékek frissítéseihez kapcsolódóan több erőforrást is használhat egy Azure-csomagra. Ilyenek például a ProductUpgradeRequest, a ProductUpgradesEligibility, a ProductUpgradesStatus, a UpgradesLineItem, a UpgradeProduct és a ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8975f0a135c88796a21f8abab944e53181f591e
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274614"
---
# <a name="product-upgrade-resources"></a>Termék frissítési erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont

Az alábbi forrásokból megtudhatja, hogyan frissítheti a partner Center termékeit Microsoft Azure (MS-AZR-0145P) előfizetésből egy Azure-csomagra.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

A **ProductUpgradesRequest** -erőforrás információt nyújt a termék-frissítési kérelmek objektumáról.

| Tulajdonság      | Típus                                                          | Leírás                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | sztring                                                        | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.      |
| productFamily | sztring                                                        | Az a termékcsalád, amelynek a frissítését kérik. |
| attribútumok    | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility

A **ProductUpgradesEligibility** -erőforrás információt nyújt az ügyfélnek a termék frissítésére vonatkozó jogosultságáról.

| Tulajdonság      | Típus                                                          | Leírás                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | sztring                                                        | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.                            |
| productFamily | sztring                                                        | Az a termékcsalád, amelynek a frissítését kérik.                       |
| isEligible    | logikai                                                          | A bool érték azt jelzi, hogy az ügyfél jogosult-e a kért frissítésre. |
| upgradeId     | sztring                                                        | A frissítési azonosító, ha az adott családhoz tartozó termék frissítése már megtörtént.        |
| reason        | sztring                                                        | Az az OK, amiért az ügyfél nem jogosult a termék frissítésére.                |
| productFamily | sztring                                                        | Az a termékcsalád, amelynek a frissítését kérik.                       |
| attribútumok    | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

A **ProductUpgradesStatus** -erőforrás információt nyújt a termék verziófrissítésének állapotáról.

| Tulajdonság | Típus   | Leírás                                          |
|----------|--------|------------------------------------------------------|
| Id       | sztring | Egy GUID-formázott karakterlánc, amely a frissítést azonosítja. |
| productFamily       | sztring                                                         | Az a termékcsalád, amelynek a frissítését kérik.
| status              | sztring                                                         | A termék verziófrissítésének állapota.
| Listaelemek           | [UpgradesLineItem](#upgradeslineitem) -erőforrások tömbje       | Objektumok tömbje, amely a kérés törzsében található minden egyes sor frissítésének részletes adatait tartalmazza.
| errorDetails        | [ErrorDetails](#errordetails) erőforrás                         | A frissítéshez kért hiba részletei.
| attribútumok          | [ResourceAttributes](utility-resources.md#resourceattributes)  | A metaadatok attribútumai. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

A **UpgradesLineItem** erőforrás a kérelem egyes sorában szereplő termék verziófrissítésének részleteit írja le.

| Tulajdonság      | Típus                                                          | Leírás                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct | [UpgradeProduct](#upgradeproduct) objektum                      | A frissítendő forrásoldali termék információi. |
| targetProduct | [UpgradeProduct](#upgradeproduct) objektum                      | A termékre vonatkozó frissítés utáni információ.   |
| upgradedDate  | karakterlánc UTC dátum-idő formátumban                                | Az előfizetés frissítésének dátuma.           |
| status        | sztring                                                        | A termék verziófrissítésének állapota.                |
| errorDetails  | [ErrorDetails](#errordetails) erőforrás                        | A frissítéshez kért hiba részletei.          |
| attribútumok    | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                          |

## <a name="upgradeproduct"></a>UpgradeProduct

A **UpgradeProduct** -erőforrás információt nyújt a frissítendő termékről.

| Tulajdonság   | Típus                                                          | Leírás                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| id         | sztring                                                        | Egy GUID-formázott karakterlánc, amely azonosítja a terméket. |
| name       | sztring                                                        | A frissítendő termék rövid neve.         |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                             |

## <a name="errordetails"></a>ErrorDetails

A **ErrorDetails** -erőforrás a frissítési folyamat során fellépő hibák részleteit tartalmazza.

| Tulajdonság   | Típus                                                          | Leírás                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| code       | sztring                                                        | Hibakód, ha a termék frissítése sikertelen.      |
| message    | sztring                                                        | Hibaüzenet, ha a termék frissítése sikertelen. |
| attribútumok | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai.                          |
