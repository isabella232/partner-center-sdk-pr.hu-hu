---
title: Az Azure-kihasználtság rekorderőforrások
description: Az Azure-beli kihasználtsági rekord az Azure-előfizetés erőforrásának kihasználtsági adatait tartalmazza.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 868381fcb29eb1391efcdf79154f7b998e3032e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974301"
---
# <a name="azure-utilization-record-resources"></a>Az Azure-kihasználtság rekorderőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az Azure-beli kihasználtsági rekord az Azure-előfizetés erőforrásának kihasználtsági adatait tartalmazza. Ha Ön egy felhőszolgáltatói partner, aki az ügyfelek Azure-előfizetései számlázási kapcsolatának a tulajdonában áll, ezzel az REST API-ral skálázható módon követheti nyomon az előfizetések használatának nyomon követését, hogy minden számlázási ciklus végén számlát küldhet az ügyfeleinek.

A használat nyomon követéséhez és a havi számla és az egyes ügyfelek számlái előrejelzéséhez kombinálhat egy Rate Card-lekérdezést az [Microsoft Azure](get-prices-for-microsoft-azure.md) árainak lekéréséhez és az ügyfél Azure-beli kihasználtsági rekordjainak lekérésére vonatkozó [kéréssel.](get-a-customer-s-utilization-record-for-azure.md)

Az árak piac és pénznem szerint eltérnek, és ez az API figyelembe veszi a helyet. Alapértelmezés szerint az API a saját partnerprofil-beállításait használja Partnerközpont böngészőnyelven, és ezek a beállítások testre szabhatók. A helytudatosságát akkor különösen fontos, ha egyetlen központi irodából több piacon is kezeli az értékesítéseket.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Egy Azure-beli kihasználtsági rekord erőforrásának tulajdonságait ismerteti.

| Tulajdonság       | Típus                                      | Kötelező | Leírás                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime (használat indítási ideje) | sztring                                    | Igen      | A használati összesítés időtartományának kezdete. A válasz a felhasználás időpontja (az erőforrás használatának időpontja és a számlázási rendszernek való jelentés időpontja) szerint van csoportosítva. |
| usageEndTime   | sztring                                    | Igen      | A használati összesítés időtartományának vége. A válasz a felhasználás ideje szerint van csoportosítva. Ez azt jelenti, hogy az erőforrást mikor használták, és mikor jelentette a számlázási rendszernek.   |
| Erőforrás       | object                                    | Igen      | Egy [AzureResource objektumot](#azureresource) tartalmaz.                                                                                                                                     |
| quantity       | szám                                    | Igen      | Az [AzureResource](#azureresource) által felhasznált mennyiség.                                                                                                                           |
| egység           | sztring                                    | No       | A mennyiség típusa (óra, bájt stb.) Ez a tulajdonság nem kötelező                                                                                                                     |
| infoFields (infoMezők)     | object                                    | Igen      | Példányszintű részletek kulcs-érték párok. Ez az objektum üres lehet.                                                                                                                    |
| instanceData (példányadatok)   | object                                    | Nem       | Egy [AzureInstanceData](#azureinstancedata) objektumot tartalmaz, amely példányszintű részletek kulcs-érték párokat tartalmaz. Ez a tulajdonság nem kötelező, és nem biztos, hogy tartalmazza.                  |
| Attribútumok     | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Igen      | A metaadat-attribútumok. Tartalmazza az "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Műveletek az AzureUtilizationRecord erőforráson

- [Ügyfél Azure-használati rekordjainak lekérése](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Egy Azure-erőforrás tulajdonságait ismerteti.

| Tulajdonság    | Típus   | Kötelező | Leírás                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | sztring | Igen      | Az Azure-erőforrás egyedi azonosítója. Más néven resourceID vagy erőforrás GUID. |
| name        | sztring | No       | A felhasznált erőforrás rövid neve. Ez a tulajdonság nem kötelező.            |
| category    | sztring | No       | A felhasznált erőforrás kategóriája. Ez a tulajdonság nem kötelező.                   |
| Alkategória | sztring | No       | A felhasznált erőforrás alkategóriája. Ez a tulajdonság nem kötelező.               |
| régió      | sztring | No       | A felhasznált erőforrás régiója. Ez a tulajdonság nem kötelező.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Egy Azure Instance Data-erőforrás tulajdonságait ismerteti.

| Tulajdonság       | Típus             | Kötelező | Leírás                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri (erőforrás-azonosító)    | sztring           | Igen      | A teljes Azure-erőforrásazonosító, amely tartalmazza az erőforráscsoportokat és a példány nevét.                   |
| location       | sztring           | Igen      | A régió, amelyben a szolgáltatás futott.                                                                               |
| partNumber     | object           | Igen      | A kereskedelmi piactér külső használatának erőforrásának azonosítására használt egyedi névtér. Ez a tulajdonság lehet egy üres sztring. |
| orderNumber (rendelésszám)    | szám           | Igen      | A kereskedelmi piactér külső megrendelésének azonosítására használt egyedi névtér. Ez a tulajdonság lehet egy üres sztring.          |
| tags           | sztringek tömbje | Nem       | A felhasználó által megadott erőforráscímkék. Ez a tulajdonság nem kötelező, és nem biztos, hogy tartalmazza.                            |
| additionalInfo | sztringek tömbje | Nem       | További adatok egy Azure-erőforráshoz. Ez a tulajdonság nem kötelező, és nem biztos, hogy tartalmazza.                          |