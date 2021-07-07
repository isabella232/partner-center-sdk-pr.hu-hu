---
title: Egy ügyfél előfizetési áthelyezési jogosultságainak lekérése
description: Az ügyfél átadásra jogosult/nem megfelelő előfizetései gyűjteményének lekérte.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: fe8af76d1e1456754dec79291ec0853fb253d108
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446292"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="4a2ba-103">Egy ügyfél előfizetési áthelyezési jogosultságainak lekérése</span><span class="sxs-lookup"><span data-stu-id="4a2ba-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="4a2ba-104">Hogyan gyűjthető be egy ügyfél átadásra jogosult vagy nem jogosult előfizetésének gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-104">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a2ba-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4a2ba-105">Prerequisites</span></span>

- <span data-ttu-id="4a2ba-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4a2ba-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4a2ba-107">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4a2ba-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4a2ba-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4a2ba-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4a2ba-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4a2ba-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4a2ba-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4a2ba-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4a2ba-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4a2ba-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="4a2ba-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4a2ba-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4a2ba-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="4a2ba-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4a2ba-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4a2ba-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4a2ba-115">Request syntax</span></span>

| <span data-ttu-id="4a2ba-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="4a2ba-116">Method</span></span>  | <span data-ttu-id="4a2ba-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4a2ba-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4a2ba-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="4a2ba-118">**GET**</span></span> | <span data-ttu-id="4a2ba-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4a2ba-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4a2ba-120">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4a2ba-120">URI parameter</span></span>

<span data-ttu-id="4a2ba-121">Ez a táblázat felsorolja az összes előfizetés lekért lekérdezési paraméterét.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-121">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="4a2ba-122">Név</span><span class="sxs-lookup"><span data-stu-id="4a2ba-122">Name</span></span>               | <span data-ttu-id="4a2ba-123">Típus</span><span class="sxs-lookup"><span data-stu-id="4a2ba-123">Type</span></span>   | <span data-ttu-id="4a2ba-124">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4a2ba-124">Required</span></span> | <span data-ttu-id="4a2ba-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="4a2ba-125">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="4a2ba-126">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="4a2ba-126">customer-tenant-id</span></span> | <span data-ttu-id="4a2ba-127">sztring</span><span class="sxs-lookup"><span data-stu-id="4a2ba-127">string</span></span> | <span data-ttu-id="4a2ba-128">Igen</span><span class="sxs-lookup"><span data-stu-id="4a2ba-128">Yes</span></span>      | <span data-ttu-id="4a2ba-129">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-129">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="4a2ba-130">transfer-type (átviteli típus)</span><span class="sxs-lookup"><span data-stu-id="4a2ba-130">transfer-type</span></span>      | <span data-ttu-id="4a2ba-131">sztring</span><span class="sxs-lookup"><span data-stu-id="4a2ba-131">string</span></span> | <span data-ttu-id="4a2ba-132">Igen</span><span class="sxs-lookup"><span data-stu-id="4a2ba-132">Yes</span></span>      | <span data-ttu-id="4a2ba-133">A kívánt átvitel típusa.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-133">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="4a2ba-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4a2ba-134">Request headers</span></span>

<span data-ttu-id="4a2ba-135">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4a2ba-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4a2ba-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4a2ba-136">Request body</span></span>

<span data-ttu-id="4a2ba-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4a2ba-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4a2ba-138">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="4a2ba-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4a2ba-139">REST response</span></span>

<span data-ttu-id="4a2ba-140">Ha a művelet sikeres, ez a metódus [TransferEligibility-erőforrások gyűjteményét](transfer-eligibility-resources.md) adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-140">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4a2ba-141">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4a2ba-141">Response success and error codes</span></span>

<span data-ttu-id="4a2ba-142">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4a2ba-143">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4a2ba-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4a2ba-144">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4a2ba-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4a2ba-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4a2ba-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
Date: Tue, 24 Mar 2020 23:43:25 GMT

[
  {
    "id": "548FA265-5F40-4765-9A6B-47826F72A4BF",
    "isEligible": false,
    "reason": "Subscription: 548FA265-5F40-4765-9A6B-47826F72A4BF is in state: Deleted"
  },
  {
    "id": "E2A3AEB3-70A7-42E3-930C-7519EEDDC45A",
    "isEligible": false,
    "reason": "Subscription: E2A3AEB3-70A7-42E3-930C-7519EEDDC45A is in state: Suspended"
  },
  {
    "id": "4B600A9A-DF56-4564-A75A-6CC6D2D0C9F9",
    "isEligible": false,
    "reason": "subscription is already part of another transfer request id : 31a06eac-c527-458a-a6b4-0de197a45996"
  },
  {
    "id": "D3350F46-AA29-4F6F-95A0-E3011988915C",
    "isEligible": true
  }
  {
    "id": "E82B2F4A-736A-4E2B-955C-C1A4C56C0171",
    "isEligible": true
  }
]
```
