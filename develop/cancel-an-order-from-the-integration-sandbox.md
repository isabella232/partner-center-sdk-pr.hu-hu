---
title: Megrendelés megszakítása az integrációs munkaterületről
description: Megtudhatja, hogyan vonhatja vissza a különböző típusú előfizetési rendeléseket a partner Center API-kkal az integrációs homokozó fiókjaiból.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 363bf209e27d5223259c8c533710a3b35bbef1e6
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768596"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Megrendelés megszakítása az integrációs munkaterületről a partner Center API-k használatával

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan lehet a partner Center API-kkal különböző típusú előfizetési rendeléseket lemondani az Integration sandbox-fiókokból. Az ilyen megrendelések tartalmazhatnak fenntartott példányokat, szoftvereket és kereskedelmi Piactéri szoftvereket (SaaS) előfizetési rendeléseket.

>[!NOTE]
>Felhívjuk a figyelmét arra, hogy a fenntartott példányok vagy a kereskedelmi Piactéri SaaS-előfizetési megrendelések törlése csak az integrációs munkaterületről lehetséges.  

Ha az API-n keresztül szeretné lemondani a szoftver éles sorrendjét, használja a [Cancel-Software-](cancel-software-purchases.md)Buys parancsot.
Az irányítópulton keresztül is megszakíthatja a szoftver éles rendeléseit a [vásárlás megszakításával](/partner-center/csp-software-subscriptions).

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy integrációs sandbox-partner fiók egy aktív fenntartott példány/szoftver/harmadik féltől származó SaaS-előfizetési rendeléssel rendelkező ügyféllel.

## <a name="c"></a>C\#

Ha meg szeretné szüntetni a rendelést az integrációs munkaterületről, adja át a fiók hitelesítő adatait a [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metódusnak, hogy lekérje a partneri műveletek elvégzéséhez szükséges [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) felületet.

Egy adott [megrendelés](order-resources.md#order)kiválasztásához használja a partner műveleti és Call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és adja meg az ügyfelet, majd a **`Orders.ById()`** megrendelés azonosítójának megadásával adja meg a sorrendet, végül **`Get`** vagy **`GetAsync`** a lekérési módszert.

Állítsa be a tulajdonságot a értékre, [**`Order.Status`**](order-resources.md#order) `cancelled` és használja a **`Patch()`** metódust a sorrend frissítéséhez.

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus     | Kérés URI-ja                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **JAVÍTÁS** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél törléséhez használja a következő lekérdezési paramétert.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti. |
| **megrendelés azonosítója** | **karakterlánc** | Y        | Az érték a megszakítani kívánt sorrendi azonosítókat jelölő karakterlánc. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a>Példa kérésre

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a metódus visszaadja a megszakított sorrendet.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
