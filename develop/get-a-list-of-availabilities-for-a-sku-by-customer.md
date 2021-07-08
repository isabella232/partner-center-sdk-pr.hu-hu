---
title: Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ügyfél alapján)
description: Egy adott termékhez és termékváltozathoz az ügyfél, a termék- és termékváltozat-azonosítók használatával kaphat rendelkezésre állási gyűjteményt az ügyféltől.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b237bbd17a6108bbcb4e23529cf476a6b8306f68
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874550"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a><span data-ttu-id="ccc7a-103">Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ügyfél alapján)</span><span class="sxs-lookup"><span data-stu-id="ccc7a-103">Get a list of availabilities for a SKU (by customer)</span></span>

<span data-ttu-id="ccc7a-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ccc7a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ccc7a-105">A következő módszerekkel kaphat rendelkezésre állási gyűjteményt egy adott termékhez és termékváltozathoz, amelyek egy adott ügyfél számára elérhetők.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-105">You can use the following methods to get a collection of availabilities for a specified product and SKU available to a particular customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccc7a-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ccc7a-106">Prerequisites</span></span>

- <span data-ttu-id="ccc7a-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ccc7a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ccc7a-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ccc7a-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ccc7a-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ccc7a-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ccc7a-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ccc7a-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ccc7a-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ccc7a-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ccc7a-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ccc7a-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="ccc7a-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ccc7a-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ccc7a-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ccc7a-115">Egy termékazonosító (**termékazonosító).**</span><span class="sxs-lookup"><span data-stu-id="ccc7a-115">A product identifier (**product-id**).</span></span>

- <span data-ttu-id="ccc7a-116">Egy termékváltozat-azonosító (**sku-id**).</span><span class="sxs-lookup"><span data-stu-id="ccc7a-116">A SKU identifier (**sku-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="ccc7a-117">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ccc7a-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ccc7a-118">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ccc7a-118">Request syntax</span></span>

| <span data-ttu-id="ccc7a-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="ccc7a-119">Method</span></span> | <span data-ttu-id="ccc7a-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ccc7a-120">Request URI</span></span>                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ccc7a-121">POST</span><span class="sxs-lookup"><span data-stu-id="ccc7a-121">POST</span></span>   | <span data-ttu-id="ccc7a-122">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{termékazonosító}/skus/{sku-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ccc7a-122">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus/{sku-id} HTTP/1.1</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="ccc7a-123">URI-paraméterek kérése</span><span class="sxs-lookup"><span data-stu-id="ccc7a-123">Request URI parameters</span></span>

| <span data-ttu-id="ccc7a-124">Név</span><span class="sxs-lookup"><span data-stu-id="ccc7a-124">Name</span></span>               | <span data-ttu-id="ccc7a-125">Típus</span><span class="sxs-lookup"><span data-stu-id="ccc7a-125">Type</span></span> | <span data-ttu-id="ccc7a-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="ccc7a-126">Required</span></span> | <span data-ttu-id="ccc7a-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="ccc7a-127">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="ccc7a-128">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="ccc7a-128">customer-tenant-id</span></span> | <span data-ttu-id="ccc7a-129">GUID</span><span class="sxs-lookup"><span data-stu-id="ccc7a-129">GUID</span></span> | <span data-ttu-id="ccc7a-130">Igen</span><span class="sxs-lookup"><span data-stu-id="ccc7a-130">Yes</span></span> | <span data-ttu-id="ccc7a-131">Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-131">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="ccc7a-132">termékazonosító</span><span class="sxs-lookup"><span data-stu-id="ccc7a-132">product-id</span></span> | <span data-ttu-id="ccc7a-133">sztring</span><span class="sxs-lookup"><span data-stu-id="ccc7a-133">string</span></span> | <span data-ttu-id="ccc7a-134">Igen</span><span class="sxs-lookup"><span data-stu-id="ccc7a-134">Yes</span></span> | <span data-ttu-id="ccc7a-135">A terméket azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-135">A string that identifies the product.</span></span> |
| <span data-ttu-id="ccc7a-136">sku-id</span><span class="sxs-lookup"><span data-stu-id="ccc7a-136">sku-id</span></span> | <span data-ttu-id="ccc7a-137">sztring</span><span class="sxs-lookup"><span data-stu-id="ccc7a-137">string</span></span> | <span data-ttu-id="ccc7a-138">Igen</span><span class="sxs-lookup"><span data-stu-id="ccc7a-138">Yes</span></span> | <span data-ttu-id="ccc7a-139">A termékváltozatot azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-139">A string that identifies the SKU.</span></span> |

### <a name="request-header"></a><span data-ttu-id="ccc7a-140">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="ccc7a-140">Request header</span></span>

<span data-ttu-id="ccc7a-141">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ccc7a-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ccc7a-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ccc7a-142">Request body</span></span>

<span data-ttu-id="ccc7a-143">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ccc7a-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ccc7a-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="ccc7a-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ccc7a-145">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ccc7a-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ccc7a-146">Response success and error codes</span></span>

<span data-ttu-id="ccc7a-147">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ccc7a-148">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ccc7a-149">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ccc7a-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="ccc7a-150">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="ccc7a-150">This method returns the following error codes:</span></span>

| <span data-ttu-id="ccc7a-151">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="ccc7a-151">HTTP Status Code</span></span> | <span data-ttu-id="ccc7a-152">Hibakód</span><span class="sxs-lookup"><span data-stu-id="ccc7a-152">Error code</span></span> | <span data-ttu-id="ccc7a-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="ccc7a-153">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="ccc7a-154">404</span><span class="sxs-lookup"><span data-stu-id="ccc7a-154">404</span></span> | <span data-ttu-id="ccc7a-155">400013</span><span class="sxs-lookup"><span data-stu-id="ccc7a-155">400013</span></span> | <span data-ttu-id="ccc7a-156">A szülőtermék nem található.</span><span class="sxs-lookup"><span data-stu-id="ccc7a-156">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="ccc7a-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ccc7a-157">Response example</span></span>

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
