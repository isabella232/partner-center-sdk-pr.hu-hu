---
title: Azure-kihasználtsági rekordok erőforrásai
description: Az Azure-kihasználtsági rekord az Azure-előfizetési erőforrások kihasználtságával kapcsolatos részleteket tartalmaz.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 21d39c4497c00f5abeeeb771dfe20cd1e2b1c13a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767763"
---
# <a name="azure-utilization-record-resources"></a>Azure-kihasználtsági rekordok erőforrásai

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Az Azure-kihasználtsági rekord az Azure-előfizetési erőforrások kihasználtságával kapcsolatos részleteket tartalmaz. Ha Ön egy olyan felhőalapú szolgáltatói partner, amely az ügyfeleknek az Azure-előfizetésekhez tartozó számlázási kapcsolattal rendelkezik, a REST API segítségével méretezhető módon követheti nyomon az előfizetésekben felmerülő használati adatokat, hogy az összes számlázási ciklus végén elküldje a számlát az ügyfeleknek.

Ha nyomon szeretné követni a használatot, és segít megjósolni a havi számlát és az egyes ügyfelek számláit, kombinálhatja a díjszabási kártya lekérdezését, és lekérheti a [Microsoft Azure díjszabását](get-prices-for-microsoft-azure.md) , hogy lekérje az [ügyfél kihasználtsági rekordjait az Azure](get-a-customer-s-utilization-record-for-azure.md)-ban.

Az árak a piac és a pénznem alapján eltérnek, és ez az API figyelembe veszi a helyet. Alapértelmezés szerint az API a partner-profil beállításait a partner Centerben és a böngésző nyelvén használja, és ezek a beállítások testreszabhatók. A hely ismertsége különösen akkor fontos, ha egyetlen, központosított irodában több piacon kezel értékesítéseket.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Egy Azure-kihasználtsági rekord erőforrásának tulajdonságait ismerteti.

| Tulajdonság       | Típus                                      | Kötelező | Leírás                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | sztring                                    | Igen      | A használati összesítés időtartományának kezdete. A válasz a felhasználás ideje szerint van csoportosítva (ha az erőforrást ténylegesen használták, és mikor jelentették a számlázási rendszernek). |
| usageEndTime   | sztring                                    | Igen      | A használati összesítés időtartományának vége. A válasz a felhasználás ideje szerint van csoportosítva. Ez azt jelenti, hogy ha az erőforrást ténylegesen használták, és a számlázási rendszernek jelent meg.   |
| erőforrás       | object                                    | Igen      | Egy [AzureResource](#azureresource) objektumot tartalmaz.                                                                                                                                     |
| quantity       | szám                                    | Igen      | A AzureResource felhasznált mennyiség [.](#azureresource)                                                                                                                           |
| egység           | sztring                                    | No       | A mennyiség típusa (óra, bájt stb.) Ez a tulajdonság nem kötelező                                                                                                                     |
| infoFields     | object                                    | Igen      | A példányok szintjének részleteit tartalmazó kulcs-érték párok. Lehet, hogy ez az objektum üres.                                                                                                                    |
| instanceData   | object                                    | Nem       | Egy olyan [AzureInstanceData](#azureinstancedata) objektumot tartalmaz, amely a példányok szintjének részleteinek kulcs-érték párokat tartalmazza. Ez a tulajdonság nem kötelező, és nem vehető fel.                  |
| attribútumok     | [ResourceAttributes](utility-resources.md#resourceattributes) | Igen      | A metaadatok attribútumai. A "objektumtípus": "AzureUtilizationRecord" kifejezést tartalmazza                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Műveletek a AzureUtilizationRecord-erőforráson

- [Ügyfél Azure-használati rekordjainak lekérése](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Az Azure-erőforrások tulajdonságait ismerteti.

| Tulajdonság    | Típus   | Kötelező | Leírás                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | sztring | Igen      | Az Azure-erőforrás egyedi azonosítója. Más néven resourceID vagy erőforrás GUID. |
| name        | sztring | No       | A felhasznált erőforrás rövid neve. Ez a tulajdonság nem kötelező.            |
| category    | sztring | No       | A felhasznált erőforrás kategóriája. Ez a tulajdonság nem kötelező.                   |
| Alkategória | sztring | No       | A felhasznált erőforrás alkategóriája. Ez a tulajdonság nem kötelező.               |
| régió      | sztring | No       | A felhasznált erőforrás régiója. Ez a tulajdonság nem kötelező.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Az Azure-példányok adaterőforrásának tulajdonságait ismerteti.

| Tulajdonság       | Típus             | Kötelező | Leírás                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | sztring           | Igen      | A teljes körű Azure-erőforrás-azonosító, amely tartalmazza az erőforráscsoportot és a példány nevét.                   |
| location       | sztring           | Igen      | Az a régió, amelyben a szolgáltatást futtatták.                                                                               |
| partNumber     | object           | Igen      | Egyedi névtér, amely az erőforrás azonosítására szolgál a kereskedelmi piactér harmadik féltől származó felhasználásához. Ez a tulajdonság lehet üres karakterlánc. |
| rendelésszáma    | szám           | Igen      | A kereskedelmi piactér harmadik féltől származó rendelésének azonosítására szolgáló egyedi névtér. Ez a tulajdonság lehet üres karakterlánc.          |
| tags           | sztringek tömbje | Nem       | A felhasználó által megadott erőforrás-címkék. Ez a tulajdonság nem kötelező, és nem vehető fel.                            |
| additionalInfo | sztringek tömbje | Nem       | További információk az Azure-erőforrásokhoz. Ez a tulajdonság nem kötelező, és nem vehető fel.                          |