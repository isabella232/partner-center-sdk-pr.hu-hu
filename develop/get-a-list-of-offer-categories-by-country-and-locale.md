---
title: Ajánlatkategóriák listájának lekérése piac alapján
description: Megtudhatja, hogyan szerezhet be egy olyan gyűjteményt, amely az adott országban/régióban található összes ajánlatot tartalmazza, és az összes Microsoft-felhőre vonatkozó területi beállítással rendelkezik.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 05aad095c6cb8eaee4cbf7ce976ca1b4b7a408c4
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500056"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="c296b-103">Ajánlatkategóriák listájának lekérése piac alapján</span><span class="sxs-lookup"><span data-stu-id="c296b-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="c296b-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="c296b-104">**Applies to:**</span></span>

- <span data-ttu-id="c296b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c296b-105">Partner Center</span></span>
- <span data-ttu-id="c296b-106">A 21Vianet által üzemeltetett Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c296b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c296b-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c296b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c296b-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c296b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c296b-109">Ez a cikk azt ismerteti, hogyan szerezhet be egy olyan gyűjteményt, amely az adott országban/régióban és területi beállításban szereplő összes ajánlati kategóriát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="c296b-109">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c296b-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c296b-110">Prerequisites</span></span>

- <span data-ttu-id="c296b-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c296b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c296b-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="c296b-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="c296b-113">C\#</span><span class="sxs-lookup"><span data-stu-id="c296b-113">C\#</span></span>

<span data-ttu-id="c296b-114">Az ajánlati kategóriák listájának lekérése egy adott országban/régióban és területi beállításban:</span><span class="sxs-lookup"><span data-stu-id="c296b-114">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="c296b-115">A [**IAggregatePartner. Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) gyűjtemény használatával hívja meg a [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) metódust egy adott környezetben.</span><span class="sxs-lookup"><span data-stu-id="c296b-115">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="c296b-116">Vizsgálja meg az eredményül kapott objektum [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="c296b-116">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="c296b-117">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="c296b-117">For an example, see the following:</span></span>

- <span data-ttu-id="c296b-118">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="c296b-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="c296b-119">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="c296b-119">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="c296b-120">Osztály: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="c296b-120">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="c296b-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c296b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c296b-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c296b-122">Request syntax</span></span>

| <span data-ttu-id="c296b-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="c296b-123">Method</span></span>  | <span data-ttu-id="c296b-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c296b-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="c296b-125">**GET**</span><span class="sxs-lookup"><span data-stu-id="c296b-125">**GET**</span></span> | <span data-ttu-id="c296b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories? ország = {ország-azonosító} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c296b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="c296b-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c296b-127">URI parameter</span></span>

<span data-ttu-id="c296b-128">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az ajánlati kategóriák beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="c296b-128">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="c296b-129">Név</span><span class="sxs-lookup"><span data-stu-id="c296b-129">Name</span></span>           | <span data-ttu-id="c296b-130">Típus</span><span class="sxs-lookup"><span data-stu-id="c296b-130">Type</span></span>       | <span data-ttu-id="c296b-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c296b-131">Required</span></span> | <span data-ttu-id="c296b-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="c296b-132">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="c296b-133">**ország azonosítója**</span><span class="sxs-lookup"><span data-stu-id="c296b-133">**country-id**</span></span> | <span data-ttu-id="c296b-134">**sztring**</span><span class="sxs-lookup"><span data-stu-id="c296b-134">**string**</span></span> | <span data-ttu-id="c296b-135">Y</span><span class="sxs-lookup"><span data-stu-id="c296b-135">Y</span></span>        | <span data-ttu-id="c296b-136">Az ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="c296b-136">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c296b-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c296b-137">Request headers</span></span>

<span data-ttu-id="c296b-138">A rendszer karakterláncként formázott **területi beállítás** megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="c296b-138">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="c296b-139">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c296b-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c296b-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c296b-140">Request body</span></span>

<span data-ttu-id="c296b-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c296b-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c296b-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c296b-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="c296b-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c296b-143">REST response</span></span>

<span data-ttu-id="c296b-144">Ha ez sikeres, ez a metódus **OfferCategory** -erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="c296b-144">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c296b-145">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c296b-145">Response success and error codes</span></span>

<span data-ttu-id="c296b-146">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c296b-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c296b-147">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c296b-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c296b-148">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c296b-148">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c296b-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c296b-149">Response example</span></span>

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
