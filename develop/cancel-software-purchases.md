---
title: Szoftvervásárlások lemondása
description: Önkiszolgáló lehetőség a szoftver-előfizetések és a folyamatos szoftvervásárlások lemondására Partnerközpont API-k használatával.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7dfa5122c585a8519312e8492922f718a51972f177a12d7431015e1cdcb5d06
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992194"
---
# <a name="cancel-software-purchases"></a>Szoftvervásárlások lemondása

Az Partnerközpont API-k használatával megszüntetheti a szoftver-előfizetéseket és a folyamatos szoftvervásárlásokat (felhasználhatja azokat a vásárlásokat a vásárlás dátumtól számított lemondási időszakban). Ilyen lemondáshoz nem kell támogatási jegyet létrehoznia, és ehelyett a következő önkiszolgáló módszereket használhatja.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Szoftverrendelés lemondása:

1. Adja át a fiók hitelesítő adatait a [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy lekért egy [**IPartner-felületet**](/dotnet/api/microsoft.store.partnercenter.ipartner) a partnerműveletekkel kapcsolatban.

2. Válassza ki azt a [megrendelést,](order-resources.md#order) amelyről le szeretné mondani a rendelést. Hívja meg [**a Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóját, majd az **Orders.ById()** metódust a rendelésazonosítóval.

3. A **rendelés lekérése** érdekében hívja meg a Get vagy **a GetAsync** metódust.

4. Állítsa az [**Order.Status**](order-resources.md#order) tulajdonságot a `cancelled` következőre: .

5. (Nem kötelező) Ha meg szeretne adni bizonyos sorelemeket a megszakításhoz, állítsa az [**Order.LineItems**](order-resources.md#order) elemet a megszakítani kívánt sorelemek listájára.

6. Frissítse a sorrendet a **Patch()** metódussal.

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus     | Kérés URI-ja                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Javítás** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1 |

### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél törléséhez használja az alábbi lekérdezési paramétereket.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú ügyfélbérlő-azonosító, amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |
| **order-id (rendelésazonosító)** | **sztring** | Y        | Az érték egy sztring, amely a megszakítani kívánt rendelés azonosítóját jelöli. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a>Példa kérésre

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus megszakított sorelemeket ad vissza a rendeléshez.

A rendelés állapota vagy  megszakítva állapotúként lesz megjelölve, ha a  rendelésben lévő összes sorelemet visszavonják, vagy akkor fejeződnek be, ha nem minden sorelemet törölnek.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

A következő példaválaszban láthatja, hogy az ajánlatazonosítóval együtt a sortétel mennyisége **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** nullára (0) vált. Ez a módosítás azt jelenti, hogy a megszakításra megjelölt sorelem sikeresen törölve lett. A példasorrend más sorelemeket is tartalmaz, amelyeket nem töröltek, ami azt jelenti, hogy a teljes rendelés állapota befejezettként lesz megjelölve, nem **megszakítva.**

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
