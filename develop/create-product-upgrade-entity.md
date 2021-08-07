---
title: Termékfrissítési entitás létrehozása egy ügyfél számára
description: A ProductUpgradeRequest erőforrás használatával termékfrissítési entitást hozhat létre az ügyfelek egy adott termékcsaládra való frissítésére.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7515bbce2914142e052349a1bbb4de20416d0931ac886fe9264cc4d3b8c1f734
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991463"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>Termékfrissítési entitás létrehozása egy ügyfél számára

A **ProductUpgradeRequest** erőforrás használatával létrehozhat egy termékfrissítési entitást az ügyfelek egy adott termékcsaládra (például Azure-csomagra) való frissítésére.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést. Kövesse a [biztonságos alkalmazásmodellt,](enable-secure-app-model.md) ha App+User hitelesítést használ Partnerközpont API-okkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Az a termékcsalád, amelyre frissíteni szeretné az ügyfelet.

## <a name="c"></a>C\#

Ügyfél frissítése Azure-csomagra:

1. Hozzon létre **egy ProductUpgradesRequest** objektumot, és adja meg az ügyfél-azonosítót és az "Azure" értéket a termékcsaládként.

2. Használja az **IAggregatePartner.ProductUpgrades gyűjteményt.**

3. Hívja meg **a Create** metódust, és adja át a **ProductUpgradesRequest objektumot,** amely egy helyfejléc-sztringet **ad** vissza.

4. **Bontsa ki a frissítési azonosítót** a helyfejléc sztringje alapján, amely a frissítési állapot [lekérdezéséhez használható.](get-product-upgrade-status.md)

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1 |

#### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

#### <a name="request-body"></a>A kérés törzse

A kérelem törzsének tartalmaznia kell egy [ProductUpgradeRequest erőforrást.](product-upgrade-resources.md#productupgraderequest)

#### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a>REST-válasz

Ha a válasz sikeres, a válasz tartalmaz egy **Hely** fejlécet, amely a termékfrissítés állapotának lekéréséhez használható URI-t tartalmaz. Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
