---
title: Licencek üzembehelyezési adatainak lekérése
description: Telepítési információk lekérte Office Dynamics-licencekhez.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9eb0dc655affb2216b11635e58e00ed6464d6792
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445663"
---
# <a name="get-licenses-deployment-information"></a>Licencek üzembehelyezési adatainak lekérése

Telepítési információk lekérte Office Dynamics-licencekhez.

## <a name="prerequisites"></a>Előfeltételek

Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="uri-parameters"></a>URI-paraméterek

| Paraméter         | Típus     | Leírás | Kötelező |
|-------------------|----------|-------------|----------|
| top               | sztring   | A kérésben visszaadni kívánt adatsorok száma. Ha nincs megadva, a maximális érték és az alapértelmezett érték 10000. Ha a lekérdezés több sort tartalmaz, a válasz törzse tartalmaz egy következő hivatkozást, amely a következő adatoldal lekérésére használható. | Nem |
| Ugrál              | int      | A lekérdezésben kihagyni kívánt sorok száma. Ezzel a paraméterrel nagy adatkészletek között lapokat laposszunk. Például a top=10000 és a skip=0 lekéri az első 10000 adatsort, a top=10000 és a skip=10000 a következő 10000 adatsort és így tovább. | Nem |
| filter (szűrő)            | sztring   | A *kérés* szűrőparamétere egy vagy több olyan utasításokat tartalmaz, amelyek szűrik a válasz sorait. Minden utasítás tartalmaz egy mezőt és egy értéket, amely az vagy operátorhoz van társítva, és az utasítások a vagy a használatával `eq` `ne` `and` `or` kombinálhatók. Íme néhány példa *szűrőparaméterre:*<br/><br/> *filter=serviceCode eq 'O365'*<br/> *filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)<br/><br/> A következő mezőket adhatja meg:<br/><br/>**serviceCode**<br/>**serviceName (szolgáltatásnév)**<br/>**Csatorna**<br/>**customerTenantId (customerTenantId)**<br/>**customerName (ügyfél neve)**<br/>**Termelés**<br/>**Productname**  | Nem |
| groupby (csoportosítás)           | sztring   | Olyan utasítás, amely csak a megadott mezőkre alkalmazza az adatösszesítőt. A következő mezőket adhatja meg:<br/><br/>**serviceCode**<br/>**serviceName (szolgáltatásnév)**<br/>**Csatorna**<br/>**customerTenantId (customerTenantId)**<br/>**customerName (ügyfél neve)**<br/>**Termelés**<br/>**Productname**<br/><br/> A visszaadott adatsorok tartalmazzák a *groupby* paraméterben megadott mezőket és a következőket:<br/><br/>**licensesDeployed**<br/>**licensesSold**  | Nem |
| processedDateTime | DateTime | Megadhatja a használati adatok feldolgozásának dátumát. Alapértelmezés szerint az adatok feldolgozásának legutóbbi dátuma | Nem |

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

Sikeres művelet esetén a válasz törzse a következő mezőket tartalmazza, amelyek az üzembe helyezett licencekkel kapcsolatos adatokat tartalmazzák.

| Mező             | Típus     | Leírás                           |
|-------------------|----------|---------------------------------------|
| serviceCode       | sztring   | Szolgáltatáskód                          |
| serviceName (szolgáltatásnév)       | sztring   | Szolgáltatásnév                          |
| Csatorna           | sztring   | Csatorna neve, viszonteladó                |
| customerTenantId (customerTenantId)  | sztring   | Az ügyfél egyedi azonosítója    |
| customerName (ügyfél neve)      | sztring   | Ügyfél neve                         |
| productId         | sztring   | A termék egyedi azonosítója     |
| Productname       | sztring   | Terméknév                          |
| licensesDeployed  | hosszú     | Telepített licencek száma           |
| licensesSold      | hosszú     | Eladott licencek száma               |
| processedDateTime | DateTime | Az adatok utolsó feldolgozásának dátuma |

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
