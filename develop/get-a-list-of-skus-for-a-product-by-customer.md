---
title: A termékhez tartozó SKU-EK listájának lekérése (az ügyfél által)
description: Az ügyfél által megadott termékhez tartozó SKU-gyűjtemény beolvasása.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6b9c9bcd52798006d7f686405f059192a722c7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767939"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="2e28a-103">A termékhez tartozó SKU-EK listájának lekérése (az ügyfél által)</span><span class="sxs-lookup"><span data-stu-id="2e28a-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="2e28a-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="2e28a-104">**Applies To**</span></span>

- <span data-ttu-id="2e28a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="2e28a-105">Partner Center</span></span>
- <span data-ttu-id="2e28a-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="2e28a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2e28a-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2e28a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2e28a-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2e28a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2e28a-109">Egy meglévő ügyfél számára elérhető, egy adott termékhez tartozó SKU-gyűjtemény beolvasása.</span><span class="sxs-lookup"><span data-stu-id="2e28a-109">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e28a-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2e28a-110">Prerequisites</span></span>

- <span data-ttu-id="2e28a-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="2e28a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e28a-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="2e28a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2e28a-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e28a-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2e28a-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2e28a-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2e28a-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="2e28a-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2e28a-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="2e28a-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2e28a-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="2e28a-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2e28a-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e28a-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2e28a-119">A termék azonosítója (**termékazonosító**).</span><span class="sxs-lookup"><span data-stu-id="2e28a-119">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="2e28a-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="2e28a-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e28a-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2e28a-121">Request syntax</span></span>

| <span data-ttu-id="2e28a-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="2e28a-122">Method</span></span> | <span data-ttu-id="2e28a-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2e28a-123">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e28a-124">POST</span><span class="sxs-lookup"><span data-stu-id="2e28a-124">POST</span></span>   | <span data-ttu-id="2e28a-125">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products/{Product-ID}/SKUs http/1.1</span><span class="sxs-lookup"><span data-stu-id="2e28a-125">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="2e28a-126">Kérelem URI-paramétere</span><span class="sxs-lookup"><span data-stu-id="2e28a-126">Request URI parameter</span></span>

| <span data-ttu-id="2e28a-127">Név</span><span class="sxs-lookup"><span data-stu-id="2e28a-127">Name</span></span>               | <span data-ttu-id="2e28a-128">Típus</span><span class="sxs-lookup"><span data-stu-id="2e28a-128">Type</span></span> | <span data-ttu-id="2e28a-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2e28a-129">Required</span></span> | <span data-ttu-id="2e28a-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="2e28a-130">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e28a-131">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="2e28a-131">customer-tenant-id</span></span> | <span data-ttu-id="2e28a-132">GUID</span><span class="sxs-lookup"><span data-stu-id="2e28a-132">GUID</span></span> | <span data-ttu-id="2e28a-133">Igen</span><span class="sxs-lookup"><span data-stu-id="2e28a-133">Yes</span></span> | <span data-ttu-id="2e28a-134">Az érték egy GUID-formátumú **ügyfél-bérlői azonosító**, amely egy ügyfél megadását lehetővé tevő azonosító.</span><span class="sxs-lookup"><span data-stu-id="2e28a-134">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="2e28a-135">termék azonosítója</span><span class="sxs-lookup"><span data-stu-id="2e28a-135">product-id</span></span> | <span data-ttu-id="2e28a-136">sztring</span><span class="sxs-lookup"><span data-stu-id="2e28a-136">string</span></span> | <span data-ttu-id="2e28a-137">Igen</span><span class="sxs-lookup"><span data-stu-id="2e28a-137">Yes</span></span> | <span data-ttu-id="2e28a-138">A terméket azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="2e28a-138">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="2e28a-139">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="2e28a-139">Request header</span></span>

<span data-ttu-id="2e28a-140">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2e28a-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2e28a-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2e28a-141">Request body</span></span>

<span data-ttu-id="2e28a-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="2e28a-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2e28a-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2e28a-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="2e28a-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2e28a-144">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e28a-145">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2e28a-145">Response success and error codes</span></span>

<span data-ttu-id="2e28a-146">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="2e28a-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2e28a-147">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="2e28a-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e28a-148">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2e28a-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="2e28a-149">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="2e28a-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="2e28a-150">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="2e28a-150">HTTP Status Code</span></span> | <span data-ttu-id="2e28a-151">Hibakód</span><span class="sxs-lookup"><span data-stu-id="2e28a-151">Error code</span></span> | <span data-ttu-id="2e28a-152">Leírás</span><span class="sxs-lookup"><span data-stu-id="2e28a-152">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="2e28a-153">404</span><span class="sxs-lookup"><span data-stu-id="2e28a-153">404</span></span> | <span data-ttu-id="2e28a-154">400013</span><span class="sxs-lookup"><span data-stu-id="2e28a-154">400013</span></span> | <span data-ttu-id="2e28a-155">A fölérendelt termék nem található.</span><span class="sxs-lookup"><span data-stu-id="2e28a-155">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="2e28a-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2e28a-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```
