---
title: Termék frissítési erőforrásai
description: Több, az Azure-csomagra Partnerközpont erőforrást is használhat. Ezek közé tartozik a ProductUpgradeRequest, a ProductUpgradesEligibility, a ProductUpgradesStatus, az UpgradesLineItem, az UpgradeProduct és az ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c995ac44dbe22000f7bc86991cb973ed31a5c018
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445340"
---
# <a name="product-upgrade-resources"></a>Termék frissítési erőforrásai

Az alábbi forrásokból többet is Partnerközpont azure-Microsoft Azure (MS-AZR-0145P) termékfrissítéséről.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

A **ProductUpgradesRequest erőforrás** információkat nyújt a termékfrissítési kérés objektumról.

| Tulajdonság      | Típus                                                          | Leírás                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | sztring                                                        | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.      |
| productFamily (termékcsalád) | sztring                                                        | Az a termékcsalád, amelyre a frissítést kérik. |
| Attribútumok    | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility (TermékupgradesEligibility)

A **ProductUpgradesEligibility** erőforrás információt nyújt arról, hogy az ügyfél jogosult-e termékfrissítésre.

| Tulajdonság      | Típus                                                          | Leírás                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | sztring                                                        | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.                            |
| productFamily (termékcsalád) | sztring                                                        | Az a termékcsalád, amelyre a frissítést kérik.                       |
| isEligible    | logikai                                                          | A bool érték azt jelzi, hogy az ügyfél jogosult-e a kért frissítésre. |
| upgradeId (frissítésiazonosító)     | sztring                                                        | A frissítési azonosító, ha az adott család termékfrissítése már meg van adva.        |
| reason        | sztring                                                        | Az ügyfél nem jogosult termékfrissítésre.                |
| productFamily (termékcsalád) | sztring                                                        | Az a termékcsalád, amelyre a frissítést kérik.                       |
| Attribútumok    | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

A **ProductUpgradesStatus erőforrás** információt nyújt a termékfrissítés állapotáról.

| Tulajdonság | Típus   | Leírás                                          |
|----------|--------|------------------------------------------------------|
| Id       | sztring | Egy GUID-formátumú sztring, amely azonosítja a frissítést. |
| productFamily (termékcsalád)       | sztring                                                         | Az a termékcsalád, amelyre a frissítést kérik.
| status              | sztring                                                         | A termékfrissítés állapota.
| lineItems (sorsorok)           | Az [UpgradesLineItem erőforrások tömbje](#upgradeslineitem)       | Objektumok tömbje, amely a kérelem törzsének részét képezi minden sorelem frissítési részleteiről nyújt információt.
| errorDetails        | [ErrorDetails erőforrás](#errordetails)                         | A kért frissítés hiba részletei.
| Attribútumok          | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

Az **UpgradesLineItem erőforrás** a kérés egyes sorelemei termékfrissítési részleteinek állapotát írja le.

| Tulajdonság      | Típus                                                          | Leírás                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct (forrástermék) | [UpgradeProduct](#upgradeproduct) objektum                      | A frissített forrástermékre vonatkozó információk. |
| targetProduct (céltermék) | [UpgradeProduct](#upgradeproduct) objektum                      | A céltermékre vonatkozó információk a frissítés után.   |
| upgradedDate (frissítésdDate)  | sztring UTC dátum-idő formátumban                                | Az előfizetés frissítésének dátuma.           |
| status        | sztring                                                        | A termékfrissítés állapota.                |
| errorDetails  | [ErrorDetails erőforrás](#errordetails)                        | A kért frissítés hiba részletei.          |
| Attribútumok    | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                          |

## <a name="upgradeproduct"></a>UpgradeProduct (Termékfrissítés)

Az **UpgradeProduct** erőforrás információt nyújt a frissített termékről.

| Tulajdonság   | Típus                                                          | Leírás                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| id         | sztring                                                        | Egy GUID-formátumú sztring, amely azonosítja a terméket. |
| name       | sztring                                                        | A frissített termék rövid neve.         |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                             |

## <a name="errordetails"></a>ErrorDetails

Az **ErrorDetails erőforrás** részleteket biztosít a frissítési folyamat során előforduló hibákról.

| Tulajdonság   | Típus                                                          | Leírás                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| code       | sztring                                                        | Hibakód, ha a termékfrissítés meghiúsul.      |
| message    | sztring                                                        | A termékfrissítés meghiúsult hibaüzenete. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                          |
