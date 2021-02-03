---
title: Az összes keresés elemzési adatainak lekérése
description: Az összes keresési elemzési információ beolvasása.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767712"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="86e1f-103">Az összes keresés elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="86e1f-103">Get all search analytics information</span></span>

<span data-ttu-id="86e1f-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="86e1f-104">**Applies To**</span></span>

- <span data-ttu-id="86e1f-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="86e1f-105">Partner Center</span></span>
- <span data-ttu-id="86e1f-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="86e1f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="86e1f-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="86e1f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="86e1f-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="86e1f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="86e1f-109">Az összes keresési elemzési információ beszerzése az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="86e1f-109">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86e1f-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="86e1f-110">Prerequisites</span></span>

- <span data-ttu-id="86e1f-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="86e1f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="86e1f-112">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="86e1f-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="86e1f-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="86e1f-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="86e1f-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="86e1f-114">Request syntax</span></span>

| <span data-ttu-id="86e1f-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="86e1f-115">Method</span></span>  | <span data-ttu-id="86e1f-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="86e1f-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="86e1f-117">**GET**</span><span class="sxs-lookup"><span data-stu-id="86e1f-117">**GET**</span></span> | <span data-ttu-id="86e1f-118">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Search http/1.1</span><span class="sxs-lookup"><span data-stu-id="86e1f-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="86e1f-119">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="86e1f-119">URI parameters</span></span>

|    <span data-ttu-id="86e1f-120">Paraméter</span><span class="sxs-lookup"><span data-stu-id="86e1f-120">Parameter</span></span>     |  <span data-ttu-id="86e1f-121">Típus</span><span class="sxs-lookup"><span data-stu-id="86e1f-121">Type</span></span>  |                                                                                                                   <span data-ttu-id="86e1f-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="86e1f-122">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="86e1f-123">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="86e1f-123">filter</span></span>      | <span data-ttu-id="86e1f-124">sztring</span><span class="sxs-lookup"><span data-stu-id="86e1f-124">string</span></span> |                                                                     <span data-ttu-id="86e1f-125">A szűrési feltételnek megfelelő adatok visszaadása.</span><span class="sxs-lookup"><span data-stu-id="86e1f-125">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="86e1f-126">**Példa**</span><span class="sxs-lookup"><span data-stu-id="86e1f-126">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="86e1f-127">groupby</span><span class="sxs-lookup"><span data-stu-id="86e1f-127">groupby</span></span>      | <span data-ttu-id="86e1f-128">sztring</span><span class="sxs-lookup"><span data-stu-id="86e1f-128">string</span></span> |                                         <span data-ttu-id="86e1f-129">A a kifejezéseket és a dátumokat is támogatja.</span><span class="sxs-lookup"><span data-stu-id="86e1f-129">Supports both terms and dates.</span></span> <span data-ttu-id="86e1f-130">Rövidzárlat-logika a gyűjtők számának korlátozásához.</span><span class="sxs-lookup"><span data-stu-id="86e1f-130">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="86e1f-131">**Példa**</span><span class="sxs-lookup"><span data-stu-id="86e1f-131">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="86e1f-132">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="86e1f-132">aggregationLevel</span></span> | <span data-ttu-id="86e1f-133">sztring</span><span class="sxs-lookup"><span data-stu-id="86e1f-133">string</span></span> | <span data-ttu-id="86e1f-134">A *aggregationLevel* paraméterhez *groupby* szükséges.</span><span class="sxs-lookup"><span data-stu-id="86e1f-134">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="86e1f-135">A *aggregationLevel* paraméter a *groupby* lévő összes Date mezőre vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="86e1f-135">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="86e1f-136">**Példa**</span><span class="sxs-lookup"><span data-stu-id="86e1f-136">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="86e1f-137">top</span><span class="sxs-lookup"><span data-stu-id="86e1f-137">top</span></span>        | <span data-ttu-id="86e1f-138">sztring</span><span class="sxs-lookup"><span data-stu-id="86e1f-138">string</span></span> |                                                                     <span data-ttu-id="86e1f-139">Az oldal korlátja 10000.</span><span class="sxs-lookup"><span data-stu-id="86e1f-139">The page limit is 10000.</span></span> <span data-ttu-id="86e1f-140">10000-nál kisebb értéket vesz fel.</span><span class="sxs-lookup"><span data-stu-id="86e1f-140">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="86e1f-141">**Példa**</span><span class="sxs-lookup"><span data-stu-id="86e1f-141">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="86e1f-142">kihagyása</span><span class="sxs-lookup"><span data-stu-id="86e1f-142">skip</span></span>       | <span data-ttu-id="86e1f-143">sztring</span><span class="sxs-lookup"><span data-stu-id="86e1f-143">string</span></span> |                                                                                  <span data-ttu-id="86e1f-144">A kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="86e1f-144">Number of rows to skip.</span></span> </br> <span data-ttu-id="86e1f-145">**Példa**</span><span class="sxs-lookup"><span data-stu-id="86e1f-145">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="86e1f-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="86e1f-146">Request headers</span></span>

<span data-ttu-id="86e1f-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="86e1f-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="86e1f-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="86e1f-148">Request body</span></span>

<span data-ttu-id="86e1f-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="86e1f-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="86e1f-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="86e1f-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="86e1f-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="86e1f-151">REST response</span></span>

<span data-ttu-id="86e1f-152">Ha ez sikeres, a válasz törzse [keresési](partner-center-analytics-resources.md#search-resource) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="86e1f-152">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="86e1f-153">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="86e1f-153">Response success and error codes</span></span>

<span data-ttu-id="86e1f-154">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="86e1f-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="86e1f-155">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="86e1f-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="86e1f-156">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="86e1f-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="86e1f-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="86e1f-157">Response example</span></span>

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a><span data-ttu-id="86e1f-158">Lásd még</span><span class="sxs-lookup"><span data-stu-id="86e1f-158">See also</span></span>

- [<span data-ttu-id="86e1f-159">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="86e1f-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
