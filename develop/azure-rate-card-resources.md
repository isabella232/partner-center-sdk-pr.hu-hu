---
title: Azure Rate Card – aktuális Azure-díjszabás
description: Megtudhatja, hogyan használhatja az Azure díjszabási kártyáját a régiójában lévő Azure-ajánlatok valós idejű, aktuális árainak beszerzéséhez. Az Azure Rate Card a partner Center REST APIon keresztül érhető el.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 2d011153f508ea0a745413b88003333452d0af24
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768551"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Azure Rate Card-erőforrások valós idejű, aktuális Azure-árak a régión belüli Azure-ajánlatokhoz

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az Azure díjszabási kártyája valós idejű árakat biztosít az Azure-ajánlatokhoz. Az Azure díjszabása meglehetősen dinamikus, és gyakran változnak. A Microsoft frissítéseket tesz közzé a partner Centerben, de a REST API biztosítja a leggyorsabb megoldást a felhőalapú megoldások szolgáltatói partnerei számára a jelenlegi árak beszerzésére.

Ha nyomon szeretné követni a használatot, és segít megjósolni a havi számlát és az egyes ügyfelek számláit, kombinálhatja a díjszabási kártya lekérdezését, és lekérheti a [Microsoft Azure díjszabását](get-prices-for-microsoft-azure.md) , hogy lekérje az [ügyfél kihasználtsági rekordjait az Azure](get-a-customer-s-utilization-record-for-azure.md)-ban.

Az árak a piac és a pénznem alapján eltérnek, és ez az API figyelembe veszi a helyet. Alapértelmezés szerint az API a partner-profil beállításait a partner Centerben és a böngésző nyelvén használja, és ezek a beállítások testreszabhatók. A hely ismertsége különösen akkor fontos, ha egyetlen, központosított irodában több piacon kezel értékesítéseket.

## <a name="azureratecard"></a>AzureRateCard

Az Azure Rate Card-erőforrások tulajdonságait ismerteti.

| Tulajdonság      | Típus                                      | Leírás                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | sztring                                    | Az a pénznem, amelyben a díjszabást megadja.                     |
| isTaxIncluded | boolean                                   | Az összes díj áfa, így ez a tulajdonság a értéket adja vissza `false` . |
| területi beállítás        | sztring                                    | Az a kulturális környezet, amelyben az erőforrás-információk honosítva vannak.       |
| méterre        | objektumok tömbje                          | [AzureMeter](#azuremeter) objektumok tömbje.                       |
| offerTerms    | objektumok tömbje                          | [AzureOfferTerm](#azureofferterm) objektumok tömbje.               |
| attribútumok    | [ResourceAttributes](utility-resources.md#resourceattributes) | A metaadatok attribútumai. Tartalmaz `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Műveletek a AzureRateCard-erőforráson

- [Díjak lekérése a Microsoft Azure-tól](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Tulajdonság         | Típus             | Leírás                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | sztring           | A mérő egyedi azonosítója.                                                                    |
| name             | sztring           | A fogyasztásmérő rövid neve.                                                                   |
| díjak            | object           | Mérési díjak. A kulcs a mérési mennyiség (string), az érték pedig a mérési arány (szám). |
| tags             | sztringek tömbje | Opcionális mérőműszer-címkék. Ez a tömb lehet üres.                                                 |
| category         | sztring           | Az erőforrás kategóriája.                                                                     |
| Alkategória      | sztring           | Az erőforrás alkategóriája.                                                                 |
| régió           | sztring           | Az azonosító régiója.                                                                             |
| egység             | sztring           | A mennyiség típusa (óra, bájt stb.)                                                     |
| includedQuantity | szám           | A felszámított mennyiség ingyenes.                                               |
| effectiveDate    | sztring           | A mérőszám érvényességi dátuma.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Tulajdonság         | Típus             | Leírás                             |
|------------------|------------------|-----------------------------------------|
| name             | sztring           | Az ajánlat kifejezésének rövid neve.        |
| discount         | szám           | Az alkalmazott kedvezmény, ha van ilyen.           |
| excludedMeterIds | sztringek tömbje | Az ajánlatból kizárt mérőműszerek, ha vannak ilyenek. |
| effectiveDate    | sztring           | Az ajánlat érvényességének dátuma.        |
