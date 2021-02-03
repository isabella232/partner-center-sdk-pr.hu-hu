---
title: Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ügyfél alapján)
description: Az ügyfél, a termék és az SKU-azonosítók használatával a megadott termékre és SKU-ra vonatkozó elérhetőségek gyűjteménye beszerezhető.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 5f4067916fea911963182954eed77f4e230e79d6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767959"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="39230-103">Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ügyfél alapján)</span><span class="sxs-lookup"><span data-stu-id="39230-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="39230-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="39230-104">**Applies to:**</span></span>

- <span data-ttu-id="39230-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="39230-105">Partner Center</span></span>
- <span data-ttu-id="39230-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="39230-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="39230-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="39230-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="39230-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="39230-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="39230-109">A következő módszerekkel kérheti le a rendelkezésre állási gyűjteményt egy adott termékhez és SKU-hoz egy adott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="39230-109">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39230-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="39230-110">Prerequisites</span></span>

- <span data-ttu-id="39230-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="39230-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="39230-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="39230-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="39230-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="39230-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="39230-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="39230-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="39230-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="39230-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="39230-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="39230-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="39230-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="39230-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="39230-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="39230-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="39230-119">A termék azonosítója (**termékazonosító**).</span><span class="sxs-lookup"><span data-stu-id="39230-119">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="39230-120">SKU-azonosító (**SKU-azonosító**).</span><span class="sxs-lookup"><span data-stu-id="39230-120">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="39230-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="39230-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="39230-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="39230-122">Request syntax</span></span>

| <span data-ttu-id="39230-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="39230-123">Method</span></span> | <span data-ttu-id="39230-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="39230-124">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="39230-125">POST</span><span class="sxs-lookup"><span data-stu-id="39230-125">POST</span></span>   | <span data-ttu-id="39230-126">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products/{Product-ID}/SKUs/{SKU-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="39230-126">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="39230-127">Kérelem URI-paraméterei</span><span class="sxs-lookup"><span data-stu-id="39230-127">Request URI parameters</span></span>

| <span data-ttu-id="39230-128">Név</span><span class="sxs-lookup"><span data-stu-id="39230-128">Name</span></span>               | <span data-ttu-id="39230-129">Típus</span><span class="sxs-lookup"><span data-stu-id="39230-129">Type</span></span> | <span data-ttu-id="39230-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="39230-130">Required</span></span> | <span data-ttu-id="39230-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="39230-131">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="39230-132">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="39230-132">customer-tenant-id</span></span> | <span data-ttu-id="39230-133">GUID</span><span class="sxs-lookup"><span data-stu-id="39230-133">GUID</span></span> | <span data-ttu-id="39230-134">Igen</span><span class="sxs-lookup"><span data-stu-id="39230-134">Yes</span></span> | <span data-ttu-id="39230-135">Az érték egy GUID-formátumú **ügyfél-bérlői azonosító**, amely egy ügyfél megadását lehetővé tevő azonosító.</span><span class="sxs-lookup"><span data-stu-id="39230-135">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="39230-136">termék azonosítója</span><span class="sxs-lookup"><span data-stu-id="39230-136">product-id</span></span> | <span data-ttu-id="39230-137">sztring</span><span class="sxs-lookup"><span data-stu-id="39230-137">string</span></span> | <span data-ttu-id="39230-138">Igen</span><span class="sxs-lookup"><span data-stu-id="39230-138">Yes</span></span> | <span data-ttu-id="39230-139">A terméket azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="39230-139">A string that identifies the product.</span></span> |
| <span data-ttu-id="39230-140">SKU-azonosító</span><span class="sxs-lookup"><span data-stu-id="39230-140">sku-id</span></span> | <span data-ttu-id="39230-141">sztring</span><span class="sxs-lookup"><span data-stu-id="39230-141">string</span></span> | <span data-ttu-id="39230-142">Igen</span><span class="sxs-lookup"><span data-stu-id="39230-142">Yes</span></span> | <span data-ttu-id="39230-143">Egy karakterlánc, amely azonosítja az SKU-t.</span><span class="sxs-lookup"><span data-stu-id="39230-143">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="39230-144">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="39230-144">Request header</span></span>

<span data-ttu-id="39230-145">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="39230-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="39230-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="39230-146">Request body</span></span>

<span data-ttu-id="39230-147">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="39230-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="39230-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="39230-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="39230-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="39230-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="39230-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="39230-150">Response success and error codes</span></span>

<span data-ttu-id="39230-151">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="39230-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="39230-152">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="39230-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="39230-153">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="39230-153">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="39230-154">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="39230-154">This method returns the following error codes:</span></span>

| <span data-ttu-id="39230-155">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="39230-155">HTTP Status Code</span></span> | <span data-ttu-id="39230-156">Hibakód</span><span class="sxs-lookup"><span data-stu-id="39230-156">Error code</span></span> | <span data-ttu-id="39230-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="39230-157">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="39230-158">404</span><span class="sxs-lookup"><span data-stu-id="39230-158">404</span></span> | <span data-ttu-id="39230-159">400013</span><span class="sxs-lookup"><span data-stu-id="39230-159">400013</span></span> | <span data-ttu-id="39230-160">A fölérendelt termék nem található.</span><span class="sxs-lookup"><span data-stu-id="39230-160">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="39230-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="39230-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
