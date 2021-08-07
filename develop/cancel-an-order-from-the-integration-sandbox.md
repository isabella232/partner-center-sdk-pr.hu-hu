---
title: Rendelés visszavonása az integrációs védőfalból
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat az integrációs sandbox-fiókokból származó előfizetési rendelések különböző típusainak lemondására.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c4843dc4626c2bb2cd1b2784f3df1c323e2eceea2edbb6330a9bd9dbcea4dc1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992211"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Rendelés visszavonása az integrációs védőfalról az Partnerközpont API-k használatával

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk azt ismerteti, hogyan használhatók Partnerközpont API-k az integrációs sandbox-fiókokból származó előfizetési rendelések különböző típusainak lemondására. Ilyen rendelések lehetnek fenntartott példányok, szoftverek és kereskedelmi piactéri Szolgáltatott szoftver (SaaS) előfizetési rendelések.

> [!NOTE] 
> Vegye figyelembe, hogy a fenntartott példányok vagy a kereskedelmi piactéri SaaS-előfizetési rendelések lemondása csak az integrációs sandbox-fiókokból lehetséges. A 60 napnál régebbi sandbox-rendelések nem szakíthatóak meg a Partnerközpont.

Az API-n keresztüli szoftverrendelések lemondásához használja a [cancel-software-purchases parancsot.](cancel-software-purchases.md)
Az irányítópulton keresztül is visszavonhatja az éles szoftverrendeléseket [a vásárlás lemondásával.](/partner-center/csp-software-subscriptions)

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Integrációs sandbox partnerfiók egy olyan ügyféllel, aki aktív fenntartott példányokkal/szoftverekkel/külső SaaS-előfizetési rendelésekkel rendelkezik.

## <a name="c"></a>C\#

Ha le kell mondania egy rendelést az integrációs védőfalról, adja át a fiók hitelesítő adatait a metódusnak a partnerműveleteket lekért [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) felület lekért felületére.

Egy adott [](order-resources.md#order)rendelés kiválasztásához használja a partnerműveleteket és a hívási metódust az ügyfél azonosítóval az ügyfél azonosítójának megadásával, majd a rendelés azonosítóját a rendelés megadásához, végül pedig a lekérési [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) **`Orders.ById()`** **`Get`** **`GetAsync`** metódust.

Állítsa a [**`Order.Status`**](order-resources.md#order) tulajdonságot a következőre: `cancelled` , és használja a **`Patch()`** metódust a sorrend frissítéséhez.

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

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus     | Kérés URI-ja                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Javítás** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterrel törölhet egy ügyfelet.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | **guid** | Y        | Az érték egy GUID formátumú **ügyfél-bérlőazonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit. |
| **order-id (rendelésazonosító)** | **sztring** | Y        | Az érték egy sztring, amely a megszakítani szükséges rendelési értékeket jegyzett meg. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha sikeres, ez a metódus a megszakított rendelést adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
