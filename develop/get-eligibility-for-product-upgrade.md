---
title: Ügyfél jogosultságának keresése Azure-csomagra való frissítéshez
description: A ProductUpgradeRequest erőforrás segítségével visszaállíthat egy ProductUpgradesEligibility-erőforrást annak megállapításához, hogy az ügyfél jogosult-e a Microsoft Azure (MS-AZR-0145P) előfizetés Azure-csomagra való frissítésére.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767691"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a>Ügyfél jogosultságának keresése Azure-csomagra való frissítéshez

**A következőkre vonatkozik:**

- Partnerközpont

A [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) erőforrás segítségével ellenőrizhető, hogy az ügyfél jogosult-e az Azure-csomagra való frissítésre Microsoft Azure (MS-AZR-0145P) előfizetésből, ez a metódus egy [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -erőforrást ad vissza az ügyfél termék-frissítési jogosultságával.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival. Kövesse a [Secure app modelt](enable-secure-app-model.md) , ha app + felhasználói hitelesítést használ a partner Center API-kkal.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- A termékcsalád.

## <a name="c"></a>C\#

Annak ellenőrzését, hogy az ügyfél jogosult-e az Azure-csomagra való frissítésre:

1. Hozzon létre egy **ProductUpgradesRequest** objektumot, és válassza az ügyfél-azonosítót és az "Azure"-t a termék családjának.

2. Használja a **IAggregatePartner. ProductUpgrades** gyűjteményt.
3. Hívja meg a **CheckEligibility** metódust, és adja meg a **ProductUpgradesRequest** objektumot, amely egy **ProductUpgradesEligibility** objektumot ad vissza.

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility http/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A kérelem törzsének tartalmaznia kell egy [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -erőforrást.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
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
        "productFamily": "azure"
}
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus egy [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -erőforrást ad vissza a törzsben.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
