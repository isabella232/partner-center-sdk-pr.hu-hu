---
title: Az ügyfél Azure-csomagra való frissítésre való jogosultságának ellenőrzése
description: A ProductUpgradeRequest erőforrás használatával productUpgradesEligibility erőforrást kaphat annak meghatározásához, hogy az ügyfél jogosult-e Microsoft Azure-előfizetésről (MS-AZR-0145P) Azure-csomagra frissíteni.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 34a20611c7d92042b5432c5ffb3ba4702d77e0c2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446258"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="abced-103">Az ügyfél Azure-csomagra való frissítésre való jogosultságának ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="abced-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="abced-104">A [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) erőforrás használatával ellenőrizheti, hogy az ügyfél jogosult-e Azure-csomagra frissíteni egy Microsoft Azure-előfizetésből (MS-AZR-0145P) Ez a módszer egy [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) erőforrást ad vissza az ügyfél termékfrissítési jogosultságával.</span><span class="sxs-lookup"><span data-stu-id="abced-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abced-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="abced-105">Prerequisites</span></span>

- <span data-ttu-id="abced-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="abced-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="abced-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="abced-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="abced-108">Kövesse a [biztonságos alkalmazásmodellt,](enable-secure-app-model.md) ha App+User hitelesítést használ Partnerközpont API-okkal.</span><span class="sxs-lookup"><span data-stu-id="abced-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="abced-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="abced-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="abced-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="abced-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="abced-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="abced-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="abced-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="abced-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="abced-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="abced-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="abced-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="abced-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="abced-115">A termékcsalád.</span><span class="sxs-lookup"><span data-stu-id="abced-115">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="abced-116">C\#</span><span class="sxs-lookup"><span data-stu-id="abced-116">C\#</span></span>

<span data-ttu-id="abced-117">Annak ellenőrzése, hogy az ügyfél jogosult-e Azure-csomagra való frissítésre:</span><span class="sxs-lookup"><span data-stu-id="abced-117">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="abced-118">Hozzon létre **egy ProductUpgradesRequest** objektumot, és adja meg az ügyfél azonosítóját és az "Azure" értéket a termékcsaládként.</span><span class="sxs-lookup"><span data-stu-id="abced-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="abced-119">Használja az **IAggregatePartner.ProductUpgrades gyűjteményt.**</span><span class="sxs-lookup"><span data-stu-id="abced-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="abced-120">Hívja meg a **CheckEligibility** metódust, és adja át a **ProductUpgradesRequest** objektumot, amely egy **ProductUpgradesEligibility objektumot ad** vissza.</span><span class="sxs-lookup"><span data-stu-id="abced-120">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="abced-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="abced-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="abced-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="abced-122">Request syntax</span></span>

| <span data-ttu-id="abced-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="abced-123">Method</span></span>   | <span data-ttu-id="abced-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="abced-124">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="abced-125">**Post**</span><span class="sxs-lookup"><span data-stu-id="abced-125">**POST**</span></span> | <span data-ttu-id="abced-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="abced-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="abced-127">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="abced-127">Request headers</span></span>

<span data-ttu-id="abced-128">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="abced-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="abced-129">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="abced-129">Request body</span></span>

<span data-ttu-id="abced-130">A kérelem törzsének tartalmaznia kell egy [**ProductUpgradeRequest erőforrást.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="abced-130">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="abced-131">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="abced-131">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="abced-132">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="abced-132">REST response</span></span>

<span data-ttu-id="abced-133">Ha sikeres, ez a metódus egy [**ProductUpgradesEligibility erőforrást**](product-upgrade-resources.md#productupgradeseligibility) ad vissza a törzsben.</span><span class="sxs-lookup"><span data-stu-id="abced-133">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="abced-134">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="abced-134">Response success and error codes</span></span>

<span data-ttu-id="abced-135">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="abced-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="abced-136">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="abced-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="abced-137">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="abced-137">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="abced-138">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="abced-138">Response example</span></span>

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
