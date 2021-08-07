---
title: Az ügyfél előfizetésének használati összegzése
description: A SubscriptionUsageSummary erőforrás használatával lekértheti egy adott Azure-szolgáltatás vagy -erőforrás előfizetés-használati összegzését az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df7757807256fee8326969011f4d038c981c07362ee354ef929e592a7931a728
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992772"
---
# <a name="get-usage-summary-for-customers-subscription"></a>Az ügyfél előfizetésének használati összegzése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A **SubscriptionUsageSummary** erőforrás használatával lekért egy előfizetés használati összegzését egy ügyfélhez. Ez az erőforrás egy adott Azure-szolgáltatás vagy -erőforrás előfizetés-használati összegzését jelöli az aktuális számlázási időszakban.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító

## <a name="c"></a>C\#

Az előfizetés használatának összegzése egy ügyfél előfizetéséhez:

1. Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**

2. Ezután hívja meg a Subscriptions tulajdonságot és **a UsageSummary tulajdonságot.** Befejezésként hívja meg a Get() vagy a GetAsync() metódust.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Osztály: **GetSubscriptionUsageSummary.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/usagesummary HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paramétereit.

| Név                   | Típus     | Kötelező | Leírás                               |
|------------------------|----------|----------|-------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az ügyfélnek megfelelő GUID.     |
| **subscription-id**    | **guid** | Y        | Egy előfizetés azonosítójának megfelelő GUID. Azure-csomag esetén ez a megfelelő előfizetési Partnerközpont [azonosítója,](subscription-resources.md#subscription)amely az Azure-csomagnak megfelel. *Az Azure-csomag előfizetési  erőforrásaihoz ebben az útvonalban adja meg a **csomagazonosítót előfizetés-azonosítóként.*** |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy **SubscriptionUsageSummary** erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Egy hálózati nyomkövetési eszközzel olvassa be ezt a kódot, a hiba típusát és a további paramétereket. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésre

Ebben a példában az ügyfél megvásárolt egy **145P-s Azure PayG-ajánlatot.**

*A Microsoft Azure (MS-AZR-0145P) előfizetéssel nem lesz változás az API-válaszban.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>AZURE-csomag REST-válasza

Ebben a példában az ügyfél megvásárolt egy Azure-csomag.

*Az Azure-csomagokat használó ügyfelek esetében a következő API-válaszváltozások vannak:*

- **A currencyLocale** helyére a **currencyCode van lecserélve**
- **A usdTotalCost** egy új mező

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
