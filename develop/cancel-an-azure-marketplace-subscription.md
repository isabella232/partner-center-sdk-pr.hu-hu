---
title: Kereskedelmi piactér vagy új kereskedelmi előfizetés lemondása
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat kereskedelmi piactér vagy új kereskedelmi előfizetés erőforrásának lemondására, amely megfelel egy ügyfélnek és egy előfizetés-azonosítónak.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cbfe17ba4880c303c3f3ba01db5955a557eb04e2
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456137"
---
# <a name="cancel-a-commercial-marketplace-or-new-commerce-subscription-using-partner-center-apis"></a>Kereskedelmi piactér vagy új kereskedelmi előfizetés lemondása Partnerközpont API-k használatával

**A következőkre vonatkozik:** Partnerközpont

Ez a cikk azt ismerteti, hogyan használhatja a Partnerközpont API-t az ügyfél- és előfizetés-azonosítónak megfelelő kereskedelmi piactér vagy új [kereskedelmi](subscription-resources.md) előfizetés erőforrásának lemondására.

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="partner-center-dashboard-method"></a>Partnerközpont irányítópult metódusa

Kereskedelmi piactér-előfizetés lemondása az Partnerközpont irányítópulton:

1. [Válasszon ki egy ügyfelet.](get-a-customer-by-name.md)

2. Válassza ki a megszüntetni kívánt előfizetést.

3. Válassza az **Előfizetés lemondása** lehetőséget, majd válassza a **Küldés lehetőséget.**

## <a name="c"></a>C\#

Az ügyfél előfizetésének lemondása:

1. [Szerezze be az előfizetést azonosító alapján.](get-a-subscription-by-id.md)

2. Módosítsa az előfizetés [**Status (Állapot) tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) Az **állapotkódokkal kapcsolatos információkért** [lásd: SubscriptionStatus enumerálás.](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)

3. A módosítás után használja a gyűjteményt, **`IAggregatePartner.Customers`** és hívja meg a **ById() metódust.**

4. Hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)

5. Hívja meg **a Patch() metódust.**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a>Mintakonzol-tesztalkalmazás

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: PartnerSDK.FeatureSample **osztály:** UpdateSubscription.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus    | Kérés URI-ja                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **JAVÍTÁS** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az előfizetés felfüggesztéséhez szükséges lekérdezési paramétert.

| Név                    | Típus     | Kötelező | Leírás                               |
|-------------------------|----------|----------|-------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **guid** | Y        | Az ügyfélnek megfelelő GUID.     |
| **id-for-subscription** | **guid** | Y        | Az előfizetéshez tartozó GUID. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérelem **törzsében** teljes előfizetési erőforrásra van szükség. Győződjön meg **arról, hogy** az Állapot tulajdonság frissítve lett.

### <a name="request-example-for-a-commercial-marketplace-subscription"></a>Példa kérése kereskedelmi piactér-előfizetéshez

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [{
        "type": "Full",
        "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
    }],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "publisherName": "publisher Name",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {"objectType": "Subscription"},
}
```

### <a name="request-example-for-a-new-commerce-subscription"></a>Példa kérése új kereskedelmi előfizetéshez

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el.

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "id": "a4c1340d-6911-4758-bba3-0c4c6007d161",
    "offerId": "CFQ7TTC0LH18:0001:CFQ7TTC0K971",
    "offerName": "Microsoft 365 Business Basic",
    "friendlyName": "Microsoft 365 Business Basic",
    "productType": {
        "id": "OnlineServicesNCE",
        "displayName": "OnlineServicesNCE"
    },
    "quantity": 1, 
    "unitType": "Licenses",
    "hasPurchasableAddons": false,
    "creationDate": "2021-01-14T16:57:15.0966728Z",
    "effectiveStartDate": "2021-01-14T16:57:14.498252Z",
    "commitmentEndDate": "2022-01-13T00:00:00Z",
    "status": "deleted", // original value = “active”
    "autoRenewEnabled": true, 
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1Y",
    "renewalTermDuration": "",
    "refundOptions": [
        {
            "type": "Full",
            "expiresAt": "2021-01-15T00:00:00Z"
        }
    ],
    "isMicrosoftProduct": true,
    "partnerId": "",
    "attentionNeeded": false,
    "actionTaken": false,
    "contractType": "subscription",
    "links": {
        "product": {
            "uri": "/products/CFQ7TTC0LH18?country=US",
            "method": "GET",
            "headers": []
        },
        "sku": {
            "uri": "/products/CFQ7TTC0LH18/skus/0001?country=US",
            "method": "GET",
            "headers": []
        },
        "availability": {
            "uri": "/products/CFQ7TTC0LH18/skus/0001/availabilities/CFQ7TTC0K971?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/d8202a51-69f9-4228-b900-d0e081af17d7/subscriptions/a4c1340d-6911-4758-bba3-0c4c6007d161",
            "method": "GET",
            "headers": []
        }
    },
    "publisherName": "Microsoft Corporation",
    "orderId": "34b37d7340cc",
    "attributes": {
        "objectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez a módszer sikeres, a törölt [előfizetés](subscription-resources.md) erőforrás-tulajdonságait adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1322
Content-Type: application/json; charset=utf-8
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
X-Locale: en-US

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [
        {
            "type": "Full",
            "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
        }
    ],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "links": {
        "product": {
            "uri": "/products/DZH318Z0BXWC?country=US",
            "method": "GET",
            "headers": []
        },
        "sku": {
            "uri": "/products/DZH318Z0BXWC/skus/0001?country=US",
            "method": "GET",
            "headers": []
        },
        "availability": {
            "uri": "/products/DZH318Z0BXWC/skus/0001/availabilities/DZH318Z0BMJX?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/5921f00a-32c0-4457-aaa1-e8018c650895/subscriptions/6e7aa601-629e-461b-8933-0898c3cc3c7c",
            "method": "GET",
            "headers": []
        }
    },
    "publisherName": "publishe rName",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {
        "etag": "",
        "objectType": "Subscription"
    }
}
```
