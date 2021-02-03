---
title: Az ügyfél termék-frissítési állapotának beolvasása
description: A ProductUpgradeRequest-erőforrás segítségével meghatározhatja az ügyfél termék-verziófrissítésének állapotát egy új termékcsaládba, például egy Microsoft Azure (MS-AZR-0145P) előfizetésből egy Azure-csomagra.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1819887d459ec72a48ea2b7a5a4121dc56718313
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767915"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="0de76-103">Az ügyfél termék-frissítési állapotának beolvasása</span><span class="sxs-lookup"><span data-stu-id="0de76-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="0de76-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="0de76-104">**Applies to:**</span></span>

- <span data-ttu-id="0de76-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="0de76-105">Partner Center</span></span>

<span data-ttu-id="0de76-106">A [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -erőforrás segítségével lekérheti a verziófrissítés állapotát egy új termékcsaládra.</span><span class="sxs-lookup"><span data-stu-id="0de76-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="0de76-107">Ez az erőforrás akkor érvényes, ha egy Microsoft Azure (MS-AZR-0145P) előfizetésből egy Azure-csomagra frissíti az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="0de76-107">This resource applies when you're upgrading a customer from an Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="0de76-108">Egy sikeres kérelem visszaadja a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="0de76-108">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0de76-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="0de76-109">Prerequisites</span></span>

- <span data-ttu-id="0de76-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="0de76-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0de76-111">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="0de76-111">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="0de76-112">Kövesse a [Secure app modelt](enable-secure-app-model.md) , ha app + felhasználói hitelesítést használ a partner Center API-kkal.</span><span class="sxs-lookup"><span data-stu-id="0de76-112">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="0de76-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0de76-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0de76-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="0de76-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0de76-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="0de76-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0de76-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="0de76-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0de76-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="0de76-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0de76-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0de76-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0de76-119">A termékcsalád.</span><span class="sxs-lookup"><span data-stu-id="0de76-119">The product family.</span></span>

- <span data-ttu-id="0de76-120">Frissítési kérelem verziófrissítése.</span><span class="sxs-lookup"><span data-stu-id="0de76-120">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="0de76-121">C\#</span><span class="sxs-lookup"><span data-stu-id="0de76-121">C\#</span></span>

<span data-ttu-id="0de76-122">Annak ellenőrzését, hogy az ügyfél jogosult-e az Azure-csomagra való frissítésre:</span><span class="sxs-lookup"><span data-stu-id="0de76-122">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="0de76-123">Hozzon létre egy **ProductUpgradesRequest** objektumot, és válassza az ügyfél-azonosítót és az "Azure"-t a termék családjának.</span><span class="sxs-lookup"><span data-stu-id="0de76-123">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="0de76-124">Használja a **IAggregatePartner. ProductUpgrades** gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="0de76-124">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="0de76-125">Hívja meg a **ById** metódust, és adja át a **upgrade-ID-** t.</span><span class="sxs-lookup"><span data-stu-id="0de76-125">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="0de76-126">Hívja meg a **CheckStatus** metódust, és adja meg a **ProductUpgradesRequest** objektumot, amely egy **ProductUpgradeStatus** objektumot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="0de76-126">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="0de76-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="0de76-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0de76-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="0de76-128">Request syntax</span></span>

| <span data-ttu-id="0de76-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="0de76-129">Method</span></span>   | <span data-ttu-id="0de76-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="0de76-130">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0de76-131">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="0de76-131">**POST**</span></span> | <span data-ttu-id="0de76-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-ID}/status http/1.1</span><span class="sxs-lookup"><span data-stu-id="0de76-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0de76-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="0de76-133">URI parameter</span></span>

<span data-ttu-id="0de76-134">A következő lekérdezési paraméterrel adhatja meg azt az ügyfelet, akinek a termék verziófrissítési állapotát keresi.</span><span class="sxs-lookup"><span data-stu-id="0de76-134">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="0de76-135">Név</span><span class="sxs-lookup"><span data-stu-id="0de76-135">Name</span></span>               | <span data-ttu-id="0de76-136">Típus</span><span class="sxs-lookup"><span data-stu-id="0de76-136">Type</span></span> | <span data-ttu-id="0de76-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="0de76-137">Required</span></span> | <span data-ttu-id="0de76-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="0de76-138">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="0de76-139">**frissítési azonosító**</span><span class="sxs-lookup"><span data-stu-id="0de76-139">**upgrade-id**</span></span> | <span data-ttu-id="0de76-140">GUID</span><span class="sxs-lookup"><span data-stu-id="0de76-140">GUID</span></span> | <span data-ttu-id="0de76-141">Igen</span><span class="sxs-lookup"><span data-stu-id="0de76-141">Yes</span></span> | <span data-ttu-id="0de76-142">Az érték egy GUID formátumú frissítési azonosító.</span><span class="sxs-lookup"><span data-stu-id="0de76-142">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="0de76-143">Ennek az azonosítónak a segítségével megadhatja a nyomon követett frissítést.</span><span class="sxs-lookup"><span data-stu-id="0de76-143">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0de76-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="0de76-144">Request headers</span></span>

<span data-ttu-id="0de76-145">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0de76-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0de76-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="0de76-146">Request body</span></span>

<span data-ttu-id="0de76-147">A kérelem törzsének tartalmaznia kell egy [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="0de76-147">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="0de76-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="0de76-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0de76-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="0de76-149">REST response</span></span>

<span data-ttu-id="0de76-150">Ha ez sikeres, ez a metódus egy [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) -erőforrást ad vissza a törzsben.</span><span class="sxs-lookup"><span data-stu-id="0de76-150">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0de76-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="0de76-151">Response success and error codes</span></span>

<span data-ttu-id="0de76-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="0de76-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0de76-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="0de76-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0de76-154">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="0de76-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0de76-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="0de76-155">Response example</span></span>

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
