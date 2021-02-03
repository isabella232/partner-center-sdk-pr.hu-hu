---
title: Termék-frissítési entitás létrehozása az ügyfél számára
description: A ProductUpgradeRequest-erőforrás használatával létrehozhat egy termék-frissítési entitást, amely egy adott termékcsaládra frissítheti az ügyfelet.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767751"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a>Termék-frissítési entitás létrehozása az ügyfél számára

**A következőkre vonatkozik:**

- Partnerközpont

Létrehozhat egy termék-frissítési entitást az ügyfél egy adott termékcsaládba (például az Azure-csomagba) való frissítéséhez a **ProductUpgradeRequest** -erőforrás használatával.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival. Kövesse a [Secure app modelt](enable-secure-app-model.md) , ha app + felhasználói hitelesítést használ a partner Center API-kkal.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Az a termékcsalád, amelyre frissíteni kívánja az ügyfelet.

## <a name="c"></a>C\#

Ügyfél frissítése az Azure-csomagra:

1. Hozzon létre egy **ProductUpgradesRequest** objektumot, és válassza az ügyfél-azonosítót és az "Azure"-t a termék családjának.

2. Használja a **IAggregatePartner. ProductUpgrades** gyűjteményt.

3. Hívja meg a **create** metódust, és adja meg a **ProductUpgradesRequest** objektumot, amely egy **Location fejléc** -karakterláncot ad vissza.

4. Bontsa ki a **frissítési azonosítót** a Location fejléc sztringből, amely a [frissítési állapot lekérdezésére](get-product-upgrade-status.md)használható.

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

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades http/1.1 |

#### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

#### <a name="request-body"></a>A kérés törzse

A kérelem törzsének tartalmaznia kell egy [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) -erőforrást.

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

Ha a művelet sikeres, a válasz egy olyan **Location** fejlécet tartalmaz, amely rendelkezik egy olyan URI-val, amely a termék verziófrissítési állapotának lekérésére használható. Mentse ezt az URI-t más kapcsolódó REST API-kkal való használatra.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
