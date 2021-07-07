---
title: Az összes javaslat elemzési adatainak lekérése
description: A hivatkozások elemzési információinak lekérte.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 7deda4098ceb9eb4e1ee75056c53c754618bf3e2
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760606"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="599ae-103">Az összes javaslat elemzési adatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="599ae-103">Get all referrals analytics information</span></span>

<span data-ttu-id="599ae-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="599ae-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="599ae-105">Az ügyfelekre vonatkozó összes hivatkozáselemzési információ lekérte.</span><span class="sxs-lookup"><span data-stu-id="599ae-105">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="599ae-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="599ae-106">Prerequisites</span></span>

- <span data-ttu-id="599ae-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="599ae-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="599ae-108">Ez a forgatókönyv csak a felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="599ae-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="599ae-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="599ae-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="599ae-110">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="599ae-110">Request syntax</span></span>

| <span data-ttu-id="599ae-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="599ae-111">Method</span></span>  | <span data-ttu-id="599ae-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="599ae-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="599ae-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="599ae-113">**GET**</span></span> | <span data-ttu-id="599ae-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="599ae-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="599ae-115">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="599ae-115">URI parameters</span></span>

| <span data-ttu-id="599ae-116">Paraméter</span><span class="sxs-lookup"><span data-stu-id="599ae-116">Parameter</span></span> | <span data-ttu-id="599ae-117">Típus</span><span class="sxs-lookup"><span data-stu-id="599ae-117">Type</span></span> | <span data-ttu-id="599ae-118">Leírás</span><span class="sxs-lookup"><span data-stu-id="599ae-118">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="599ae-119">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="599ae-119">filter</span></span> | <span data-ttu-id="599ae-120">sztring</span><span class="sxs-lookup"><span data-stu-id="599ae-120">string</span></span> | <span data-ttu-id="599ae-121">A szűrési feltételnek megfelelő adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="599ae-121">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="599ae-122">**Példa**</span><span class="sxs-lookup"><span data-stu-id="599ae-122">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="599ae-123">groupby</span><span class="sxs-lookup"><span data-stu-id="599ae-123">groupby</span></span> | <span data-ttu-id="599ae-124">sztring</span><span class="sxs-lookup"><span data-stu-id="599ae-124">string</span></span> | <span data-ttu-id="599ae-125">A feltételeket és a dátumokat is támogatja.</span><span class="sxs-lookup"><span data-stu-id="599ae-125">Supports both terms and dates.</span></span> <span data-ttu-id="599ae-126">Rövid áramköri logika a gyűjtők számának korlátozására.</span><span class="sxs-lookup"><span data-stu-id="599ae-126">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="599ae-127">**Példa**</span><span class="sxs-lookup"><span data-stu-id="599ae-127">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="599ae-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="599ae-128">aggregationLevel</span></span> | <span data-ttu-id="599ae-129">sztring</span><span class="sxs-lookup"><span data-stu-id="599ae-129">string</span></span> | <span data-ttu-id="599ae-130">Az *aggregációszint* paraméterhez csoportosítás *szükséges.*</span><span class="sxs-lookup"><span data-stu-id="599ae-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="599ae-131">Az *aggregationLevel* paraméter a csoportosításban található összes *dátummezőre vonatkozik.*</span><span class="sxs-lookup"><span data-stu-id="599ae-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="599ae-132">**Példa**</span><span class="sxs-lookup"><span data-stu-id="599ae-132">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="599ae-133">top</span><span class="sxs-lookup"><span data-stu-id="599ae-133">top</span></span> | <span data-ttu-id="599ae-134">sztring</span><span class="sxs-lookup"><span data-stu-id="599ae-134">string</span></span> | <span data-ttu-id="599ae-135">Az oldalkorlát 10000.</span><span class="sxs-lookup"><span data-stu-id="599ae-135">The page limit is 10000.</span></span> <span data-ttu-id="599ae-136">10000-esnél kisebb értéket vesz fel.</span><span class="sxs-lookup"><span data-stu-id="599ae-136">Takes any value less than 10000.</span></span></br> <span data-ttu-id="599ae-137">**Példa**</span><span class="sxs-lookup"><span data-stu-id="599ae-137">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="599ae-138">Ugrál</span><span class="sxs-lookup"><span data-stu-id="599ae-138">skip</span></span> | <span data-ttu-id="599ae-139">sztring</span><span class="sxs-lookup"><span data-stu-id="599ae-139">string</span></span> | <span data-ttu-id="599ae-140">A kihagyni kívánt sorok száma.</span><span class="sxs-lookup"><span data-stu-id="599ae-140">Number of rows to skip.</span></span></br> <span data-ttu-id="599ae-141">**Példa**</span><span class="sxs-lookup"><span data-stu-id="599ae-141">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="599ae-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="599ae-142">Request headers</span></span>

<span data-ttu-id="599ae-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="599ae-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="599ae-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="599ae-144">Request body</span></span>

<span data-ttu-id="599ae-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="599ae-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="599ae-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="599ae-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="599ae-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="599ae-147">REST response</span></span>

<span data-ttu-id="599ae-148">Ha ez sikeres, a válasz törzse hivatkozási erőforrások [gyűjteményét](partner-center-analytics-resources.md#referrals-resource) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="599ae-148">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="599ae-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="599ae-149">Response success and error codes</span></span>

<span data-ttu-id="599ae-150">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="599ae-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="599ae-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="599ae-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="599ae-152">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="599ae-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="599ae-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="599ae-153">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="599ae-154">Lásd még</span><span class="sxs-lookup"><span data-stu-id="599ae-154">See also</span></span>

- [<span data-ttu-id="599ae-155">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="599ae-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
