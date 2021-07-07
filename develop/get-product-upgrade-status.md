---
title: Az ügyfél termékfrissítési állapotának lekért állapota
description: A ProductUpgradeRequest erőforrással megállapíthatja egy ügyfél termékfrissítésének állapotát egy új termékcsaládba, például egy Azure-csomagra való Microsoft Azure-előfizetésből (MS-AZR-0145P).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d925dd0fae987226ad1f8e71fad380ba144b83
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445561"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a>Az ügyfél termékfrissítési állapotának lekért állapota

A [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) erőforrással egy új termékcsaládra való frissítés állapotát kaphatja meg. Ez az erőforrás akkor érvényes, ha egy azure-Microsoft Azure (MS-AZR-0145P) előfizetésről frissít egy ügyfelet. A sikeres kérés a [**ProductUpgradesEligibility erőforrást adja**](product-upgrade-resources.md#productupgradeseligibility) vissza.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést. Kövesse a [biztonságos alkalmazásmodellt,](enable-secure-app-model.md) ha App+User hitelesítést használ Partnerközpont API-okkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- A termékcsalád.

- A frissítési kérelem frissítési azonosítója.

## <a name="c"></a>C\#

Annak ellenőrzése, hogy egy ügyfél jogosult-e Azure-csomagra való frissítésre:

1. Hozzon létre **egy ProductUpgradesRequest** objektumot, és adja meg az ügyfél azonosítóját és az "Azure" értéket a termék családként.

2. Használja az **IAggregatePartner.ProductUpgrades gyűjteményt.**

3. Hívja meg **a ById metódust,** és adja meg **az upgrade-id azonosítót.**

4. Hívja meg a **CheckStatus** metódust, és adja át a **ProductUpgradesRequest** objektumot, amely egy **ProductUpgradeStatus** objektumot ad vissza.

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja |
|----------|-----------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel adhatja meg azt az ügyfelet, akinek termékfrissítési állapotot kap.

| Név               | Típus | Kötelező | Leírás                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **frissítési azonosító** | GUID | Igen | Az érték egy GUID-formátumú frissítési azonosító. Ezzel az azonosítóval megadhatja a nyomon követni kívánt frissítést. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

A kérelem törzsének tartalmaznia kell egy [**ProductUpgradeRequest erőforrást.**](product-upgrade-resources.md#productupgraderequest)

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy [**ProductUpgradesEligibility erőforrást**](product-upgrade-resources.md#productupgradeseligibility) ad vissza a törzsben.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
