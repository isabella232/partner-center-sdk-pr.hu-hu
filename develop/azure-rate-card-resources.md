---
title: Azure-díjkártya – aktuális Azure-díjszabás
description: Ismerje meg, hogyan használhatja az Azure Rate Cardot az Adott régióban elérhető Azure-ajánlatok valós idejű, aktuális árainak lekért útjára. Az Azure Rate Card az Partnerközpont REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 52b9a9bea59690a8185a381647498de69a1476b1a4d4e8d632c5d13382776114
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991210"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Azure-díjszabású kártya-erőforrások a régióban található Azure-ajánlatok valós idejű, aktuális díjszabásának lehozása érdekében

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az Azure Rate Card valós idejű árakat biztosít az Azure-ajánlatokhoz. Az Azure díjszabása dinamikus, és gyakran változik. A Microsoft frissítéseket tesz közzé a Partnerközpont, de a REST API a leggyorsabb lehetőséget Felhőszolgáltató a jelenlegi árakhoz.

A használat nyomon követéséhez és a havi számla és az egyes ügyfelek számlái előrejelzéséhez kombinálhat egy Rate Card-lekérdezést az [Microsoft Azure](get-prices-for-microsoft-azure.md) árainak lekéréséhez és az ügyfél Azure-beli kihasználtsági rekordjainak lekérésére vonatkozó [kéréssel.](get-a-customer-s-utilization-record-for-azure.md)

Az árak piac és pénznem szerint különböznek, és ez az API figyelembe veszi a helyet. Alapértelmezés szerint az API a partnerprofil beállításait használja a Partnerközpont böngészőnyelven, és ezek a beállítások testre szabhatók. A helytudatosság különösen fontos, ha az értékesítéseket több piacon kezeli egyetlen központi irodából.

## <a name="azureratecard"></a>AzureRateCard

Egy Azure Rate Card-erőforrás tulajdonságait ismerteti.

| Tulajdonság      | Típus                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | sztring                                    | A pénznem, amelyben a díjszabás meg van téve.                     |
| isTaxIncluded | boolean                                   | Az összes díjszabás előzetes, ezért ez a tulajdonság értékként a értéket adja `false` vissza. |
| területi beállítás        | sztring                                    | Az a kulturális környezet, amelyben az erőforrás-információk honosulnak.       |
| Méter        | objektumok tömbje                          | [AzureMeter-objektumok tömbje.](#azuremeter)                       |
| offerTerms (ajánlati idő)    | objektumok tömbje                          | [AzureOfferTerm-objektumok tömbje.](#azureofferterm)               |
| Attribútumok    | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | A metaadat-attribútumok. Tartalmaz `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Műveletek az AzureRateCard erőforráson

- [Díjak lekérése a Microsoft Azure-tól](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Tulajdonság         | Típus             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| id               | sztring           | A mérő egyedi azonosítója.                                                                    |
| name             | sztring           | A fogyasztásmérő rövid neve.                                                                   |
| Árak            | object           | Fogyasztásmérők díjszabása. A kulcs a fogyasztásmérő mennyisége (sztring), az érték pedig a fogyasztásmérő sebessége (száma). |
| tags             | sztringek tömbje | Nem kötelező fogyasztásmérő-címkék. Ez a tömb üres is lehet.                                                 |
| category         | sztring           | Az erőforrás kategóriája.                                                                     |
| Alkategória      | sztring           | Az erőforrás alkategóriája.                                                                 |
| régió           | sztring           | Az azonosító régiója.                                                                             |
| egység             | sztring           | A mennyiség típusa (óra, bájt stb.)                                                     |
| includedQuantity | szám           | Az ingyenesen tartalmazott mérési mennyiség.                                               |
| effectiveDate (hatályosdátum)    | sztring           | Az a dátum, amikor az fogyasztásmérő érvényben van.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Tulajdonság         | Típus             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | sztring           | Az ajánlat kifejezésének rövid neve.        |
| discount         | szám           | Az alkalmazott kedvezmény, ha van ilyen.           |
| excludedMeterIds (excludedMeterIds) | sztringek tömbje | Az ajánlatból kizárt mérők, ha vannak. |
| effectiveDate (hatályosdátum)    | sztring           | Az ajánlat hatályba léptének dátuma.        |
