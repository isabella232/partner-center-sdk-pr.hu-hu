---
title: Az Azure-kihasználtság rekorderőforrások
description: Az Azure-beli kihasználtsági rekord az Azure-előfizetés erőforrásának kihasználtságával kapcsolatos adatokat tartalmaz.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: eb905dd41d5ab177a29bc1bd949c5eb865e4614e204250709d91f1a31304b267
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992279"
---
# <a name="azure-utilization-record-resources"></a>Az Azure-kihasználtság rekorderőforrások

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az Azure-beli kihasználtsági rekord az Azure-előfizetés erőforrásának kihasználtságával kapcsolatos adatokat tartalmaz. Ha Ön egy felhőszolgáltatói partner, aki az ügyfelek Azure-előfizetései számlázási kapcsolatának a tulajdonában áll, ezzel az REST API-ral skálázható módon követheti nyomon az előfizetések használatának nyomon követését, hogy minden számlázási ciklus végén számlát küldhet az ügyfeleinek.

A használat nyomon követéséhez és a havi számla és az egyes ügyfelek számlái előrejelzéséhez kombinálhat egy Rate Card-lekérdezést az [Microsoft Azure](get-prices-for-microsoft-azure.md) árainak lekéréséhez és az ügyfél Azure-beli kihasználtsági rekordjainak lekérésére vonatkozó [kéréssel.](get-a-customer-s-utilization-record-for-azure.md)

Az árak piac és pénznem szerint eltérnek, és ez az API figyelembe veszi a helyet. Alapértelmezés szerint az API a saját partnerprofil-beállításait használja Partnerközpont böngészőnyelven, és ezek a beállítások testre szabhatók. A helytudatosságát különösen akkor fontos, ha az értékesítéseket több piacon kezeli egyetlen központi irodából.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Egy Azure-beli kihasználtsági rekord erőforrásának tulajdonságait ismerteti.

| Tulajdonság       | Típus                                      | Kötelező | Leírás                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | sztring                                    | Yes      | A használati összesítés időtartományának kezdete. A válasz a felhasználás időpontja (az erőforrás használatának időpontja és a számlázási rendszernek való jelentés időpontja) szerint van csoportosítva. |
| usageEndTime   | sztring                                    | Yes      | A használati összesítés időtartományának vége. A válasz a felhasználás ideje szerint van csoportosítva. Ez azt jelenti, hogy az erőforrást mikor használták, és mikor jelentette a számlázási rendszernek.   |
| erőforrás       | object                                    | Yes      | Egy [AzureResource objektumot](#azureresource) tartalmaz.                                                                                                                                     |
| quantity       | szám                                    | Yes      | Az [AzureResource](#azureresource) által felhasznált mennyiség.                                                                                                                           |
| egység           | sztring                                    | No       | A mennyiség típusa (óra, bájt stb.) Ez a tulajdonság nem kötelező                                                                                                                     |
| infoFields (infoMezők)     | object                                    | Yes      | Példányszintű részletek kulcs-érték párok. Ez az objektum üres lehet.                                                                                                                    |
| instanceData (példányadatok)   | object                                    | No       | Egy [AzureInstanceData](#azureinstancedata) objektumot tartalmaz, amely példányszintű részletek kulcs-érték párokat tartalmaz. Ez a tulajdonság nem kötelező, és nem biztos, hogy tartalmazza.                  |
| Attribútumok     | [ResourceAttributes (Erőforrás-attribútumok)](utility-resources.md#resourceattributes) | Yes      | A metaadat-attribútumok. Tartalmazza az "objectType": "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>Műveletek az AzureUtilizationRecord erőforráson

- [Ügyfél Azure-használati rekordjainak lekérése](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Egy Azure-erőforrás tulajdonságait ismerteti.

| Tulajdonság    | Típus   | Kötelező | Leírás                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| id          | sztring | Yes      | Az Azure-erőforrás egyedi azonosítója. Más néven resourceID vagy erőforrás GUID. |
| name        | sztring | No       | A felhasznált erőforrás rövid neve. Ez a tulajdonság nem kötelező.            |
| category    | sztring | No       | A felhasznált erőforrás kategóriája. Ez a tulajdonság nem kötelező.                   |
| Alkategória | sztring | No       | A felhasznált erőforrás alkategóriája. Ez a tulajdonság nem kötelező.               |
| régió      | sztring | No       | A felhasznált erőforrás régiója. Ez a tulajdonság nem kötelező.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Egy Azure Instance Data-erőforrás tulajdonságait ismerteti.

| Tulajdonság       | Típus             | Kötelező | Leírás                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri (erőforrás-azonosító)    | sztring           | Yes      | A teljes Azure-erőforrásazonosító, amely tartalmazza az erőforráscsoportokat és a példány nevét.                   |
| location       | sztring           | Yes      | A régió, amelyben a szolgáltatás futott.                                                                               |
| partNumber     | object           | Yes      | A kereskedelmi piactér külső használatának erőforrásának azonosítására használt egyedi névtér. Ez a tulajdonság lehet egy üres sztring. |
| orderNumber (rendelésszám)    | szám           | Yes      | A kereskedelmi piactér külső megrendelésének azonosítására használt egyedi névtér. Ez a tulajdonság lehet egy üres sztring.          |
| tags           | sztringek tömbje | No       | A felhasználó által megadott erőforráscímkék. Ez a tulajdonság nem kötelező, és nem biztos, hogy tartalmazza.                            |
| additionalInfo | sztringek tömbje | No       | További adatok egy Azure-erőforráshoz. Ez a tulajdonság nem kötelező, és nem biztos, hogy tartalmazza.                          |