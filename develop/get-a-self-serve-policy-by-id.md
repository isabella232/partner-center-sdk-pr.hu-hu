---
title: Önkiszolgáló szabályzat lekért azonosítója
description: Lekérte a megadott önkiszolgáló szabályzatot az azonosítójával.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 074d7ba65c7aab91687a67f50e871cee913fc2bb
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873836"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="9a769-103">Önkiszolgáló szabályzat lekért azonosítója</span><span class="sxs-lookup"><span data-stu-id="9a769-103">Get a self-serve policy by ID</span></span>

<span data-ttu-id="9a769-104">Lekérte a megadott önkiszolgáló szabályzatot az azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="9a769-104">Gets the specified self-serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a769-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9a769-105">Prerequisites</span></span>

- <span data-ttu-id="9a769-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9a769-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9a769-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="9a769-107">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="9a769-108">Egy önkiszolgáló szabályzatazonosító.</span><span class="sxs-lookup"><span data-stu-id="9a769-108">A self-serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="9a769-109">Példák</span><span class="sxs-lookup"><span data-stu-id="9a769-109">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="9a769-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST-kérés</span><span class="sxs-lookup"><span data-stu-id="9a769-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="9a769-111">**Kérés szintaxisa**</span><span class="sxs-lookup"><span data-stu-id="9a769-111">**Request syntax**</span></span>

| <span data-ttu-id="9a769-112">Metódus</span><span class="sxs-lookup"><span data-stu-id="9a769-112">Method</span></span>  | <span data-ttu-id="9a769-113">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9a769-113">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="9a769-114">**Kap**</span><span class="sxs-lookup"><span data-stu-id="9a769-114">**GET**</span></span> | <span data-ttu-id="9a769-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9a769-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="9a769-116">**URI-paraméter**</span><span class="sxs-lookup"><span data-stu-id="9a769-116">**URI parameter**</span></span>

<span data-ttu-id="9a769-117">A megadott termék lekért értékével az alábbi elérésiút-paramétereket használhatja.</span><span class="sxs-lookup"><span data-stu-id="9a769-117">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="9a769-118">Név</span><span class="sxs-lookup"><span data-stu-id="9a769-118">Name</span></span>                       | <span data-ttu-id="9a769-119">Típus</span><span class="sxs-lookup"><span data-stu-id="9a769-119">Type</span></span>         | <span data-ttu-id="9a769-120">Kötelező</span><span class="sxs-lookup"><span data-stu-id="9a769-120">Required</span></span> | <span data-ttu-id="9a769-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="9a769-121">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="9a769-122">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="9a769-122">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="9a769-123">**sztring**</span><span class="sxs-lookup"><span data-stu-id="9a769-123">**string**</span></span>   | <span data-ttu-id="9a769-124">Igen</span><span class="sxs-lookup"><span data-stu-id="9a769-124">Yes</span></span>      | <span data-ttu-id="9a769-125">Az önkiszolgáló szabályzatot azonosító sztring.</span><span class="sxs-lookup"><span data-stu-id="9a769-125">A string that identifies the self-serve policy.</span></span>                 |

<span data-ttu-id="9a769-126">**Kérelemfejlécek**</span><span class="sxs-lookup"><span data-stu-id="9a769-126">**Request headers**</span></span>

- <span data-ttu-id="9a769-127">További információ: [Fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9a769-127">For more information, see [Headers](headers.md).</span></span>

<span data-ttu-id="9a769-128">**Kérelem törzse**</span><span class="sxs-lookup"><span data-stu-id="9a769-128">**Request body**</span></span>

<span data-ttu-id="9a769-129">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="9a769-129">None.</span></span>

<span data-ttu-id="9a769-130">**Példa kérésre**</span><span class="sxs-lookup"><span data-stu-id="9a769-130">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="9a769-131">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9a769-131">REST response</span></span>

<span data-ttu-id="9a769-132">Ha ez sikeres, a válasz törzse tartalmaz egy [SelfServePolicy erőforrást.](self-serve-policy-resources.md#selfservepolicy)</span><span class="sxs-lookup"><span data-stu-id="9a769-132">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="9a769-133">**Sikeres válasz és hibakódok**</span><span class="sxs-lookup"><span data-stu-id="9a769-133">**Response success and error codes**</span></span>

<span data-ttu-id="9a769-134">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="9a769-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9a769-135">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="9a769-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9a769-136">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9a769-136">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="9a769-137">Ez a metódus a következő hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="9a769-137">This method returns the following error codes:</span></span>

| <span data-ttu-id="9a769-138">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="9a769-138">HTTP Status Code</span></span>     | <span data-ttu-id="9a769-139">Hibakód</span><span class="sxs-lookup"><span data-stu-id="9a769-139">Error code</span></span>   | <span data-ttu-id="9a769-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="9a769-140">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="9a769-141">404</span><span class="sxs-lookup"><span data-stu-id="9a769-141">404</span></span>                  | <span data-ttu-id="9a769-142">600039</span><span class="sxs-lookup"><span data-stu-id="9a769-142">600039</span></span>       | <span data-ttu-id="9a769-143">Az önkiszolgáló szabályzat nem található.</span><span class="sxs-lookup"><span data-stu-id="9a769-143">Self-serve policy not found.</span></span>                                                     |

<span data-ttu-id="9a769-144">**Példa válaszra**</span><span class="sxs-lookup"><span data-stu-id="9a769-144">**Response example**</span></span>

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