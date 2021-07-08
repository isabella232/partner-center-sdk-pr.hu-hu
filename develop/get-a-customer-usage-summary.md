---
title: Egy ügyfél összes előfizetésének használati összegzése
description: A CustomerUsageSummary erőforrással lekértheti egy adott Azure-szolgáltatás vagy -erőforrás ügyfélhasználatát az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88c69637c94b9263ede6924cf2dd09513aa00f70
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874618"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a>Egy ügyfél összes előfizetésének használati összegzése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **CustomerUsageSummary** erőforrással lekértheti egy adott Azure-szolgáltatás vagy -erőforrás ügyfélhasználatát az aktuális számlázási időszakban.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="c"></a>C\#

Az ügyfél összes előfizetésének használati összegzése:

1. Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById()** metódust.

2. Hívja meg **a UsageSummary** tulajdonságot, majd a **Get() vagy** **a GetAsync() metódust:**

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Osztály: **GetCustomerUsageSummary.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paraméterét.

| Név                   | Típus     | Kötelező | Leírás                           |
|------------------------|----------|----------|---------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az ügyfélnek megfelelő GUID. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha sikeres, ez a metódus egy **CustomerUsageSummary** erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Egy hálózati nyomkövetési eszközzel olvassa be ezt a kódot, a hiba típusát és a további paramétereket. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a>Példa válasz Microsoft Azure (MS-AZR-0145P) előfizetésre

Ebben a példában az ügyfél megvásárolt egy **145P Azure PayG-ajánlatot.**

*A Microsoft Azure (MS-AZR-0145P) előfizetéssel nem változik az API-válasz.*

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

### <a name="response-example-for-azure-plan"></a>Azure-csomag válasz példája

Ebben a példában az ügyfél megvásárolt egy Azure-csomag.

*Az Azure-csomaggal használó ügyfelek esetében az API-válasz a következő változásokat tartalmazza:*

- **A currencyLocale** helyett **a currencyCode található**
- **Az usdTotalCost** egy új mező

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
