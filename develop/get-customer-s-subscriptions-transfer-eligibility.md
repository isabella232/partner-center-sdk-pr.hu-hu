---
title: Egy ügyfél előfizetési áthelyezési jogosultságainak lekérése
description: Ügyfél-előfizetések gyűjteményének beszerzése, amelyek jogosultak/ineligibile az átvitelhez.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 43086a32fa0dbbdecf65aac167c687f26fc4c2c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767703"
---
# <a name="get-a-customers-subscriptions-transfer-eligibility"></a><span data-ttu-id="36fd5-103">Egy ügyfél előfizetési áthelyezési jogosultságainak lekérése</span><span class="sxs-lookup"><span data-stu-id="36fd5-103">Get a customer's subscriptions transfer eligibility</span></span>

<span data-ttu-id="36fd5-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="36fd5-104">**Applies To**</span></span>

- <span data-ttu-id="36fd5-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="36fd5-105">Partner Center</span></span>

<span data-ttu-id="36fd5-106">Ügyfél-előfizetések gyűjteményének beszerzése, amelyek jogosultak/nem jogosultak az átvitelre.</span><span class="sxs-lookup"><span data-stu-id="36fd5-106">How to get a collection of a customer's subscriptions that are eligible/ineligible for transfer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36fd5-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="36fd5-107">Prerequisites</span></span>

- <span data-ttu-id="36fd5-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="36fd5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="36fd5-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="36fd5-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="36fd5-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="36fd5-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="36fd5-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="36fd5-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="36fd5-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="36fd5-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="36fd5-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="36fd5-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="36fd5-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="36fd5-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="36fd5-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="36fd5-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="36fd5-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="36fd5-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="36fd5-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="36fd5-117">Request syntax</span></span>

| <span data-ttu-id="36fd5-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="36fd5-118">Method</span></span>  | <span data-ttu-id="36fd5-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="36fd5-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="36fd5-120">**GET**</span><span class="sxs-lookup"><span data-stu-id="36fd5-120">**GET**</span></span> | <span data-ttu-id="36fd5-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/transferseligibility? transferType = {átvitel-típus} http/1.1</span><span class="sxs-lookup"><span data-stu-id="36fd5-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/transferseligibility?transferType={transfer-type} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="36fd5-122">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="36fd5-122">URI parameter</span></span>

<span data-ttu-id="36fd5-123">Ez a táblázat felsorolja az összes előfizetés lekéréséhez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="36fd5-123">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="36fd5-124">Név</span><span class="sxs-lookup"><span data-stu-id="36fd5-124">Name</span></span>               | <span data-ttu-id="36fd5-125">Típus</span><span class="sxs-lookup"><span data-stu-id="36fd5-125">Type</span></span>   | <span data-ttu-id="36fd5-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="36fd5-126">Required</span></span> | <span data-ttu-id="36fd5-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="36fd5-127">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="36fd5-128">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="36fd5-128">customer-tenant-id</span></span> | <span data-ttu-id="36fd5-129">sztring</span><span class="sxs-lookup"><span data-stu-id="36fd5-129">string</span></span> | <span data-ttu-id="36fd5-130">Igen</span><span class="sxs-lookup"><span data-stu-id="36fd5-130">Yes</span></span>      | <span data-ttu-id="36fd5-131">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="36fd5-131">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="36fd5-132">átvitel típusa</span><span class="sxs-lookup"><span data-stu-id="36fd5-132">transfer-type</span></span>      | <span data-ttu-id="36fd5-133">sztring</span><span class="sxs-lookup"><span data-stu-id="36fd5-133">string</span></span> | <span data-ttu-id="36fd5-134">Igen</span><span class="sxs-lookup"><span data-stu-id="36fd5-134">Yes</span></span>      | <span data-ttu-id="36fd5-135">A kívánt átvitel típusa.</span><span class="sxs-lookup"><span data-stu-id="36fd5-135">The type of transfer that is intended.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="36fd5-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="36fd5-136">Request headers</span></span>

<span data-ttu-id="36fd5-137">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="36fd5-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="36fd5-138">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="36fd5-138">Request body</span></span>

<span data-ttu-id="36fd5-139">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="36fd5-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="36fd5-140">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="36fd5-140">Request example</span></span>

```http
GET /v1/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transferseligibility?transferType=directtoindirect HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 202b5e9a-ae82-4ab9-8a0a-f4e9e04eb14d
MS-CorrelationId: cd589c16-dc94-49ad-e529-125c258573d6
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="36fd5-141">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="36fd5-141">REST response</span></span>

<span data-ttu-id="36fd5-142">Ha ez sikeres, ez a metódus [TransferEligibility](transfer-eligibility-resources.md) -erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="36fd5-142">If successful, this method returns a collection of [TransferEligibility](transfer-eligibility-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="36fd5-143">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="36fd5-143">Response success and error codes</span></span>

<span data-ttu-id="36fd5-144">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="36fd5-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="36fd5-145">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="36fd5-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="36fd5-146">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="36fd5-146">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="36fd5-147">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="36fd5-147">Response example</span></span>

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
