---
title: MFA nélküli portálkérelmek lekérése
description: A többtényezős hitelesítés (MFA) nélküli felhasználói kérelmek listájának lekérése a partneri REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 41627751d3402d7712d96c15c4281a25ed9a44a7
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445578"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="e5e4b-103">MFA nélküli portálkérelmek lekérése</span><span class="sxs-lookup"><span data-stu-id="e5e4b-103">Get portal requests without MFA</span></span>

<span data-ttu-id="e5e4b-104">Ez a cikk bemutatja, hogyan kérheti le a legutóbbi kérések listáját azokról a felhasználókról, akik a Partnerközpont többtényezős hitelesítés (MFA) elvégzése nélkül férnek hozzá a portálhoz.</span><span class="sxs-lookup"><span data-stu-id="e5e4b-104">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5e4b-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e5e4b-105">Prerequisites</span></span>

- <span data-ttu-id="e5e4b-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e5e4b-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e5e4b-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="e5e4b-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e5e4b-108">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="e5e4b-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e5e4b-109">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="e5e4b-109">Request syntax</span></span>

| <span data-ttu-id="e5e4b-110">Metódus</span><span class="sxs-lookup"><span data-stu-id="e5e4b-110">Method</span></span>  | <span data-ttu-id="e5e4b-111">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e5e4b-111">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="e5e4b-112">**Kap**</span><span class="sxs-lookup"><span data-stu-id="e5e4b-112">**GET**</span></span> | <span data-ttu-id="e5e4b-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="e5e4b-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e5e4b-114">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e5e4b-114">Request headers</span></span>

- <span data-ttu-id="e5e4b-115">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e5e4b-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e5e4b-116">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e5e4b-116">Request body</span></span>

<span data-ttu-id="e5e4b-117">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="e5e4b-117">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e5e4b-118">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e5e4b-118">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="e5e4b-119">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e5e4b-119">REST response</span></span>

<span data-ttu-id="e5e4b-120">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza a [Portal-kérések](mfa-resources.md#portal-request-without-mfa) erőforrásainak gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="e5e4b-120">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e5e4b-121">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e5e4b-121">Response success and error codes</span></span>

<span data-ttu-id="e5e4b-122">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="e5e4b-122">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e5e4b-123">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="e5e4b-123">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e5e4b-124">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e5e4b-124">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e5e4b-125">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e5e4b-125">Response example</span></span>

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
