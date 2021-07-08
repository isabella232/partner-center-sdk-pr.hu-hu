---
title: Az MFA bevezetésének állapotának lekérte
description: Lekért egy listát az egyes partnerek többtényezős hitelesítés bevezetésének állapotáról a partneri REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9b8848c2a4531dd6609f86aae6876cec436eeea9
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760521"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="444ed-103">Az MFA bevezetésének állapotának lekérte</span><span class="sxs-lookup"><span data-stu-id="444ed-103">Get MFA adoption status</span></span>

<span data-ttu-id="444ed-104">**A következőre vonatkozik:** Partnerközpont API</span><span class="sxs-lookup"><span data-stu-id="444ed-104">**Applies to**: Partner Center API</span></span>

<span data-ttu-id="444ed-105">Ez a cikk a többtényezős hitelesítés (MFA) bérlőn belüli egyes partnerekre vonatkozó bevezetésének állapotát ismerteti.</span><span class="sxs-lookup"><span data-stu-id="444ed-105">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="444ed-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="444ed-106">Prerequisites</span></span>

- <span data-ttu-id="444ed-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="444ed-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="444ed-108">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="444ed-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="444ed-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="444ed-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="444ed-110">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="444ed-110">Request syntax</span></span>

| <span data-ttu-id="444ed-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="444ed-111">Method</span></span>  | <span data-ttu-id="444ed-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="444ed-112">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="444ed-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="444ed-113">**GET**</span></span> | <span data-ttu-id="444ed-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span><span class="sxs-lookup"><span data-stu-id="444ed-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="444ed-115">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="444ed-115">Request headers</span></span>

- <span data-ttu-id="444ed-116">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="444ed-116">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="444ed-117">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="444ed-117">Request body</span></span>

<span data-ttu-id="444ed-118">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="444ed-118">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="444ed-119">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="444ed-119">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="444ed-120">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="444ed-120">REST response</span></span>

<span data-ttu-id="444ed-121">Ha ez a metódus sikeres, a válasz törzsében az alkalmazás-erőforrások által összegezve visszaadott [API-kérések](mfa-resources.md#api-request-summarized-by-application) gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="444ed-121">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="444ed-122">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="444ed-122">Response success and error codes</span></span>

<span data-ttu-id="444ed-123">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="444ed-123">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="444ed-124">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="444ed-124">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="444ed-125">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="444ed-125">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="444ed-126">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="444ed-126">Response example</span></span>

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
