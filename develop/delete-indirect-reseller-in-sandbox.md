---
title: Közvetett viszonteladó törlése a sandboxban
description: Információkat nyújt a tesztbox közvetett viszonteladóinak törlésével és a teljes tesztelés API-okkal való engedélyezésével kapcsolatban.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba1fd002ac62aba4e414d263b33ecc8153054602
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973009"
---
# <a name="delete-indirect-reseller-in-sandbox"></a><span data-ttu-id="834b1-103">Közvetett viszonteladó törlése a sandboxban</span><span class="sxs-lookup"><span data-stu-id="834b1-103">Delete Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="834b1-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="834b1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="834b1-105">Ez a dokumentum bemutatja, hogyan törölhet közvetett tesztkészlet-szolgáltatókat, és hogyan engedélyezheti a teljes tesztelést API-k használatával.</span><span class="sxs-lookup"><span data-stu-id="834b1-105">This document shows how to delete Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

> [!Important]
> <span data-ttu-id="834b1-106">Ez a dokumentum azokat a funkciókat ismerteti, amelyek csak a sandbox környezetben engedélyezettek a közvetett modellélmények esetében.</span><span class="sxs-lookup"><span data-stu-id="834b1-106">This document describes features that are only allowed in the Sandbox environment for Indirect Model experiences.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="834b1-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="834b1-107">Prerequisites</span></span>

- <span data-ttu-id="834b1-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="834b1-108">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="834b1-109">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="834b1-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a><span data-ttu-id="834b1-110">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller</span><span class="sxs-lookup"><span data-stu-id="834b1-110">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller</span></span> 

<span data-ttu-id="834b1-111">Ez a funkció csak a Sandboxban érhető el, és lehetővé teszi a Sandbox indirect Resellers (Közvetett viszonteladók) létrehozására a Sandbox Indirect Providers (Közvetett viszonteladók) szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="834b1-111">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="834b1-112">A sandbox indirect reseller törlésének előfeltételei</span><span class="sxs-lookup"><span data-stu-id="834b1-112">Prerequisites for Deleting a Sandbox Indirect Reseller</span></span>
    1. <span data-ttu-id="834b1-113">Az előfizetések felfüggesztése a Sandbox Indirect Reseller minden egyes ügyfele esetében</span><span class="sxs-lookup"><span data-stu-id="834b1-113">Suspend the subscriptions for each customer of Sandbox Indirect Reseller</span></span>
    2. <span data-ttu-id="834b1-114">Közvetett viszonteladó összes ügyfele törlése</span><span class="sxs-lookup"><span data-stu-id="834b1-114">Delete all customers of Indirect Reseller</span></span>
2. <span data-ttu-id="834b1-115">A közvetett sandbox-viszonteladók engedélyezett maximális száma közvetett sandbox-szolgáltatónként.</span><span class="sxs-lookup"><span data-stu-id="834b1-115">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="834b1-116">A közvetett sandbox (közvetett) viszonteladó törlése után a kvóta alaphelyzetbe áll.</span><span class="sxs-lookup"><span data-stu-id="834b1-116">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

## <a name="delete-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="834b1-117">Delete Sandbox Indirect Reseller through API</span><span class="sxs-lookup"><span data-stu-id="834b1-117">Delete Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="834b1-118">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="834b1-118">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="834b1-119">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="834b1-119">Request syntax</span></span>

| <span data-ttu-id="834b1-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="834b1-120">Method</span></span> | <span data-ttu-id="834b1-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="834b1-121">Request URI</span></span>                                                                             |
|------------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="834b1-122">**Töröl**</span><span class="sxs-lookup"><span data-stu-id="834b1-122">**DELETE**</span></span> | <span data-ttu-id="834b1-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span><span class="sxs-lookup"><span data-stu-id="834b1-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="834b1-124">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="834b1-124">Request headers</span></span>

