---
title: Ajánlatkategóriák listájának lekérése piac alapján
description: Megtudhatja, hogyan szerez be egy olyan gyűjteményt, amely az összes ajánlatkategóriát tartalmazza egy adott országban/régióban és területi adatokat az összes Microsoft-felhőhöz.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e699355f07dda3941eafed32f5f635d94000abd1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874278"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="ffa09-103">Ajánlatkategóriák listájának lekérése piac alapján</span><span class="sxs-lookup"><span data-stu-id="ffa09-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="ffa09-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ffa09-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ffa09-105">Ez a cikk azt ismerteti, hogyan lehet egy adott ország/régió és területi terület összes ajánlatkategóriáját tartalmazó gyűjteményt lekért.</span><span class="sxs-lookup"><span data-stu-id="ffa09-105">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffa09-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ffa09-106">Prerequisites</span></span>

- <span data-ttu-id="ffa09-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ffa09-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ffa09-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="ffa09-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="ffa09-109">C\#</span><span class="sxs-lookup"><span data-stu-id="ffa09-109">C\#</span></span>

<span data-ttu-id="ffa09-110">Egy adott ország/régió és területi terület ajánlatkategóriái listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="ffa09-110">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="ffa09-111">Az [**IAggregatePartner.Operations gyűjtemény**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) használatával hívja meg az [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) metódust egy adott környezetben.</span><span class="sxs-lookup"><span data-stu-id="ffa09-111">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="ffa09-112">Vizsgálja meg az eredményül kapott objektum [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="ffa09-112">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="ffa09-113">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="ffa09-113">For an example, see the following:</span></span>

- <span data-ttu-id="ffa09-114">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ffa09-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ffa09-115">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="ffa09-115">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="ffa09-116">Osztály: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="ffa09-116">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="ffa09-117">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ffa09-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ffa09-118">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ffa09-118">Request syntax</span></span>

| <span data-ttu-id="ffa09-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="ffa09-119">Method</span></span>  | <span data-ttu-id="ffa09-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ffa09-120">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="ffa09-121">**Kap**</span><span class="sxs-lookup"><span data-stu-id="ffa09-121">**GET**</span></span> | <span data-ttu-id="ffa09-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ffa09-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="ffa09-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="ffa09-123">URI parameter</span></span>

<span data-ttu-id="ffa09-124">Ez a táblázat felsorolja az ajánlatkategóriák lekérdezhető lekérdezési paramétereit.</span><span class="sxs-lookup"><span data-stu-id="ffa09-124">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="ffa09-125">Név</span><span class="sxs-lookup"><span data-stu-id="ffa09-125">Name</span></span>           | <span data-ttu-id="ffa09-126">Típus</span><span class="sxs-lookup"><span data-stu-id="ffa09-126">Type</span></span>       | <span data-ttu-id="ffa09-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="ffa09-127">Required</span></span> | <span data-ttu-id="ffa09-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="ffa09-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="ffa09-129">**country-id (országazonosító)**</span><span class="sxs-lookup"><span data-stu-id="ffa09-129">**country-id**</span></span> | <span data-ttu-id="ffa09-130">**sztring**</span><span class="sxs-lookup"><span data-stu-id="ffa09-130">**string**</span></span> | <span data-ttu-id="ffa09-131">Y</span><span class="sxs-lookup"><span data-stu-id="ffa09-131">Y</span></span>        | <span data-ttu-id="ffa09-132">Az ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="ffa09-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ffa09-133">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ffa09-133">Request headers</span></span>

<span data-ttu-id="ffa09-134">Szükség **van egy sztringként** formázott területi azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="ffa09-134">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="ffa09-135">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ffa09-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ffa09-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ffa09-136">Request body</span></span>

<span data-ttu-id="ffa09-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ffa09-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ffa09-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ffa09-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="ffa09-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ffa09-139">REST response</span></span>

<span data-ttu-id="ffa09-140">Ha a művelet sikeres, ez a metódus **OfferCategory-erőforrások** gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="ffa09-140">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ffa09-141">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ffa09-141">Response success and error codes</span></span>

<span data-ttu-id="ffa09-142">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ffa09-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ffa09-143">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ffa09-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ffa09-144">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ffa09-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ffa09-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ffa09-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
