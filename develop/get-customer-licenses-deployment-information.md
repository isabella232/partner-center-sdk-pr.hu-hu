---
title: Ügyféllicencek üzembehelyezési adatainak lekérése
description: Licencek üzembe helyezési elemzésének le szolgáltatása egy adott ügyfél számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 91fe9da185aa59025d4dc8263257b207edb4a5be
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446462"
---
# <a name="get-customer-licenses-deployment-information"></a>Ügyféllicencek üzembehelyezési adatainak lekérése

Licencek üzembe helyezési elemzésének le szolgáltatása egy adott ügyfél számára.

> [!NOTE]
> Ezt a forgatókönyvet a Licencek le get deployment information (Licencek üzembe helyezési [információinak le szolgáltatása) szuperküldi le.](get-licenses-deployment-information.md)

## <a name="prerequisites"></a>Előfeltételek

Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Egy adott ügyfél üzembe helyezésével kapcsolatos összesített adatok lekéréséhez először hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához. Ezután szerezze be az ügyfélszintű elemzési gyűjtemény műveleteinek felületét az [**Analytics tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) Ezután a [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) (Licencek) tulajdonságból olvassa be az ügyfélszintű licencelemzési gyűjtemény felületét. Végül hívja meg a [**Deployment.Get metódust**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) a licencek üzembe helyezésével kapcsolatos összesített adatok lehívására. Ha a metódus sikeres, a [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objektumok gyűjteményét fogja kapni.

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/analytics/licenses/deployment HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél azonosításához használja a következő elérésiút-paramétert.

| Név        | Típus | Kötelező | Leírás                                                |
|-------------|------|----------|------------------------------------------------------------|
| ügyfélazonosító | guid | Igen      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz törzse sikeres, a [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) erőforrások gyűjteményét tartalmazza, amelyek információt nyújtanak az üzembe helyezett licencekkel kapcsolatban.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1012
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CV: deEp2Wy6DUitMCYA.0
MS-ServerId: 102030524
Date: Wed, 15 Mar 2017 01:19:18 GMT

{
    "totalCount": 3,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 1,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 5,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 2,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
