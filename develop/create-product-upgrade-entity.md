---
title: Termékfrissítési entitás létrehozása egy ügyfél számára
description: A ProductUpgradeRequest erőforrással termékfrissítési entitást hozhat létre az ügyfelek adott termékcsaládra való frissítésére.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4e346b7f5294a8847047c85115d8c80f34eaca84
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973409"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="1b7ba-103">Termékfrissítési entitás létrehozása egy ügyfél számára</span><span class="sxs-lookup"><span data-stu-id="1b7ba-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="1b7ba-104">A **ProductUpgradeRequest** erőforrás használatával létrehozhat egy termékfrissítési entitást, amely frissíti az ügyfelet egy adott termékcsaládra (például Azure-csomagra).</span><span class="sxs-lookup"><span data-stu-id="1b7ba-104">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b7ba-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1b7ba-105">Prerequisites</span></span>

- <span data-ttu-id="1b7ba-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1b7ba-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1b7ba-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="1b7ba-108">Kövesse a [biztonságos alkalmazásmodellt,](enable-secure-app-model.md) ha App+User hitelesítést használ Partnerközpont API-okkal.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="1b7ba-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1b7ba-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1b7ba-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1b7ba-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1b7ba-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1b7ba-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1b7ba-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1b7ba-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1b7ba-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="1b7ba-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1b7ba-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1b7ba-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1b7ba-115">Az a termékcsalád, amelyre frissíteni szeretné az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-115">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="1b7ba-116">C\#</span><span class="sxs-lookup"><span data-stu-id="1b7ba-116">C\#</span></span>

<span data-ttu-id="1b7ba-117">Ügyfél frissítése Azure-csomagra:</span><span class="sxs-lookup"><span data-stu-id="1b7ba-117">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="1b7ba-118">Hozzon létre **egy ProductUpgradesRequest** objektumot, és adja meg az ügyfél azonosítóját és az "Azure" értéket a termék családként.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="1b7ba-119">Használja az **IAggregatePartner.ProductUpgrades gyűjteményt.**</span><span class="sxs-lookup"><span data-stu-id="1b7ba-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="1b7ba-120">Hívja meg a **Create** metódust, és adja át a **ProductUpgradesRequest** objektumot, amely egy helyfejléc **sztringet ad** vissza.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-120">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="1b7ba-121">Bontsa **ki a frissítési azonosítót** a hely fejlécsringből, amely a frissítési [állapot lekérdezéséhez használható.](get-product-upgrade-status.md)</span><span class="sxs-lookup"><span data-stu-id="1b7ba-121">Extract the **upgrade-id** from the location header string that can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="1b7ba-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="1b7ba-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1b7ba-123">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="1b7ba-123">Request syntax</span></span>

| <span data-ttu-id="1b7ba-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="1b7ba-124">Method</span></span>   | <span data-ttu-id="1b7ba-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1b7ba-125">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="1b7ba-126">**Post**</span><span class="sxs-lookup"><span data-stu-id="1b7ba-126">**POST**</span></span> | <span data-ttu-id="1b7ba-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1b7ba-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="1b7ba-128">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="1b7ba-128">Request headers</span></span>

<span data-ttu-id="1b7ba-129">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1b7ba-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="1b7ba-130">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1b7ba-130">Request body</span></span>

<span data-ttu-id="1b7ba-131">A kérelem törzsének tartalmaznia kell egy [ProductUpgradeRequest erőforrást.](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="1b7ba-131">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="1b7ba-132">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1b7ba-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="1b7ba-133">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1b7ba-133">REST response</span></span>

<span data-ttu-id="1b7ba-134">Ha a válasz sikeres, a válasz tartalmaz egy **Hely** fejlécet, amely rendelkezik egy URI-azonosítóval, amely a termékfrissítés állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-134">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="1b7ba-135">Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-135">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1b7ba-136">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1b7ba-136">Response success and error codes</span></span>

<span data-ttu-id="1b7ba-137">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1b7ba-138">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="1b7ba-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1b7ba-139">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1b7ba-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1b7ba-140">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1b7ba-140">Response example</span></span>

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
