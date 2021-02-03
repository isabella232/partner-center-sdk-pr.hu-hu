---
title: Az összes javaslat elemzési adatainak lekérése
description: Az összes átirányítási elemzés információjának beolvasása.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767928"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="9b074-103">Az összes javaslat elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="9b074-103">Get all referrals analytics information</span></span>

<span data-ttu-id="9b074-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="9b074-104">**Applies To**</span></span>

- <span data-ttu-id="9b074-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="9b074-105">Partner Center</span></span>
- <span data-ttu-id="9b074-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="9b074-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9b074-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="9b074-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9b074-108">Az összes átirányítási elemzés információinak beszerzése az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="9b074-108">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b074-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9b074-109">Prerequisites</span></span>

- <span data-ttu-id="9b074-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="9b074-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9b074-111">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="9b074-111">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="9b074-112">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="9b074-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9b074-113">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="9b074-113">Request syntax</span></span>

| <span data-ttu-id="9b074-114">Metódus</span><span class="sxs-lookup"><span data-stu-id="9b074-114">Method</span></span>  | <span data-ttu-id="9b074-115">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9b074-115">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="9b074-116">**GET**</span><span class="sxs-lookup"><span data-stu-id="9b074-116">**GET**</span></span> | <span data-ttu-id="9b074-117">[*\{ BASEURL \}*](partner-center-rest-urls.md)/partner/v1/Analytics/Referrals http/1.1</span><span class="sxs-lookup"><span data-stu-id="9b074-117">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="9b074-118">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="9b074-118">URI parameters</span></span>

| <span data-ttu-id="9b074-119">Paraméter</span><span class="sxs-lookup"><span data-stu-id="9b074-119">Parameter</span></span> | <span data-ttu-id="9b074-120">Típus</span><span class="sxs-lookup"><span data-stu-id="9b074-120">Type</span></span> | <span data-ttu-id="9b074-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="9b074-121">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="9b074-122">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="9b074-122">filter</span></span> | <span data-ttu-id="9b074-123">sztring</span><span class="sxs-lookup"><span data-stu-id="9b074-123">string</span></span> | <span data-ttu-id="9b074-124">A szűrési feltételnek megfelelő adatok visszaadása.</span><span class="sxs-lookup"><span data-stu-id="9b074-124">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="9b074-125">**Példa**</span><span class="sxs-lookup"><span data-stu-id="9b074-125">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="9b074-126">groupby</span><span class="sxs-lookup"><span data-stu-id="9b074-126">groupby</span></span> | <span data-ttu-id="9b074-127">sztring</span><span class="sxs-lookup"><span data-stu-id="9b074-127">string</span></span> | <span data-ttu-id="9b074-128">A a kifejezéseket és a dátumokat is támogatja.</span><span class="sxs-lookup"><span data-stu-id="9b074-128">Supports both terms and dates.</span></span> <span data-ttu-id="9b074-129">Rövidzárlat-logika a gyűjtők számának korlátozásához.</span><span class="sxs-lookup"><span data-stu-id="9b074-129">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="9b074-130">**Példa**</span><span class="sxs-lookup"><span data-stu-id="9b074-130">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="9b074-131">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="9b074-131">aggregationLevel</span></span> | <span data-ttu-id="9b074-132">sztring</span><span class="sxs-lookup"><span data-stu-id="9b074-132">string</span></span> | <span data-ttu-id="9b074-133">A *aggregationLevel* paraméterhez *groupby* szükséges.</span><span class="sxs-lookup"><span data-stu-id="9b074-133">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="9b074-134">A *aggregationLevel* paraméter a *groupby* lévő összes Date mezőre vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="9b074-134">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="9b074-135">**Példa**</span><span class="sxs-lookup"><span data-stu-id="9b074-135">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="9b074-136">top</span><span class="sxs-lookup"><span data-stu-id="9b074-136">top</span></span> | <span data-ttu-id="9b074-137">sztring</span><span class="sxs-lookup"><span data-stu-id="9b074-137">string</span></span> | <span data-ttu-id="9b074-138">Az oldal korlátja 10000.</span><span class="sxs-lookup"><span data-stu-id="9b074-138">The page limit is 10000.</span></span> <span data-ttu-id="9b074-139">10000-nál kisebb értéket vesz fel.</span><span class="sxs-lookup"><span data-stu-id="9b074-139">Takes any value less than 10000.</span></span></br> <span data-ttu-id="9b074-140">**Példa**</span><span class="sxs-lookup"><span data-stu-id="9b074-140">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="9b074-141">kihagyása</span><span class="sxs-lookup"><span data-stu-id="9b074-141">skip</span></span> | <span data-ttu-id="9b074-142">sztring</span><span class="sxs-lookup"><span data-stu-id="9b074-142">string</span></span> | <span data-ttu-id="9b074-143">A kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="9b074-143">Number of rows to skip.</span></span></br> <span data-ttu-id="9b074-144">**Példa**</span><span class="sxs-lookup"><span data-stu-id="9b074-144">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="9b074-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9b074-145">Request headers</span></span>

<span data-ttu-id="9b074-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9b074-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9b074-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9b074-147">Request body</span></span>

<span data-ttu-id="9b074-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="9b074-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9b074-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9b074-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="9b074-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9b074-150">REST response</span></span>

<span data-ttu-id="9b074-151">Ha ez sikeres, a válasz törzse az [átirányítási](partner-center-analytics-resources.md#referrals-resource) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="9b074-151">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9b074-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9b074-152">Response success and error codes</span></span>

<span data-ttu-id="9b074-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="9b074-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9b074-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="9b074-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9b074-155">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9b074-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9b074-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9b074-156">Response example</span></span>

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a><span data-ttu-id="9b074-157">Lásd még</span><span class="sxs-lookup"><span data-stu-id="9b074-157">See also</span></span>

- [<span data-ttu-id="9b074-158">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="9b074-158">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
