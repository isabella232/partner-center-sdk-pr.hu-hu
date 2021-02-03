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
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="9b9cf-103">Termék-frissítési entitás létrehozása az ügyfél számára</span><span class="sxs-lookup"><span data-stu-id="9b9cf-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="9b9cf-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="9b9cf-104">**Applies to:**</span></span>

- <span data-ttu-id="9b9cf-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="9b9cf-105">Partner Center</span></span>

<span data-ttu-id="9b9cf-106">Létrehozhat egy termék-frissítési entitást az ügyfél egy adott termékcsaládba (például az Azure-csomagba) való frissítéséhez a **ProductUpgradeRequest** -erőforrás használatával.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-106">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b9cf-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9b9cf-107">Prerequisites</span></span>

- <span data-ttu-id="9b9cf-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9b9cf-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="9b9cf-110">Kövesse a [Secure app modelt](enable-secure-app-model.md) , ha app + felhasználói hitelesítést használ a partner Center API-kkal.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="9b9cf-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9b9cf-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9b9cf-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9b9cf-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9b9cf-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9b9cf-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9b9cf-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9b9cf-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9b9cf-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9b9cf-117">Az a termékcsalád, amelyre frissíteni kívánja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-117">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="9b9cf-118">C\#</span><span class="sxs-lookup"><span data-stu-id="9b9cf-118">C\#</span></span>

<span data-ttu-id="9b9cf-119">Ügyfél frissítése az Azure-csomagra:</span><span class="sxs-lookup"><span data-stu-id="9b9cf-119">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="9b9cf-120">Hozzon létre egy **ProductUpgradesRequest** objektumot, és válassza az ügyfél-azonosítót és az "Azure"-t a termék családjának.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="9b9cf-121">Használja a **IAggregatePartner. ProductUpgrades** gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="9b9cf-122">Hívja meg a **create** metódust, és adja meg a **ProductUpgradesRequest** objektumot, amely egy **Location fejléc** -karakterláncot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-122">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="9b9cf-123">Bontsa ki a **frissítési azonosítót** a Location fejléc sztringből, amely a [frissítési állapot lekérdezésére](get-product-upgrade-status.md)használható.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-123">Extract the **upgrade-id** from the location header string which can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="9b9cf-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="9b9cf-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9b9cf-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="9b9cf-125">Request syntax</span></span>

| <span data-ttu-id="9b9cf-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="9b9cf-126">Method</span></span>   | <span data-ttu-id="9b9cf-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9b9cf-127">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="9b9cf-128">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="9b9cf-128">**POST**</span></span> | <span data-ttu-id="9b9cf-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades http/1.1</span><span class="sxs-lookup"><span data-stu-id="9b9cf-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="9b9cf-130">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9b9cf-130">Request headers</span></span>

<span data-ttu-id="9b9cf-131">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9b9cf-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="9b9cf-132">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9b9cf-132">Request body</span></span>

<span data-ttu-id="9b9cf-133">A kérelem törzsének tartalmaznia kell egy [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-133">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="9b9cf-134">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9b9cf-134">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9b9cf-135">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9b9cf-135">REST response</span></span>

<span data-ttu-id="9b9cf-136">Ha a művelet sikeres, a válasz egy olyan **Location** fejlécet tartalmaz, amely rendelkezik egy olyan URI-val, amely a termék verziófrissítési állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-136">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="9b9cf-137">Mentse ezt az URI-t más kapcsolódó REST API-kkal való használatra.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-137">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9b9cf-138">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9b9cf-138">Response success and error codes</span></span>

<span data-ttu-id="9b9cf-139">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9b9cf-140">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9b9cf-141">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="9b9cf-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9b9cf-142">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9b9cf-142">Response example</span></span>

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
