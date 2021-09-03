---
title: Egy előfizetés lekérése azonosító alapján
description: Lekért egy előfizetési erőforrást, amely megfelel az ügyfél-azonosítónak és az előfizetés-azonosítónak.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 26825084d89648affe904b9415d3143b3e65ebae
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123455984"
---
# <a name="get-a-subscription-by-id"></a>Egy előfizetés lekérése azonosító alapján

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekért [egy előfizetési](subscription-resources.md) erőforrást, amely megfelel az ügyfél-azonosítónak és az előfizetés-azonosítónak.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, a következő irányítópulton Partnerközpont [ki:](https://partner.microsoft.com/dashboard). Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

## <a name="c"></a>C\#

Az előfizetés azonosító alapján való beszerzéséhez először szerezze be az előfizetési műveletek interfészét az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus hívásával az ügyfél azonosítójával, az ügyfél azonosításához pedig a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódussal az előfizetés azonosításához. Ezzel a [**felülettel lekérhető**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) az előfizetés részleteinek lekérése a [**Get hívása használatával.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionID;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionID).Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** Partnerközpont SDK Samples **Osztály:** GetSubscription.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **KAP** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az előfizetés lekért lekérdezési paramétereit.

| Név                    | Típus     | Kötelező | Leírás                               |
|-------------------------|----------|----------|-------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **guid** | Y        | Az ügyfélnek megfelelő GUID.     |
| **id-for-subscription** | **guid** | Y        | Az előfizetéshez tartozó GUID. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy [Előfizetés](subscription-resources.md) erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd a Partnerközpont [REST-hibakódok között.](error-codes.md)

### <a name="response-example-for-a-microsoft-azure-subscription"></a>Példa válasz egy Microsoft Azure előfizetésre

```http
HTTP/1.1 200 OK
Content-Length: 833
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CV: 7v11Wa//5EuGEo+A.0
MS-ServerId: 202010406
Date: Fri, 27 Jan 2017 21:51:40 GMT

{
    "id": "A356AC8C-E310-44F4-BF85-C7F29044AF99",
    "entitlementId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
    "offerId": "MS-AZR-0145P",
    "offerName": "Microsoft Azure",
    "friendlyName": "Microsoft Azure",
    "quantity": 1,
    "unitType": "Usage-based",
    "creationDate": "2016-05-10T07:30:05.427Z",
    "effectiveStartDate": "2016-05-10T00:00:00Z",
    "commitmentEndDate": "9999-12-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": false,
    "billingType": "usage",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/MS-AZR-0145P?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "B23FDEDD-D6BD-415A-8B71-3624C81C9644",
    "attributes": {
        "etag": "eyJpZCI6ImEzNTZhYzhjLWUzMTAtNDRmNC1iZjg1LWM3ZjI5MDQ0YWY5OSIsInZlcnNpb24iOjJ9",
        "objectType": "Subscription"
    }
}
```

### <a name="response-example-for-an-add-on-subscription"></a>Példa egy bővítmény-előfizetésre

A bővítmény-előfizetésre adott válasz tartalmazza a szülő-előfizetés azonosítóját a törzsben és a hivatkozásokban.

```http
HTTP/1.1 200 OK
Content-Length: 1132
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6eacec93-852d-4167-9d96-c57809bea7ed
MS-RequestId: 22bfd0fb-d1e6-4a8f-aa1a-124b7c820d80
MS-CV: cmde2DtbuUWi8JLq.0
MS-ServerId: 201022015
Date: Fri, 27 Jan 2017 00:12:53 GMT

{
    "id": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
    "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
    "offerName": "Exchange Online Archiving for Exchange Online",
    "friendlyName": "Some friendly name",
    "quantity": 2,
    "unitType": "Licenses",
    "parentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
    "creationDate": "2017-01-25T23:01:08.693Z",
    "effectiveStartDate": "2017-01-25T00:00:00Z",
    "commitmentEndDate": "2018-02-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": true,
    "billingType": "license",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
            "method": "GET",
            "headers": []
        },
        "parentSubscription": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "CF3B0E37-BE0B-4CDD-B584-D1A97D98A922",
    "attributes": {
        "etag": "eyJpZCI6Ijk2OGJhMWNmLWMxNDYtNGFkZi1hMzAwLTMwOGRjZjcxOGVlZSIsInZlcnNpb24iOjF9",
        "objectType": "Subscription"
    }
}
```
### <a name="response-example-for-a-new-commerce-subscription"></a>Válasz példa egy új kereskedelmi előfizetésre

> [!Note] 
> Az új kereskedelmi módosítások jelenleg csak az M365/D365 új kereskedelmi felhasználói élmény technikai előzetesének részét képezi partnerek számára érhetők el.

```http
HTTP/1.1 200 OK
Content-Length: 1132
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4ercec93-852d-4167-9d96-c57809bea7ed
MS-RequestId: 54sfd0fb-d1e6-4a8f-aa1a-124b7c820d80
MS-CV: cmde2DtbuUWi8JLq.0
MS-ServerId: 201022015
Date: Fri, 19 Feb 2021 00:14:53 GMT

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
    "status": "expired", 
    "autoRenewEnabled": false, 
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
