---
title: Termék termék termékterméklistáinak lekért listája (ügyfél szerint)
description: Lekért egy gyűjteményt az adott termék termékhez ügyfél szerint.
ms.assetid: ''
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b76526d97ba9027897fc88954ba45186d58aefb8
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874159"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a><span data-ttu-id="b90de-103">Termék termék termékterméklistáinak lekért listája (ügyfél szerint)</span><span class="sxs-lookup"><span data-stu-id="b90de-103">Get a list of SKUs for a product (by customer)</span></span>

<span data-ttu-id="b90de-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b90de-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b90de-105">Lekérte egy adott terméktermék-gyűjteményét, amely elérhető egy meglévő ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="b90de-105">Gets a collection of SKUs for a particular product that is available to an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b90de-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b90de-106">Prerequisites</span></span>

- <span data-ttu-id="b90de-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b90de-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b90de-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="b90de-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b90de-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b90de-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b90de-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b90de-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b90de-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b90de-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b90de-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b90de-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b90de-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="b90de-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b90de-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b90de-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b90de-115">Egy termékazonosító **(termékazonosító).**</span><span class="sxs-lookup"><span data-stu-id="b90de-115">A product ID (**product-id**).</span></span>

## <a name="rest-request"></a><span data-ttu-id="b90de-116">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="b90de-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b90de-117">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="b90de-117">Request syntax</span></span>

| <span data-ttu-id="b90de-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="b90de-118">Method</span></span> | <span data-ttu-id="b90de-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b90de-119">Request URI</span></span>                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b90de-120">POST</span><span class="sxs-lookup"><span data-stu-id="b90de-120">POST</span></span>   | <span data-ttu-id="b90de-121">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{termékazonosító}/skus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b90de-121">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{product-id}/skus HTTP/1.1</span></span> |

### <a name="request-uri-parameter"></a><span data-ttu-id="b90de-122">Kérés URI paramétere</span><span class="sxs-lookup"><span data-stu-id="b90de-122">Request URI parameter</span></span>

| <span data-ttu-id="b90de-123">Név</span><span class="sxs-lookup"><span data-stu-id="b90de-123">Name</span></span>               | <span data-ttu-id="b90de-124">Típus</span><span class="sxs-lookup"><span data-stu-id="b90de-124">Type</span></span> | <span data-ttu-id="b90de-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b90de-125">Required</span></span> | <span data-ttu-id="b90de-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="b90de-126">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="b90de-127">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="b90de-127">customer-tenant-id</span></span> | <span data-ttu-id="b90de-128">GUID</span><span class="sxs-lookup"><span data-stu-id="b90de-128">GUID</span></span> | <span data-ttu-id="b90de-129">Igen</span><span class="sxs-lookup"><span data-stu-id="b90de-129">Yes</span></span> | <span data-ttu-id="b90de-130">Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="b90de-130">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="b90de-131">termékazonosító</span><span class="sxs-lookup"><span data-stu-id="b90de-131">product-id</span></span> | <span data-ttu-id="b90de-132">sztring</span><span class="sxs-lookup"><span data-stu-id="b90de-132">string</span></span> | <span data-ttu-id="b90de-133">Igen</span><span class="sxs-lookup"><span data-stu-id="b90de-133">Yes</span></span> | <span data-ttu-id="b90de-134">A terméket azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="b90de-134">A string that identifies the product.</span></span> |

### <a name="request-header"></a><span data-ttu-id="b90de-135">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="b90de-135">Request header</span></span>

<span data-ttu-id="b90de-136">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b90de-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b90de-137">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b90de-137">Request body</span></span>

<span data-ttu-id="b90de-138">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b90de-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b90de-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b90de-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="b90de-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b90de-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b90de-141">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b90de-141">Response success and error codes</span></span>

<span data-ttu-id="b90de-142">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="b90de-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b90de-143">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="b90de-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b90de-144">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b90de-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="b90de-145">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="b90de-145">This method returns the following error codes:</span></span>

| <span data-ttu-id="b90de-146">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="b90de-146">HTTP Status Code</span></span> | <span data-ttu-id="b90de-147">Hibakód</span><span class="sxs-lookup"><span data-stu-id="b90de-147">Error code</span></span> | <span data-ttu-id="b90de-148">Leírás</span><span class="sxs-lookup"><span data-stu-id="b90de-148">Description</span></span> |
|------------------|------------|-------------|
| <span data-ttu-id="b90de-149">404</span><span class="sxs-lookup"><span data-stu-id="b90de-149">404</span></span> | <span data-ttu-id="b90de-150">400013</span><span class="sxs-lookup"><span data-stu-id="b90de-150">400013</span></span> | <span data-ttu-id="b90de-151">A szülőtermék nem található.</span><span class="sxs-lookup"><span data-stu-id="b90de-151">The parent product was not found.</span></span> |

### <a name="response-example"></a><span data-ttu-id="b90de-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b90de-152">Response example</span></span>

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
