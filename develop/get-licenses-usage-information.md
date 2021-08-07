---
title: Licencek használati adatainak lekérése
description: Licenchasználati információk lekérte a számítási feladatok szintjén a Office Dynamics szolgáltatáshoz.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a93c59c8c2a4c82ad7f3e81e814386e1ac0c046c3b0bada80eaaac40d9179d93
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990426"
---
# <a name="get-licenses-usage-information"></a>Licencek használati adatainak lekérése

Licenchasználati információk lekérte a számítási feladatok szintjén a Office Dynamics szolgáltatáshoz.

## <a name="prerequisites"></a>Előfeltételek

Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="uri-parameters"></a>URI-paraméterek

| Paraméter         | Típus     | Leírás | Kötelező |
|-------------------|----------|-------------|----------|
| top               | sztring   | A kérelemben visszaadni kívánt adatsorok száma. Ha nincs megadva, a maximális érték és az alapértelmezett érték 10000. Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható. | No |
| Ugrál              | int      | A lekérdezésben kihagyni kívánt sorok száma. Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk. Például a top=10000 és a skip=0 lekéri az első 10000 adatsort, a top=10000 és a skip=10000 a következő 10000 adatsort és így tovább. | No |
| filter (szűrő)            | sztring   | A *kérés* szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait. Minden utasítás tartalmaz egy mezőt és egy értéket, amely az vagy operátorhoz van társítva, és az utasítások kombinálhatók **`eq`** **`ne`** a vagy a **`and`** **`or`** használatával. Íme néhány példa *szűrőparaméterre:*<br/><br/>*filter=workloadCode eq 'SFB'*<br/><br/>*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)<br/><br/>A következő mezőket adhatja meg:<br/><br/>**workloadCode**<br/>**workloadName (számítási feladat neve)**<br/>**serviceCode**<br/>**serviceName (szolgáltatásnév)**<br/>**Csatorna**<br/>**customerTenantId (customerTenantId)**<br/>**customerName (ügyfél neve)**<br/>**Termelés**<br/>**Productname** | No |
| groupby           | sztring   | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt. A következő mezőket adhatja meg:<br/><br/>**workloadCode**<br/>**workloadName (számítási feladat neve)**<br/>**serviceCode**<br/>**serviceName (szolgáltatásnév)**<br/>**channelcustomerTenantId**<br/>**customerName (ügyfél neve)**<br/>**Termelés**<br/>**Productname**<br/><br/>A visszaadott adatsorok tartalmazzák a *groupby* paraméterben megadott mezőket és a következőket:<br/><br/>**licensesActive**<br/>**licensesQualified** | No |
| processedDateTime | DateTime | Megadhatja a használati adatok feldolgozásának dátumát. Alapértelmezés szerint az adatok feldolgozásának legkésőbbi dátuma | No |

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén a válasz törzse a következő mezőket tartalmazza, amelyek a licenchasználattal kapcsolatos adatokat tartalmazzák.

| Mező             | Típus     | Description                                   |
|-------------------|----------|-----------------------------------------------|
| workloadCode      | sztring   | Számítási feladat kódja                                 |
| workloadName (számítási feladat neve)      | sztring   | Számítási feladat neve                                 |
| serviceCode       | sztring   | Szolgáltatáskód                                  |
| serviceName (szolgáltatásnév)       | sztring   | Szolgáltatásnév                                  |
| Csatorna           | sztring   | Csatorna neve, viszonteladó                        |
| customerTenantId (customerTenantId)  | sztring   | Az ügyfél egyedi azonosítója            |
| customerName (ügyfél neve)      | sztring   | Ügyfél neve                                 |
| productId         | sztring   | A termék egyedi azonosítója             |
| Productname       | sztring   | Terméknév                                  |
| licensesActive    | hosszú     | Aktív licencek száma számítási feladatonként        |
| licensesQualified | hosszú     | A számítási feladat minősített licenceinek száma |
| processedDateTime | DateTime | Az adatok utolsó feldolgozásának dátuma         |

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
