---
title: Használati összefoglalás beszerzése az ügyfél összes előfizetéséhez
description: A CustomerUsageSummary-erőforrás segítségével lekérheti az adott Azure-szolgáltatás vagy-erőforrás ügyfél általi használatát az aktuális számlázási időszak alatt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767960"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a>Használati összefoglalás beszerzése az ügyfél összes előfizetéséhez

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A **CustomerUsageSummary** -erőforrás segítségével lekérheti az adott Azure-szolgáltatás vagy-erőforrás ügyfél általi használatát az aktuális számlázási időszak alatt.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél-előfizetések használati összegzésének beszerzése:

1. A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.

2. Hívja meg a **UsageSummary** tulajdonságot, amelyet a **Get ()** vagy a **GetAsync ()** metódus követ:

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

Példaként tekintse meg a következőket:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Osztály: **GetCustomerUsageSummary.cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagesummary http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja a szükséges lekérdezési paramétert, hogy lekérje az ügyfél névleges használati adatait.

| Név                   | Típus     | Kötelező | Leírás                           |
|------------------------|----------|----------|---------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az ügyfélhez tartozó GUID. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus egy **CustomerUsageSummary** -erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a>Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésre

Ebben a példában az ügyfél egy **145P Azure TB** -ajánlatot vásárolt.

*Microsoft Azure (MS-AZR-0145P) előfizetéssel rendelkező ügyfelek esetében nem változik az API-válasz.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a>Válasz példa az Azure-csomagra

Ebben a példában az ügyfél egy Azure-csomagot vásárolt.

*Az Azure-csomagokkal rendelkező ügyfelek esetében az API-válasz módosításai a következők:*

- a **currencyLocale** helyére a **currencyCode**
- a **usdTotalCost** egy új mező

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
