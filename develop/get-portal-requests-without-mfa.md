---
title: MFA nélküli portálkérelmek lekérése
description: A többtényezős hitelesítés (MFA) nélküli felhasználói kérelmek listájának beolvasása a partner REST API használatával.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: fd350aa3301f00926942ae6c6af359b0d0edc423
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767924"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="c22f5-103">MFA nélküli portálkérelmek lekérése</span><span class="sxs-lookup"><span data-stu-id="c22f5-103">Get portal requests without MFA</span></span>

<span data-ttu-id="c22f5-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="c22f5-104">Applies to:</span></span>

- <span data-ttu-id="c22f5-105">Partnerközpont API</span><span class="sxs-lookup"><span data-stu-id="c22f5-105">Partner Center API</span></span>

<span data-ttu-id="c22f5-106">Ez a cikk azt ismerteti, hogyan kérhető le a partner Center portált a többtényezős hitelesítés (MFA) befejezése nélkül elérő felhasználók legutóbbi kéréseinek listája.</span><span class="sxs-lookup"><span data-stu-id="c22f5-106">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c22f5-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c22f5-107">Prerequisites</span></span>

- <span data-ttu-id="c22f5-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c22f5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c22f5-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="c22f5-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c22f5-110">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c22f5-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c22f5-111">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c22f5-111">Request syntax</span></span>

| <span data-ttu-id="c22f5-112">Metódus</span><span class="sxs-lookup"><span data-stu-id="c22f5-112">Method</span></span>  | <span data-ttu-id="c22f5-113">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c22f5-113">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="c22f5-114">**GET**</span><span class="sxs-lookup"><span data-stu-id="c22f5-114">**GET**</span></span> | <span data-ttu-id="c22f5-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="c22f5-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c22f5-116">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c22f5-116">Request headers</span></span>

- <span data-ttu-id="c22f5-117">További információért lásd a [partneri központ Rest-fejléceit](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="c22f5-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="c22f5-118">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c22f5-118">Request body</span></span>

<span data-ttu-id="c22f5-119">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c22f5-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c22f5-120">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c22f5-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="c22f5-121">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c22f5-121">REST response</span></span>

<span data-ttu-id="c22f5-122">Ha a művelet sikeres, ez a módszer egy [portál-kérelem](mfa-resources.md#portal-request-without-mfa) erőforrásainak gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="c22f5-122">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c22f5-123">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c22f5-123">Response success and error codes</span></span>

<span data-ttu-id="c22f5-124">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c22f5-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c22f5-125">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c22f5-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c22f5-126">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c22f5-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c22f5-127">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c22f5-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 296
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 23 Apr 2020 22:10:30 GMT
{
    "totalCount": 1,
    "items": [
        {
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "lastNonMfaCompliantRequestDateTime": "2020-04-21T22:09:53.051"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
