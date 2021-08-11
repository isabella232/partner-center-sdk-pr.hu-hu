---
title: Termék frissítési erőforrásai
description: Több, az Azure-csomag termékfrissítésével Partnerközpont erőforrást is használhat. Ezek közé tartozik a ProductUpgradeRequest, a ProductUpgradesEligibility, a ProductUpgradesStatus, az UpgradesLineItem, az UpgradeProduct és az ErrorDetails.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a251168dbe1e153365beec212feca6fafddaef1700ad8651ec9d459aebf24600
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997396"
---
# <a name="product-upgrade-resources"></a>Termék frissítési erőforrásai

Az alábbi forrásokból további információt Partnerközpont azure-Microsoft Azure (MS-AZR-0145P) termékfrissítéséről.

## <a name="productupgraderequest"></a>ProductUpgradeRequest

A **ProductUpgradesRequest erőforrás** információkat biztosít a termékfrissítési kérés objektumról.

| Tulajdonság      | Típus                                                          | Description                                                |
|---------------|---------------------------------------------------------------|------------------------------------------------------------|
| customerId    | sztring                                                        | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.      |
| productFamily (termékcsalád) | sztring                                                        | Az a termékcsalád, amelyre a frissítést kérik. |
| Attribútumok    | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                   |

## <a name="productupgradeseligibility"></a>ProductUpgradesEligibility (TermékupgradesEligibility)

A **ProductUpgradesEligibility** erőforrás információt nyújt arról, hogy az ügyfél jogosult-e termékfrissítésre.

| Tulajdonság      | Típus                                                          | Description                                                                      |
|---------------|---------------------------------------------------------------|----------------------------------------------------------------------------------|
| customerId    | sztring                                                        | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.                            |
| productFamily (termékcsalád) | sztring                                                        | Az a termékcsalád, amelyre a frissítést kérik.                       |
| isEligible    | logikai                                                          | A bool érték jelzi, hogy az ügyfél jogosult-e a kért frissítésre. |
| upgradeId (frissítésiazonosító)     | sztring                                                        | A frissítési azonosító, ha az adott család termékfrissítése már meg van adva.        |
| reason        | sztring                                                        | Az ügyfél nem jogosult termékfrissítésre.                |
| productFamily (termékcsalád) | sztring                                                        | Az a termékcsalád, amelyre a frissítést kérik.                       |
| Attribútumok    | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                                                         |

## <a name="productupgradesstatus"></a>ProductUpgradesStatus

A **ProductUpgradesStatus erőforrás** a termékfrissítés állapotáról nyújt információkat.

| Tulajdonság | Típus   | Description                                          |
|----------|--------|------------------------------------------------------|
| Id       | sztring | Egy GUID-formátumú sztring, amely azonosítja a frissítést. |
| productFamily (termékcsalád)       | sztring                                                         | Az a termékcsalád, amelyre a frissítést kérik.
| status              | sztring                                                         | A termékfrissítés állapota.
| lineItems (sorsorok)           | [UpgradesLineItem erőforrások tömbje](#upgradeslineitem)       | Objektumok tömbje, amely a kérelem törzsének részét képezi minden sorelem frissítési részleteinek információit tartalmazza.
| errorDetails        | [ErrorDetails erőforrás](#errordetails)                         | A kért frissítés hiba részletei.
| Attribútumok          | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes)  | A metaadat-attribútumok. |

## <a name="upgradeslineitem"></a>UpgradesLineItem

Az **UpgradesLineItem erőforrás** a kérés egyes sorelemei termékfrissítési részleteinek állapotát írja le.

| Tulajdonság      | Típus                                                          | Description                                       |
|---------------|---------------------------------------------------------------|---------------------------------------------------|
| sourceProduct (forrástermék) | [UpgradeProduct](#upgradeproduct) objektum                      | A frissített forrástermékre vonatkozó információk. |
| targetProduct (céltermék) | [UpgradeProduct](#upgradeproduct) objektum                      | A céltermékkel kapcsolatos információk a frissítés után.   |
| upgradedDate (frissítésdDate)  | sztring UTC dátum-idő formátumban                                | Az előfizetés frissítésének dátuma.           |
| status        | sztring                                                        | A termékfrissítés állapota.                |
| errorDetails  | [ErrorDetails erőforrás](#errordetails)                        | A kért frissítés hiba részletei.          |
| Attribútumok    | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                          |

## <a name="upgradeproduct"></a>UpgradeProduct (Termékfrissítés)

Az **UpgradeProduct** erőforrás információkat biztosít a frissített termékről.

| Tulajdonság   | Típus                                                          | Description                                          |
|------------|---------------------------------------------------------------|------------------------------------------------------|
| id         | sztring                                                        | Egy GUID-formátumú sztring, amely azonosítja a terméket. |
| name       | sztring                                                        | A frissített termék rövid neve.         |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                             |

## <a name="errordetails"></a>ErrorDetails

Az **ErrorDetails erőforrás** részleteket biztosít a frissítési folyamat során előforduló hibákról.

| Tulajdonság   | Típus                                                          | Description                                       |
|------------|---------------------------------------------------------------|---------------------------------------------------|
| code       | sztring                                                        | Hibakód, ha a termékfrissítés meghiúsul.      |
| message    | sztring                                                        | A termékfrissítés meghiúsult hibaüzenete. |
| Attribútumok | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok.                          |
