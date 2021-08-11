---
title: Előfizetés kiépítési állapotának lekérése
description: Hogyan lehet lekért előfizetés-kiépítési állapotot egy ügyfél-előfizetéshez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b36776279171186da7d81f9c1ff3d0828206fc2749ab8108f882ad7460575d60
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995560"
---
# <a name="get-subscription-provisioning-status"></a>Előfizetés kiépítési állapotának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Hogyan lehet lekért előfizetés-kiépítési állapotot egy ügyfél-előfizetéshez.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító.

- A művelet végrehajtásához delegált rendszergazdai engedélyek szükségesek az előfizetésen.

## <a name="c"></a>C\#

Az előfizetés kiépítési állapotának leához először használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához. Ezután az előfizetési műveletek interfészének lehívásához hívja meg a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust az előfizetés azonosítójával. Ezután a [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) tulajdonság használatával szerezzen be egy felületet az aktuális előfizetés kiépítési állapotműveletéhez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) metódust a [**SubscriptionProvisioningStatus objektum**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) lekéréséhez.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/provisioningstatus HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.

| Név            | Típus   | Kötelező | Leírás                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| ügyfél-azonosító     | sztring | Yes      | Egy GUID formátumú sztring, amely azonosítja az ügyfelet.     |
| subscription-id | sztring | Yes      | Egy GUID formátumú sztring, amely azonosítja az előfizetést. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén a válasz törzse tartalmaz egy [SubscriptionProvisioningStatus erőforrást.](subscription-resources.md#subscriptionprovisioningstatus)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a>Megjegyzések

- Licenc módosításakor a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) állapotmezője "pending" (függőben) lesz.

- Az állapot mező 15 percenként frissül.
