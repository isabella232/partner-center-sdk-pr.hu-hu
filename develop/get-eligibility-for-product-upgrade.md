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
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="731f0-103">Ügyfél jogosultságának keresése Azure-csomagra való frissítéshez</span><span class="sxs-lookup"><span data-stu-id="731f0-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="731f0-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="731f0-104">**Applies to:**</span></span>

- <span data-ttu-id="731f0-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="731f0-105">Partner Center</span></span>

<span data-ttu-id="731f0-106">A [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) erőforrás segítségével ellenőrizhető, hogy az ügyfél jogosult-e az Azure-csomagra való frissítésre Microsoft Azure (MS-AZR-0145P) előfizetésből, ez a metódus egy [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -erőforrást ad vissza az ügyfél termék-frissítési jogosultságával.</span><span class="sxs-lookup"><span data-stu-id="731f0-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="731f0-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="731f0-107">Prerequisites</span></span>

- <span data-ttu-id="731f0-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="731f0-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="731f0-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="731f0-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="731f0-110">Kövesse a [Secure app modelt](enable-secure-app-model.md) , ha app + felhasználói hitelesítést használ a partner Center API-kkal.</span><span class="sxs-lookup"><span data-stu-id="731f0-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="731f0-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="731f0-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="731f0-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="731f0-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="731f0-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="731f0-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="731f0-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="731f0-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="731f0-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="731f0-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="731f0-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="731f0-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="731f0-117">A termékcsalád.</span><span class="sxs-lookup"><span data-stu-id="731f0-117">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="731f0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="731f0-118">C\#</span></span>

<span data-ttu-id="731f0-119">Annak ellenőrzését, hogy az ügyfél jogosult-e az Azure-csomagra való frissítésre:</span><span class="sxs-lookup"><span data-stu-id="731f0-119">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="731f0-120">Hozzon létre egy **ProductUpgradesRequest** objektumot, és válassza az ügyfél-azonosítót és az "Azure"-t a termék családjának.</span><span class="sxs-lookup"><span data-stu-id="731f0-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="731f0-121">Használja a **IAggregatePartner. ProductUpgrades** gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="731f0-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="731f0-122">Hívja meg a **CheckEligibility** metódust, és adja meg a **ProductUpgradesRequest** objektumot, amely egy **ProductUpgradesEligibility** objektumot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="731f0-122">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="731f0-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="731f0-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="731f0-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="731f0-124">Request syntax</span></span>

| <span data-ttu-id="731f0-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="731f0-125">Method</span></span>   | <span data-ttu-id="731f0-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="731f0-126">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="731f0-127">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="731f0-127">**POST**</span></span> | <span data-ttu-id="731f0-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility http/1.1</span><span class="sxs-lookup"><span data-stu-id="731f0-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="731f0-129">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="731f0-129">Request headers</span></span>

<span data-ttu-id="731f0-130">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="731f0-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="731f0-131">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="731f0-131">Request body</span></span>

<span data-ttu-id="731f0-132">A kérelem törzsének tartalmaznia kell egy [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="731f0-132">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="731f0-133">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="731f0-133">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="731f0-134">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="731f0-134">REST response</span></span>

<span data-ttu-id="731f0-135">Ha ez sikeres, ez a metódus egy [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -erőforrást ad vissza a törzsben.</span><span class="sxs-lookup"><span data-stu-id="731f0-135">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="731f0-136">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="731f0-136">Response success and error codes</span></span>

<span data-ttu-id="731f0-137">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="731f0-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="731f0-138">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="731f0-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="731f0-139">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="731f0-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="731f0-140">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="731f0-140">Response example</span></span>

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
