---
title: Előfizetés használati adatainak lekérése erőforrás szerint
description: A ResourceUsageRecord erőforrás használatával lekértheti az ügyfél erőforrás-használati rekordjait adott Azure-szolgáltatásokra vagy -erőforrásokra vonatkozóan az aktuális számlázási időszakban.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 81c8fcb868f7d4d50e23d69579138a6c03e9ea4ae93058d141a029c103489dcb
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992840"
---
# <a name="get-usage-data-for-subscription-by-resource"></a>Előfizetés használati adatainak lekérése erőforrás szerint

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk a **ResourceUsageRecord erőforrás leépítését** ismerteti. Ez az erőforrás az Azure-csomagban kiépített egyes erőforrások havi összesített összegeként szolgál. Ezzel az erőforrással lekérte egy ügyfél erőforrás-használati rekordjait adott Azure-szolgáltatásokra vagy -erőforrásokra vonatkozóan az aktuális számlázási időszakban. Ez az API olyan adatokat ad vissza, amelyek korábban nem voltak elérhetők az Azure-beli költési API-kon keresztül.

*Ez az útvonal nem támogatja Microsoft Azure (MS-AZR-0145P) előfizetéseket.*

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító

## <a name="c"></a>C\#

Egy adott Azure-szolgáltatás vagy -erőforrás erőforrás-használati rekordjainak lekérte az aktuális számlázási időszakban:

1. Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**

2. Hívja meg a Subscriptions (Előfizetések) és **a UsageRecords**(Használati adatok) tulajdonságot, majd a **Resources (Erőforrások) tulajdonságot.** Befejezésként hívja meg a Get() vagy a GetAsync() metódust.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Osztály: **GetSubscriptionUsageRecordsByResource.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/resourceusagerecords HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Ez a táblázat felsorolja az ügyfél minősített használati információinak lekérdezhető lekérdezési paramétereit.

| Név                   | Típus     | Kötelező | Leírás                               |
|------------------------|----------|----------|-------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az ügyfélnek megfelelő GUID.     |
| **subscription-id**    | **guid** | Y        | Egy Partnerközpont-előfizetési erőforrás azonosítójának megfelelő [](subscription-resources.md#subscription)GUID, amely egy Microsoft Azure-előfizetést (MS-AZR-0145P) vagy egy Azure-csomagot képvisel. *Az Azure-csomag előfizetési  erőforrásaihoz ebben az útvonalban adja meg a **csomagazonosítót előfizetés-azonosítóként.*** |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy **PagedResourceCollection \<ResourceUsageRecord>** erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Egy hálózati nyomkövetési eszközzel olvassa be ezt a kódot, a hiba típusát és a további paramétereket. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
