---
title: Licencek üzembehelyezési adatainak lekérése
description: Az Office-és Dynamics-licencek telepítési adatainak beszerzése.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768164"
---
# <a name="get-licenses-deployment-information"></a>Licencek üzembehelyezési adatainak lekérése

**A következőkre vonatkozik**

- Partnerközpont

Az Office-és Dynamics-licencek telepítési adatainak beszerzése.

## <a name="prerequisites"></a>Előfeltételek

A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Analytics/Commercial/Deployment/License/http/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="uri-parameters"></a>URI-paraméterek

| Paraméter         | Típus     | Leírás | Kötelező |
|-------------------|----------|-------------|----------|
| top               | sztring   | A kérelemben visszaadni kívánt adatsorok száma. A maximális érték és az alapértelmezett érték, ha nincs megadva, 10000. Ha több sor van a lekérdezésben, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldalának lekérésére használható. | Nem |
| kihagyása              | int      | A lekérdezésben kihagyni kívánt sorok száma. Használja ezt a paramétert a nagy adathalmazokon keresztüli lapra. Például a Top = 10000 és a skip = 0 lekérdezi az első 10000 adatsort, a Top = 10000 és a skip = 10000 lekéri a következő 10000 sort, és így tovább. | Nem |
| filter (szűrő)            | sztring   | A kérelem *Filter* paraméterében egy vagy több olyan utasítás található, amely a válasz sorait szűri. Minden utasítás tartalmaz egy mezőt és egy értéket, amely társítva van az `eq` vagy `ne` operátorhoz, és a utasítások kombinálhatók a vagy a használatával `and` `or` . Íme néhány példa a *szűrési* paraméterekre:<br/><br/> *Filter = meg EQ "O365"*<br/> *Filter = meg EQ "O365"* vagy (*Channel EQ "viszonteladó"*)<br/><br/> A következő mezőket adhatja meg:<br/><br/>**Meg**<br/>**serviceName**<br/>**csatorna**<br/>**customerTenantId**<br/>**Customername (**<br/>**productId**<br/>**productName**  | Nem |
| groupby           | sztring   | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítést. A következő mezőket adhatja meg:<br/><br/>**Meg**<br/>**serviceName**<br/>**csatorna**<br/>**customerTenantId**<br/>**Customername (**<br/>**productId**<br/>**productName**<br/><br/> A visszaadott adatsorok tartalmazzák a *groupby* paraméterben megadott mezőket, valamint a következőket:<br/><br/>**licensesDeployed**<br/>**licensesSold**  | Nem |
| processedDateTime | DateTime | Megadhatja azt a dátumot, amelyből a használati adatokat feldolgozták. Alapértelmezett érték az adatok feldolgozásának legkésőbbi dátuma | Nem |

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse a következő mezőket tartalmazza, amelyek a telepített licencekre vonatkozó információkat tartalmaznak.

| Mező             | Típus     | Leírás                           |
|-------------------|----------|---------------------------------------|
| Meg       | sztring   | Szolgáltatási kód                          |
| serviceName       | sztring   | Szolgáltatásnév                          |
| csatorna           | sztring   | Csatorna neve, viszonteladó                |
| customerTenantId  | sztring   | Az ügyfél egyedi azonosítója    |
| Customername (      | sztring   | Ügyfél neve                         |
| productId         | sztring   | A termék egyedi azonosítója     |
| productName       | sztring   | Terméknév                          |
| licensesDeployed  | hosszú     | Telepített licencek száma           |
| licensesSold      | hosszú     | Eladott licencek száma               |
| processedDateTime | DateTime | Az adatok legutóbbi feldolgozásának dátuma |

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
