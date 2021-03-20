---
title: Partnerközpont – REST API-változásnapló
description: Ez az oldal a partner Center REST API-k változásait sorolja fel
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: b2c2cac36a8bd1bec7aa5bf6e5d1aa73b4779535
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711848"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="e3dfe-103">December 2020 a partner Center REST API-k változásai</span><span class="sxs-lookup"><span data-stu-id="e3dfe-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="e3dfe-104">Tekintse át a partner Center REST API-k módosításait.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="e3dfe-105">Fejlesztés az oktatási árképzés támogathatósági API-jai számára</span><span class="sxs-lookup"><span data-stu-id="e3dfe-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="e3dfe-106">Mi változott?</span><span class="sxs-lookup"><span data-stu-id="e3dfe-106">What has changed?</span></span>

<span data-ttu-id="e3dfe-107">A partner Center API jelenleg az oktatási ügyfelek jogosultságának ellenőrzéséhez és a képesítések beszerzéséhez szükséges.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="e3dfe-108">A GET minősítési API-t nem változtatja meg.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="e3dfe-109">Azonban a PUT minősítési API-hoz hozzáadott egy visszatérési esetet.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="e3dfe-110">A GET-nem változik.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-110">GET - doesn't change.</span></span> [<span data-ttu-id="e3dfe-111">Aktuális API-cikk</span><span class="sxs-lookup"><span data-stu-id="e3dfe-111">Current API article</span></span>](./get-customer-qualification-synchronous.md)
- <span data-ttu-id="e3dfe-112">A rendszer felveszi a visszaküldési esetet.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-112">PUT - return case will be added.</span></span> [<span data-ttu-id="e3dfe-113">Aktuális API-cikk</span><span class="sxs-lookup"><span data-stu-id="e3dfe-113">Current API article</span></span>](./update-customer-qualification-synchronous.md)

<span data-ttu-id="e3dfe-114">Ezek az API-k február 2021 végén megszűnnek, és az alább leírtak szerint új API-kat kell cserélni.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-114">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="e3dfe-115">Érintett forgatókönyvek:</span><span class="sxs-lookup"><span data-stu-id="e3dfe-115">Scenarios impacted:</span></span>

<span data-ttu-id="e3dfe-116">Ügyfél-jogosultság az oktatási díjszabáshoz a Select SKUs esetében</span><span class="sxs-lookup"><span data-stu-id="e3dfe-116">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="e3dfe-117">Részletes leírások</span><span class="sxs-lookup"><span data-stu-id="e3dfe-117">Detail descriptions</span></span>

<span data-ttu-id="e3dfe-118">A rendszer két új GET és POST minősítési API-t fog bevezetni.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-118">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="e3dfe-119">Az új API-k **képesítéseket** és nem **minősítést** használnak.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-119">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="e3dfe-120">Az API-k a FY21 Q2-ben való teszteléshez lesznek elérhetők.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-120">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="e3dfe-121">Végzettség beszerzése</span><span class="sxs-lookup"><span data-stu-id="e3dfe-121">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="e3dfe-122">Példa a válaszra:</span><span class="sxs-lookup"><span data-stu-id="e3dfe-122">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="e3dfe-123">Válasz mezői:</span><span class="sxs-lookup"><span data-stu-id="e3dfe-123">Response fields:</span></span> 

- <span data-ttu-id="e3dfe-124">VettingStatus-értékek: jóváhagyva, megtagadva, inreview stb.</span><span class="sxs-lookup"><span data-stu-id="e3dfe-124">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="e3dfe-125">VettingReason értékek:</span><span class="sxs-lookup"><span data-stu-id="e3dfe-125">VettingReason values:</span></span>
   - <span data-ttu-id="e3dfe-126">Nem oktatási ügyfél</span><span class="sxs-lookup"><span data-stu-id="e3dfe-126">Not an Education Customer</span></span>
   - <span data-ttu-id="e3dfe-127">Már nem oktatási ügyfél</span><span class="sxs-lookup"><span data-stu-id="e3dfe-127">No longer an Education Customer</span></span>
   - <span data-ttu-id="e3dfe-128">Nem oktatási ügyfél – felülvizsgálat után</span><span class="sxs-lookup"><span data-stu-id="e3dfe-128">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="e3dfe-129">Korlátozott oktatási ügyfél</span><span class="sxs-lookup"><span data-stu-id="e3dfe-129">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="e3dfe-130">Nem akadémiai tartomány</span><span class="sxs-lookup"><span data-stu-id="e3dfe-130">Not an Academic Domain</span></span>
   - <span data-ttu-id="e3dfe-131">Nem jogosult könyvtár</span><span class="sxs-lookup"><span data-stu-id="e3dfe-131">Not an eligible Library</span></span>
   - <span data-ttu-id="e3dfe-132">Nem jogosult Múzeum</span><span class="sxs-lookup"><span data-stu-id="e3dfe-132">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="e3dfe-133">POST minősítések</span><span class="sxs-lookup"><span data-stu-id="e3dfe-133">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="e3dfe-134">Példa a válaszra:</span><span class="sxs-lookup"><span data-stu-id="e3dfe-134">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="e3dfe-135">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="e3dfe-135">Next steps</span></span>

[<span data-ttu-id="e3dfe-136">Partnerközpont – REST API-referencia</span><span class="sxs-lookup"><span data-stu-id="e3dfe-136">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)