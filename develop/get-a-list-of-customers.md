---
title: Az ügyfelek listájának lekérése
description: A partner összes ügyfelet képviselő erőforrások gyűjteményének lekért gyűjtése.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 840c9d1a61451763d37a19639f99b12f1deb7521
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874346"
---
# <a name="get-a-list-of-customers"></a>Az ügyfelek listájának lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk bemutatja, hogyan gyűjti össze a partner összes ügyfelet képviselő erőforrásokat.

> [!TIP]
> Ezt a műveletet az irányítópulton Partnerközpont is végrehajthatja. A főoldal **Ügyfélkezelés területén** válassza az **Ügyfelek megtekintése lehetőséget.** Vagy az oldalsávon válassza az Ügyfelek **lehetőséget.**

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Az összes ügyfél listájának lekért listája:

1. Az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjtemény használatával hozzon létre **egy IPartner** objektumot.

2. Az ügyféllista lekérdezése a [**Query() vagy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) [**a QueryAsync() metódusokkal.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) (A lekérdezések létrehozásával vonatkozó utasításokért lásd a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztályt.)

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Osztály: **CustomerPaging.cs**

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Az összes ügyfél listájának lekért listája:

1. Az [**IAggregatePartner.getCustomers**] függvény használatával lekért hivatkozás az ügyfélműveletekkel kapcsolatban.

2. Az ügyféllista lekérése a **query() függvény** használatával.

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Hajtsa végre [**a Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) parancsot paraméterek nélkül az ügyfelek teljes listájának leállításához.

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterrel lekérdezheti az ügyfelek listáját.

| Név     | Típus    | Kötelező | Leírás                                        |
|----------|---------|----------|----------------------------------------------------|
| **Méret** | **int** | Y        | Az egyszerre megjelenítendő eredmények száma. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus ügyfélerőforrások [gyűjteményét](customer-resources.md#customer) adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
