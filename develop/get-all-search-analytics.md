---
title: Az összes keresés elemzési adatainak lekérése
description: A keresési elemzésekre vonatkozó összes információ lekért információ.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e789a013b01fb63a38c72f4fe94864ecf21f7e4b
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760164"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="89af9-103">Az összes keresés elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="89af9-103">Get all search analytics information</span></span>

<span data-ttu-id="89af9-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="89af9-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="89af9-105">Az összes keresési elemzési információ lekért információ az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="89af9-105">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89af9-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="89af9-106">Prerequisites</span></span>

- <span data-ttu-id="89af9-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="89af9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="89af9-108">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="89af9-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="89af9-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="89af9-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="89af9-110">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="89af9-110">Request syntax</span></span>

| <span data-ttu-id="89af9-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="89af9-111">Method</span></span>  | <span data-ttu-id="89af9-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="89af9-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="89af9-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="89af9-113">**GET**</span></span> | <span data-ttu-id="89af9-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="89af9-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="89af9-115">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="89af9-115">URI parameters</span></span>

|    <span data-ttu-id="89af9-116">Paraméter</span><span class="sxs-lookup"><span data-stu-id="89af9-116">Parameter</span></span>     |  <span data-ttu-id="89af9-117">Típus</span><span class="sxs-lookup"><span data-stu-id="89af9-117">Type</span></span>  |                                                                                                                   <span data-ttu-id="89af9-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="89af9-118">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="89af9-119">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="89af9-119">filter</span></span>      | <span data-ttu-id="89af9-120">sztring</span><span class="sxs-lookup"><span data-stu-id="89af9-120">string</span></span> |                                                                     <span data-ttu-id="89af9-121">A szűrési feltételnek megfelelő adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="89af9-121">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="89af9-122">**Példa**</span><span class="sxs-lookup"><span data-stu-id="89af9-122">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="89af9-123">groupby (csoportosítás)</span><span class="sxs-lookup"><span data-stu-id="89af9-123">groupby</span></span>      | <span data-ttu-id="89af9-124">sztring</span><span class="sxs-lookup"><span data-stu-id="89af9-124">string</span></span> |                                         <span data-ttu-id="89af9-125">A feltételeket és a dátumokat is támogatja.</span><span class="sxs-lookup"><span data-stu-id="89af9-125">Supports both terms and dates.</span></span> <span data-ttu-id="89af9-126">Rövid áramköri logika a gyűjtők számának korlátozására.</span><span class="sxs-lookup"><span data-stu-id="89af9-126">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="89af9-127">**Példa**</span><span class="sxs-lookup"><span data-stu-id="89af9-127">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="89af9-128">aggregationLevel (összesítési szint)</span><span class="sxs-lookup"><span data-stu-id="89af9-128">aggregationLevel</span></span> | <span data-ttu-id="89af9-129">sztring</span><span class="sxs-lookup"><span data-stu-id="89af9-129">string</span></span> | <span data-ttu-id="89af9-130">Az *aggregációszint* paraméterhez csoportosítás *szükséges.*</span><span class="sxs-lookup"><span data-stu-id="89af9-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="89af9-131">Az *aggregátumszint* paraméter a csoportosítási gyűjtőben található összes *dátummezőre vonatkozik.*</span><span class="sxs-lookup"><span data-stu-id="89af9-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="89af9-132">**Példa**</span><span class="sxs-lookup"><span data-stu-id="89af9-132">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="89af9-133">top</span><span class="sxs-lookup"><span data-stu-id="89af9-133">top</span></span>        | <span data-ttu-id="89af9-134">sztring</span><span class="sxs-lookup"><span data-stu-id="89af9-134">string</span></span> |                                                                     <span data-ttu-id="89af9-135">Az oldalkorlát 10000.</span><span class="sxs-lookup"><span data-stu-id="89af9-135">The page limit is 10000.</span></span> <span data-ttu-id="89af9-136">10000-esnél kisebb értéket vesz fel.</span><span class="sxs-lookup"><span data-stu-id="89af9-136">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="89af9-137">**Példa**</span><span class="sxs-lookup"><span data-stu-id="89af9-137">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="89af9-138">Ugrál</span><span class="sxs-lookup"><span data-stu-id="89af9-138">skip</span></span>       | <span data-ttu-id="89af9-139">sztring</span><span class="sxs-lookup"><span data-stu-id="89af9-139">string</span></span> |                                                                                  <span data-ttu-id="89af9-140">A kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="89af9-140">Number of rows to skip.</span></span> </br> <span data-ttu-id="89af9-141">**Példa**</span><span class="sxs-lookup"><span data-stu-id="89af9-141">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="89af9-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="89af9-142">Request headers</span></span>

<span data-ttu-id="89af9-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="89af9-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="89af9-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="89af9-144">Request body</span></span>

<span data-ttu-id="89af9-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="89af9-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="89af9-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="89af9-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="89af9-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="89af9-147">REST response</span></span>

<span data-ttu-id="89af9-148">Ha a művelet sikeres, a válasz törzse keresési erőforrások [gyűjteményét](partner-center-analytics-resources.md#search-resource) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="89af9-148">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="89af9-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="89af9-149">Response success and error codes</span></span>

<span data-ttu-id="89af9-150">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="89af9-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89af9-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="89af9-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89af9-152">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="89af9-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="89af9-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="89af9-153">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="89af9-154">Lásd még</span><span class="sxs-lookup"><span data-stu-id="89af9-154">See also</span></span>

- [<span data-ttu-id="89af9-155">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="89af9-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
