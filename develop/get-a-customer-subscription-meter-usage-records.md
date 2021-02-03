---
title: Előfizetés használati adatainak lekérése mérő szerint
description: A MeterUsageRecord erőforrás-gyűjtemény használatával beolvashatja az adott Azure-szolgáltatásokra vagy-erőforrásokra vonatkozó használati adatokat az aktuális számlázási időszak alatt.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767972"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>Előfizetés használati adatainak lekérése mérő szerint

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A **MeterUsageRecord** erőforrás-gyűjtemény használatával beolvashatja az adott Azure-szolgáltatásokra vagy-erőforrásokra vonatkozó használati adatokat az aktuális számlázási időszak alatt. Ez az erőforrás-gyűjtemény az aktuális számlázási ciklushoz tartozó összes mérőszám összesített összegét képviseli a teljes Azure-csomagon belül.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító

*Ez az új útvonal egyenértékű a következővel `subscriptions/{subscription-id}/usagerecords/resources` :, amely továbbra is csak Microsoft Azure (MS-AZR-0145P) előfizetések esetében fog működni.* Ez az új útvonal Microsoft Azure (MS-AZR-0145P) előfizetéseket és Azure-csomagokat is támogat. Ahhoz, hogy ezt az információt megkapja az Azure-csomaghoz, át kell váltania erre az új útvonalra. A következő szakaszokban említett tulajdonságok kivételével a válasz megegyezik a régi útvonallal.

## <a name="c"></a>C\#

Adott Azure-szolgáltatás vagy-erőforrás díjszabási használati adatainak beolvasása az aktuális számlázási időszakban:

1. A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.

2. Hívja meg az előfizetések tulajdonságot, és a **UsageRecords**, majd a **meters** tulajdonságot. Fejezze be a Get () vagy a GetAsync () metódus meghívásával.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

Példaként tekintse meg a következő mintát:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSamples**
- Osztály: **GetSubscriptionUsageRecordsByMeter.cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/meterusagerecords http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Ez a táblázat felsorolja a szükséges lekérdezési paramétereket, hogy megkapják az ügyfél névleges használati adatait.

| Név                   | Típus     | Kötelező | Leírás                               |
|------------------------|----------|----------|-------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az ügyfélhez tartozó GUID.     |
| **előfizetés-azonosító**    | **guid** | Y        | A partner Center [előfizetési erőforrás](subscription-resources.md#subscription)azonosítójának megfelelő GUID, amely egy Microsoft Azure (MS-AZR-0145P) előfizetést vagy egy Azure-csomagot jelöl. *Az Azure-csomag előfizetési erőforrásai esetében adja meg az **előfizetési azonosítóként** szolgáló **díjcsomag azonosítóját** ebben az útvonalban.* |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus **egy \<MeterUsageRecord> PagedResourceCollection** -erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek beolvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Válasz példa Microsoft Azure (MS-AZR-0145P) előfizetésekre

Ebben a példában az ügyfél megvásárolta az **Azure TB 145P**.

*Microsoft Azure (MS-AZR-0145P) előfizetéssel rendelkező ügyfelek esetében nem változik az API-válasz.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>REST-válaszok – példa az Azure-csomagra

Ebben a példában az ügyfél egy Azure-csomagot vásárolt.

*Az Azure-csomaggal rendelkező ügyfelek esetében az API-válasz módosításai a következők:*

- a **currencyLocale** helyére a **currencyCode**
- a **usdTotalCost** egy új mező

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
