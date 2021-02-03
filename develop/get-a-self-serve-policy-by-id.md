---
title: Önkiszolgáló szabályzat lekérése azonosító alapján
description: Lekérdezi a megadott önkiszolgálási házirendet az AZONOSÍTÓjának használatával.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ec01d0d9b7c3858cdacf1dbaad3b2b0bb7b6a1a4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767932"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="8c441-103">Önkiszolgáló szabályzat lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="8c441-103">Get a self serve policy by ID</span></span>

<span data-ttu-id="8c441-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="8c441-104">**Applies To**</span></span>

- <span data-ttu-id="8c441-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8c441-105">Partner Center</span></span>

<span data-ttu-id="8c441-106">Lekérdezi a megadott önkiszolgálási házirendet az AZONOSÍTÓjának használatával.</span><span class="sxs-lookup"><span data-stu-id="8c441-106">Gets the specified self serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c441-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8c441-107">Prerequisites</span></span>

- <span data-ttu-id="8c441-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="8c441-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8c441-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="8c441-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="8c441-110">Önkiszolgáló házirend-azonosító.</span><span class="sxs-lookup"><span data-stu-id="8c441-110">A self serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="8c441-111">Példák</span><span class="sxs-lookup"><span data-stu-id="8c441-111">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="8c441-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="8c441-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="8c441-113">**Kérelem szintaxisa**</span><span class="sxs-lookup"><span data-stu-id="8c441-113">**Request syntax**</span></span>

| <span data-ttu-id="8c441-114">Metódus</span><span class="sxs-lookup"><span data-stu-id="8c441-114">Method</span></span>  | <span data-ttu-id="8c441-115">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8c441-115">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="8c441-116">**GET**</span><span class="sxs-lookup"><span data-stu-id="8c441-116">**GET**</span></span> | <span data-ttu-id="8c441-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="8c441-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="8c441-118">**URI-paraméter**</span><span class="sxs-lookup"><span data-stu-id="8c441-118">**URI parameter**</span></span>

<span data-ttu-id="8c441-119">A megadott termék beolvasásához használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="8c441-119">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="8c441-120">Név</span><span class="sxs-lookup"><span data-stu-id="8c441-120">Name</span></span>                       | <span data-ttu-id="8c441-121">Típus</span><span class="sxs-lookup"><span data-stu-id="8c441-121">Type</span></span>         | <span data-ttu-id="8c441-122">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8c441-122">Required</span></span> | <span data-ttu-id="8c441-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c441-123">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="8c441-124">**SelfServePolicy-azonosító**</span><span class="sxs-lookup"><span data-stu-id="8c441-124">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="8c441-125">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="8c441-125">**string**</span></span>   | <span data-ttu-id="8c441-126">Igen</span><span class="sxs-lookup"><span data-stu-id="8c441-126">Yes</span></span>      | <span data-ttu-id="8c441-127">Az önkiszolgáló házirendet azonosító karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="8c441-127">A string that identifies the self serve policy.</span></span>                 |

<span data-ttu-id="8c441-128">**Kérésfejlécek**</span><span class="sxs-lookup"><span data-stu-id="8c441-128">**Request headers**</span></span>

- <span data-ttu-id="8c441-129">További információért lásd a [fejléceket](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="8c441-129">See [Headers](headers.md) for more information.</span></span>

<span data-ttu-id="8c441-130">**Kérelem törzse**</span><span class="sxs-lookup"><span data-stu-id="8c441-130">**Request body**</span></span>

<span data-ttu-id="8c441-131">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="8c441-131">None.</span></span>

<span data-ttu-id="8c441-132">**Példa kérésre**</span><span class="sxs-lookup"><span data-stu-id="8c441-132">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="8c441-133">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8c441-133">REST response</span></span>

<span data-ttu-id="8c441-134">Ha ez sikeres, a válasz törzse [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="8c441-134">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="8c441-135">**Válasz sikeres és hibakódok**</span><span class="sxs-lookup"><span data-stu-id="8c441-135">**Response success and error codes**</span></span>

<span data-ttu-id="8c441-136">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="8c441-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8c441-137">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="8c441-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8c441-138">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8c441-138">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="8c441-139">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="8c441-139">This method returns the following error codes:</span></span>

| <span data-ttu-id="8c441-140">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="8c441-140">HTTP Status Code</span></span>     | <span data-ttu-id="8c441-141">Hibakód</span><span class="sxs-lookup"><span data-stu-id="8c441-141">Error code</span></span>   | <span data-ttu-id="8c441-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="8c441-142">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="8c441-143">404</span><span class="sxs-lookup"><span data-stu-id="8c441-143">404</span></span>                  | <span data-ttu-id="8c441-144">600039</span><span class="sxs-lookup"><span data-stu-id="8c441-144">600039</span></span>       | <span data-ttu-id="8c441-145">Az önkiszolgáló házirend nem található.</span><span class="sxs-lookup"><span data-stu-id="8c441-145">Self serve policy not found.</span></span>                                                     |

<span data-ttu-id="8c441-146">**Példa válaszra**</span><span class="sxs-lookup"><span data-stu-id="8c441-146">**Response example**</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```