- <span data-ttu-id="834b1-125">Ez az API idempotent (nem fog más eredményt eredményezni, ha többször is meghívja)</span><span class="sxs-lookup"><span data-stu-id="834b1-125">This API is idempotent (it will not yield a different result if you call it multiple times)</span></span>
- <span data-ttu-id="834b1-126">Szükség van egy kérésazonosítóra és egy korrelációs azonosítóra</span><span class="sxs-lookup"><span data-stu-id="834b1-126">A request ID and correlation ID are required</span></span>
- <span data-ttu-id="834b1-127">További információ: [REST Partnerközpont fejlécek](headers.md)</span><span class="sxs-lookup"><span data-stu-id="834b1-127">For more information, see [Partner Center REST headers](headers.md)</span></span>

### <a name="request-example"></a><span data-ttu-id="834b1-128">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="834b1-128">Request Example</span></span>

<span data-ttu-id="834b1-129">Töröl https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span><span class="sxs-lookup"><span data-stu-id="834b1-129">DELETE https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span></span>

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a><span data-ttu-id="834b1-130">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="834b1-130">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="834b1-131">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="834b1-131">Response success and error codes</span></span>

<span data-ttu-id="834b1-132">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint egyéb hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="834b1-132">Each response comes with an HTTP status code that indicates success or failure and other debugging information.</span></span> <span data-ttu-id="834b1-133">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="834b1-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="834b1-134">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="834b1-134">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="834b1-135">Ez a metódus a következő sikeres állapotot és hibakódokat adja vissza:</span><span class="sxs-lookup"><span data-stu-id="834b1-135">This method returns the following status success and error codes:</span></span>

| <span data-ttu-id="834b1-136">HTTP-állapotkód</span><span class="sxs-lookup"><span data-stu-id="834b1-136">HTTP Status Code</span></span>                     | <span data-ttu-id="834b1-137">Hibakód</span><span class="sxs-lookup"><span data-stu-id="834b1-137">Error code</span></span>     | <span data-ttu-id="834b1-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="834b1-138">Description</span></span>                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="834b1-139">401</span><span class="sxs-lookup"><span data-stu-id="834b1-139">401</span></span>                                  | <span data-ttu-id="834b1-140">6002</span><span class="sxs-lookup"><span data-stu-id="834b1-140">6002</span></span>           | <span data-ttu-id="834b1-141">Jogosulatlan jogkivonat vagy nem tippszolgáltatói fiók</span><span class="sxs-lookup"><span data-stu-id="834b1-141">Unauthorized token or Not a Tip Provider Account</span></span> |
| <span data-ttu-id="834b1-142">403</span><span class="sxs-lookup"><span data-stu-id="834b1-142">403</span></span>                                  | <span data-ttu-id="834b1-143">6003</span><span class="sxs-lookup"><span data-stu-id="834b1-143">6003</span></span>           | <span data-ttu-id="834b1-144">A Delete Sandbox IR nem engedélyezett</span><span class="sxs-lookup"><span data-stu-id="834b1-144">Delete Sandbox IR is not allowed</span></span>                 |
| <span data-ttu-id="834b1-145">403</span><span class="sxs-lookup"><span data-stu-id="834b1-145">403</span></span>                                  | <span data-ttu-id="834b1-146">6004</span><span class="sxs-lookup"><span data-stu-id="834b1-146">6004</span></span>           | <span data-ttu-id="834b1-147">A sandbox IR-művelet létrehozása nem engedélyezett</span><span class="sxs-lookup"><span data-stu-id="834b1-147">Create Sandbox IR operation not allowed</span></span>          |
| <span data-ttu-id="834b1-148">409</span><span class="sxs-lookup"><span data-stu-id="834b1-148">409</span></span>                                  | <span data-ttu-id="834b1-149">1003</span><span class="sxs-lookup"><span data-stu-id="834b1-149">1003</span></span>           | <span data-ttu-id="834b1-150">Ütközés a bérlő létrehozása során</span><span class="sxs-lookup"><span data-stu-id="834b1-150">Conflict while creating tenant</span></span>                   |
