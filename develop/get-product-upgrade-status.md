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
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="0419d-103">Az ügyfél termékfrissítési állapotának lekért állapota</span><span class="sxs-lookup"><span data-stu-id="0419d-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="0419d-104">A [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) erőforrással egy új termékcsaládra való frissítés állapotát kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="0419d-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="0419d-105">Ez az erőforrás akkor érvényes, ha egy azure-Microsoft Azure (MS-AZR-0145P) előfizetésről frissít egy ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="0419d-105">This resource applies when you're upgrading a customer from a Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="0419d-106">A sikeres kérés a [**ProductUpgradesEligibility erőforrást adja**](product-upgrade-resources.md#productupgradeseligibility) vissza.</span><span class="sxs-lookup"><span data-stu-id="0419d-106">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0419d-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="0419d-107">Prerequisites</span></span>

- <span data-ttu-id="0419d-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0419d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0419d-109">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="0419d-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="0419d-110">Kövesse a [biztonságos alkalmazásmodellt,](enable-secure-app-model.md) ha App+User hitelesítést használ Partnerközpont API-okkal.</span><span class="sxs-lookup"><span data-stu-id="0419d-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="0419d-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0419d-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0419d-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0419d-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0419d-113">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="0419d-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0419d-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="0419d-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0419d-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="0419d-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0419d-116">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0419d-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0419d-117">A termékcsalád.</span><span class="sxs-lookup"><span data-stu-id="0419d-117">The product family.</span></span>

- <span data-ttu-id="0419d-118">A frissítési kérelem frissítési azonosítója.</span><span class="sxs-lookup"><span data-stu-id="0419d-118">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="0419d-119">C\#</span><span class="sxs-lookup"><span data-stu-id="0419d-119">C\#</span></span>

<span data-ttu-id="0419d-120">Annak ellenőrzése, hogy egy ügyfél jogosult-e Azure-csomagra való frissítésre:</span><span class="sxs-lookup"><span data-stu-id="0419d-120">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="0419d-121">Hozzon létre **egy ProductUpgradesRequest** objektumot, és adja meg az ügyfél azonosítóját és az "Azure" értéket a termék családként.</span><span class="sxs-lookup"><span data-stu-id="0419d-121">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="0419d-122">Használja az **IAggregatePartner.ProductUpgrades gyűjteményt.**</span><span class="sxs-lookup"><span data-stu-id="0419d-122">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="0419d-123">Hívja meg **a ById metódust,** és adja meg **az upgrade-id azonosítót.**</span><span class="sxs-lookup"><span data-stu-id="0419d-123">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="0419d-124">Hívja meg a **CheckStatus** metódust, és adja át a **ProductUpgradesRequest** objektumot, amely egy **ProductUpgradeStatus** objektumot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="0419d-124">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="0419d-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="0419d-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0419d-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="0419d-126">Request syntax</span></span>

| <span data-ttu-id="0419d-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="0419d-127">Method</span></span>   | <span data-ttu-id="0419d-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="0419d-128">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0419d-129">**Post**</span><span class="sxs-lookup"><span data-stu-id="0419d-129">**POST**</span></span> | <span data-ttu-id="0419d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0419d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0419d-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="0419d-131">URI parameter</span></span>

<span data-ttu-id="0419d-132">A következő lekérdezési paraméterrel adhatja meg azt az ügyfelet, akinek termékfrissítési állapotot kap.</span><span class="sxs-lookup"><span data-stu-id="0419d-132">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="0419d-133">Név</span><span class="sxs-lookup"><span data-stu-id="0419d-133">Name</span></span>               | <span data-ttu-id="0419d-134">Típus</span><span class="sxs-lookup"><span data-stu-id="0419d-134">Type</span></span> | <span data-ttu-id="0419d-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="0419d-135">Required</span></span> | <span data-ttu-id="0419d-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="0419d-136">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="0419d-137">**frissítési azonosító**</span><span class="sxs-lookup"><span data-stu-id="0419d-137">**upgrade-id**</span></span> | <span data-ttu-id="0419d-138">GUID</span><span class="sxs-lookup"><span data-stu-id="0419d-138">GUID</span></span> | <span data-ttu-id="0419d-139">Igen</span><span class="sxs-lookup"><span data-stu-id="0419d-139">Yes</span></span> | <span data-ttu-id="0419d-140">Az érték egy GUID-formátumú frissítési azonosító.</span><span class="sxs-lookup"><span data-stu-id="0419d-140">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="0419d-141">Ezzel az azonosítóval megadhatja a nyomon követni kívánt frissítést.</span><span class="sxs-lookup"><span data-stu-id="0419d-141">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0419d-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="0419d-142">Request headers</span></span>

<span data-ttu-id="0419d-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0419d-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0419d-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="0419d-144">Request body</span></span>

<span data-ttu-id="0419d-145">A kérelem törzsének tartalmaznia kell egy [**ProductUpgradeRequest erőforrást.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="0419d-145">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="0419d-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="0419d-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0419d-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="0419d-147">REST response</span></span>

<span data-ttu-id="0419d-148">Ha sikeres, ez a metódus egy [**ProductUpgradesEligibility erőforrást**](product-upgrade-resources.md#productupgradeseligibility) ad vissza a törzsben.</span><span class="sxs-lookup"><span data-stu-id="0419d-148">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0419d-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="0419d-149">Response success and error codes</span></span>

<span data-ttu-id="0419d-150">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="0419d-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0419d-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="0419d-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0419d-152">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0419d-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0419d-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="0419d-153">Response example</span></span>

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
