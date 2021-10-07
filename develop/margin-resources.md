---
title: Margin-erőforrások
description: A margókat képviselő erőforrások. A margók leírására vonatkozó forrásokat tartalmaz.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 83ea2f95c72f4e5074e3396ef226462b5b007878
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646402"
---
# <a name="margin-resources"></a>Margin-erőforrások

A rendelkezésre álló margókat képviselő erőforrások. A margó leírására vonatkozó erőforrásokat tartalmaz.  

A független szoftverszállító (ISV) kedvezményeket vagy margókat hozhat létre adott felhőszolgáltatók (CSP-k) számára. Az alábbi források a margókat ábrázolják és írják le.
                
## <a name="margin"></a>Margin                   
                        
Egy adott CSP-hez használható margót képvisel.
                
| Név            | Típus            | Description                               |
|-----------------|-----------------|-------------------------------------------|
| id              | sztring          | A margó egyedi azonosítója.         |
| marginPercentage (marginPercentage) | szám         | A CSP kiskereskedelmi árára alkalmazott százalékos kedvezmény.  |
| productId       | sztring          | A margóhoz elérhető termékazonosító.   |
| productTitle    | sztring          | A termék címe, amely számára a margó elérhető. |
| productType     | sztring          | Az a terméktípus, amely számára a margó elérhető.   |
| publisherName   | sztring          | Annak az ISV-nek a neve, aki létrehozta a margót.  |
| skuId (termékváltozat-azonosító)           | sztring          | A margóhoz elérhető termékváltozat-azonosító.  |
| skuTitle        | sztring          | Az SKU címe, amely számára a margó elérhető. |
| startDate (kezdőDátum)       | sztring          | A margó elérhetővé válik a kezdési dátum. |
| endDate (endDate)         | sztring          | A margó elérhetővé válik a záró dátuma. |
| status          | sztring          | Állapot azt jelzi, hogy a margó elérhető-e. |
| statusDate (állapotdátum)      | sztring          | Az állapot utolsó frissítésének dátuma. |

## <a name="definitions"></a>Definíciók

A margókat leíró különböző típusú összetevők.                    

| Név            | Leírás          |
|-----------------|----------------------|
| Margin |  Egyéni margót határoz meg.  |    
| MarginSearchResponse (MarginSearchResponse) |  A margó válaszadatát határozza meg.  |  
        
## <a name="related-documentation"></a>Kapcsolódó dokumentáció

- [A margók Partnerközpont áttekintése](/partner-center/csp-commercial-marketplace-margins)
- [Piactéri ajánlatok vásárlása](/partner-center/csp-commercial-marketplace-purchase)
- [Piactéri ajánlatok kezelése](/partner-center/csp-commercial-marketplace-manage)
- [Margók listájának lekért listája](get-margins.md)
- [A margók listájának letöltése](download-margins.md)
