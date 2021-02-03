---
title: Az MFA bevezetési állapotának beolvasása
description: Szerezze be a multi-Factor Authentication bevezetési állapotának listáját az egyes partnereknél a partner REST API használatával.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: f82d163b704323c81e2948b78eb9b9d1a14ddc52
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767888"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="78016-103">MFA bevezetési állapotának beolvasása</span><span class="sxs-lookup"><span data-stu-id="78016-103">Get MFA adoption status</span></span>

<span data-ttu-id="78016-104">A következőkre vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="78016-104">Applies to:</span></span>

- <span data-ttu-id="78016-105">Partnerközpont API</span><span class="sxs-lookup"><span data-stu-id="78016-105">Partner Center API</span></span>

<span data-ttu-id="78016-106">Ez a cikk azt ismerteti, hogyan kérhető le a többtényezős hitelesítés (MFA) bevezetési állapota a bérlőn belüli egyes partnerek számára.</span><span class="sxs-lookup"><span data-stu-id="78016-106">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78016-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="78016-107">Prerequisites</span></span>

- <span data-ttu-id="78016-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="78016-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="78016-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="78016-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="78016-110">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="78016-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="78016-111">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="78016-111">Request syntax</span></span>

| <span data-ttu-id="78016-112">Metódus</span><span class="sxs-lookup"><span data-stu-id="78016-112">Method</span></span>  | <span data-ttu-id="78016-113">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="78016-113">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="78016-114">**GET**</span><span class="sxs-lookup"><span data-stu-id="78016-114">**GET**</span></span> | <span data-ttu-id="78016-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span><span class="sxs-lookup"><span data-stu-id="78016-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="78016-116">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="78016-116">Request headers</span></span>

- <span data-ttu-id="78016-117">További információért lásd a [partneri központ Rest-fejléceit](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="78016-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="78016-118">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="78016-118">Request body</span></span>

<span data-ttu-id="78016-119">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="78016-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="78016-120">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="78016-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="78016-121">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="78016-121">REST response</span></span>

<span data-ttu-id="78016-122">Ha ez sikeres, ez a metódus egy API-kérelem gyűjteményét adja vissza, amely a válasz törzsében az [alkalmazás erőforrásai alapján van összesítve](mfa-resources.md#api-request-summarized-by-application) .</span><span class="sxs-lookup"><span data-stu-id="78016-122">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="78016-123">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="78016-123">Response success and error codes</span></span>

<span data-ttu-id="78016-124">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="78016-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="78016-125">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="78016-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="78016-126">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="78016-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="78016-127">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="78016-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 313
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
[
    {
        "loginDate": "2020-05-20",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 7,
        "applicationId": "14f38d7d-c4fc-448a-b2df-0fc60e75465a",
        "applicationName": ""
    },
    {
        "loginDate": "2020-05-19",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 14,
        "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
        "applicationName": ""
    }
]
```
