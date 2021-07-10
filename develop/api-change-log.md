---
title: Partnerközpont – REST API-változásnapló
description: Ez az oldal a REST API-k Partnerközpont sorolja fel
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/09/2021
ms.locfileid: "113571995"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a><span data-ttu-id="838f8-103">A REST API-k Partnerközpont 2020. decemberi változásai</span><span class="sxs-lookup"><span data-stu-id="838f8-103">December 2020 changes to Partner Center REST APIs</span></span>

<span data-ttu-id="838f8-104">Itt ellenőrizheti a REST API Partnerközpont módosításait.</span><span class="sxs-lookup"><span data-stu-id="838f8-104">Check here for changes to Partner Center REST APIs.</span></span>

## <a name="enhancements-to-education-pricing-eligibility-apis"></a><span data-ttu-id="838f8-105">Az oktatási díjszabás jogosultsági API- k fejlesztései</span><span class="sxs-lookup"><span data-stu-id="838f8-105">Enhancements to education pricing Eligibility APIs</span></span>



### <a name="what-has-changed"></a><span data-ttu-id="838f8-106">Mi változott?</span><span class="sxs-lookup"><span data-stu-id="838f8-106">What has changed?</span></span>

<span data-ttu-id="838f8-107">A Partnerközpont API jelenleg GET és PUT minősítésekkel rendelkezik az Education-ügyfelek jogosultságának ellenőrzésére.</span><span class="sxs-lookup"><span data-stu-id="838f8-107">Currently, the Partner Center API has GET and PUT qualifications to verify Education customers’ eligibility.</span></span> <span data-ttu-id="838f8-108">A GET Qualification API nem módosul.</span><span class="sxs-lookup"><span data-stu-id="838f8-108">There will be no changes to the GET Qualification API.</span></span> <span data-ttu-id="838f8-109">Hozzáadtunk azonban egy visszatérési esetet a PUT-minősítési API-hoz.</span><span class="sxs-lookup"><span data-stu-id="838f8-109">However, we’ve added a return case to the PUT Qualification API.</span></span>

- <span data-ttu-id="838f8-110">GET – nem változik.</span><span class="sxs-lookup"><span data-stu-id="838f8-110">GET - doesn't change.</span></span>
- <span data-ttu-id="838f8-111">PUT – a visszatérési eset hozzá lesz adva.</span><span class="sxs-lookup"><span data-stu-id="838f8-111">PUT - return case will be added.</span></span>

<span data-ttu-id="838f8-112">Ezeket az API-kat 2021 februárjától kivezetjük, és az alábbiakban leírtak szerint új API-k váltják fel őket.</span><span class="sxs-lookup"><span data-stu-id="838f8-112">These APIs will be retired at the end of February 2021, to be replaced by new APIs as described below.</span></span>

### <a name="scenarios-impacted"></a><span data-ttu-id="838f8-113">Érintett forgatókönyvek:</span><span class="sxs-lookup"><span data-stu-id="838f8-113">Scenarios impacted:</span></span>

<span data-ttu-id="838f8-114">Az ügyfelek oktatási jogosultsága a kiválasztott termékcsomagok díjszabására</span><span class="sxs-lookup"><span data-stu-id="838f8-114">Customer eligibility for education pricing on select SKUs</span></span>

### <a name="detail-descriptions"></a><span data-ttu-id="838f8-115">Részletek leírása</span><span class="sxs-lookup"><span data-stu-id="838f8-115">Detail descriptions</span></span>

<span data-ttu-id="838f8-116">Két új GET és POST minősítési API lesz bevezetve.</span><span class="sxs-lookup"><span data-stu-id="838f8-116">Two new GET and POST Qualifications APIs will be introduced.</span></span> <span data-ttu-id="838f8-117">Az új API-k a **Minősítéseket fogják használni,** nem **a Minősítést.**</span><span class="sxs-lookup"><span data-stu-id="838f8-117">The new APIs will be using **Qualifications**, not **Qualification**.</span></span> <span data-ttu-id="838f8-118">Az API-k a 2. negyedévi FY21 teszteléshez lesznek elérhetők.</span><span class="sxs-lookup"><span data-stu-id="838f8-118">The APIs will be available for testing in FY21 Q2.</span></span>

#### <a name="get-qualifications"></a><span data-ttu-id="838f8-119">GET-minősítések</span><span class="sxs-lookup"><span data-stu-id="838f8-119">GET Qualifications</span></span>

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a><span data-ttu-id="838f8-120">Példa a válaszra:</span><span class="sxs-lookup"><span data-stu-id="838f8-120">Response example:</span></span>

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a><span data-ttu-id="838f8-121">Válaszmezők:</span><span class="sxs-lookup"><span data-stu-id="838f8-121">Response fields:</span></span> 

- <span data-ttu-id="838f8-122">VettingStatus-értékek: Approved (Jóváhagyva), Denied (Elutasítva), InReview (Áttekintés) stb.</span><span class="sxs-lookup"><span data-stu-id="838f8-122">VettingStatus values: Approved, Denied, InReview, etc.</span></span>

- <span data-ttu-id="838f8-123">A VettingReason értékei:</span><span class="sxs-lookup"><span data-stu-id="838f8-123">VettingReason values:</span></span>
   - <span data-ttu-id="838f8-124">Nem oktatási ügyfél</span><span class="sxs-lookup"><span data-stu-id="838f8-124">Not an Education Customer</span></span>
   - <span data-ttu-id="838f8-125">Már nem oktatási ügyfél</span><span class="sxs-lookup"><span data-stu-id="838f8-125">No longer an Education Customer</span></span>
   - <span data-ttu-id="838f8-126">Nem oktatási ügyfél – felülvizsgálat után</span><span class="sxs-lookup"><span data-stu-id="838f8-126">Not an Education Customer - After Review</span></span>
   - <span data-ttu-id="838f8-127">Oktatási ügyfélként korlátozott</span><span class="sxs-lookup"><span data-stu-id="838f8-127">Restricted being an Education Customer</span></span>
   - <span data-ttu-id="838f8-128">Nem tudományos tartomány</span><span class="sxs-lookup"><span data-stu-id="838f8-128">Not an Academic Domain</span></span>
   - <span data-ttu-id="838f8-129">Nem jogosult kódtár</span><span class="sxs-lookup"><span data-stu-id="838f8-129">Not an eligible Library</span></span>
   - <span data-ttu-id="838f8-130">Nem jogosult a Program</span><span class="sxs-lookup"><span data-stu-id="838f8-130">Not an eligible Museum</span></span>
 
#### <a name="post-qualifications"></a><span data-ttu-id="838f8-131">POST-minősítések</span><span class="sxs-lookup"><span data-stu-id="838f8-131">POST Qualifications</span></span>

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a><span data-ttu-id="838f8-132">Példa a válaszra:</span><span class="sxs-lookup"><span data-stu-id="838f8-132">Response example:</span></span>

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a><span data-ttu-id="838f8-133">Következő lépések</span><span class="sxs-lookup"><span data-stu-id="838f8-133">Next steps</span></span>

[<span data-ttu-id="838f8-134">Partnerközpont – REST API-referencia</span><span class="sxs-lookup"><span data-stu-id="838f8-134">Partner Center REST API reference</span></span>](partner-center-rest-api-reference.md)
