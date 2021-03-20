---
title: Ügyfél képzettségének beszerzése
description: Megtudhatja, hogyan használhatja az aszinkron érvényesítést az ügyfél a partner Center API-n keresztüli minősítésének beszerzéséhez. A partnerek ezt az oktatási ügyfelek ellenőrzésére használhatják.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 2c860d4a35104131197e06d4712f4ef41ba0008e
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711913"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="d4ad6-104">Ügyfél-képesítés aszinkron beszerzése</span><span class="sxs-lookup"><span data-stu-id="d4ad6-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="d4ad6-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="d4ad6-105">**Applies To**</span></span>

- <span data-ttu-id="d4ad6-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d4ad6-106">Partner Center</span></span>

<span data-ttu-id="d4ad6-107">Az ügyfél képzettségének aszinkron beszerzése.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4ad6-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d4ad6-108">Prerequisites</span></span>

- <span data-ttu-id="d4ad6-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d4ad6-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d4ad6-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d4ad6-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d4ad6-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d4ad6-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d4ad6-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d4ad6-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d4ad6-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d4ad6-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d4ad6-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="d4ad6-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="d4ad6-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d4ad6-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d4ad6-118">Request syntax</span></span>

| <span data-ttu-id="d4ad6-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="d4ad6-119">Method</span></span>  | <span data-ttu-id="d4ad6-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d4ad6-120">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d4ad6-121">**GET**</span><span class="sxs-lookup"><span data-stu-id="d4ad6-121">**GET**</span></span> | <span data-ttu-id="d4ad6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="d4ad6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d4ad6-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d4ad6-123">URI parameter</span></span>

<span data-ttu-id="d4ad6-124">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az összes minősítés beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-124">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="d4ad6-125">Név</span><span class="sxs-lookup"><span data-stu-id="d4ad6-125">Name</span></span>               | <span data-ttu-id="d4ad6-126">Típus</span><span class="sxs-lookup"><span data-stu-id="d4ad6-126">Type</span></span>   | <span data-ttu-id="d4ad6-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d4ad6-127">Required</span></span> | <span data-ttu-id="d4ad6-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="d4ad6-128">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="d4ad6-129">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="d4ad6-129">**customer-tenant-id**</span></span> | <span data-ttu-id="d4ad6-130">sztring</span><span class="sxs-lookup"><span data-stu-id="d4ad6-130">string</span></span> | <span data-ttu-id="d4ad6-131">Yes</span><span class="sxs-lookup"><span data-stu-id="d4ad6-131">Yes</span></span>      | <span data-ttu-id="d4ad6-132">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-132">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d4ad6-133">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d4ad6-133">Request headers</span></span>

<span data-ttu-id="d4ad6-134">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d4ad6-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d4ad6-135">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d4ad6-135">Request body</span></span>

<span data-ttu-id="d4ad6-136">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d4ad6-137">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d4ad6-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="d4ad6-138">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d4ad6-138">REST response</span></span>

<span data-ttu-id="d4ad6-139">Ha a művelet sikeres, ez a módszer képesítések gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-139">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="d4ad6-140">Az alábbi példák az **oktatási** végzettséggel rendelkező ügyfelekre vonatkozó **Get** hívásra vonatkoznak.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-140">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d4ad6-141">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d4ad6-141">Response success and error codes</span></span>

<span data-ttu-id="d4ad6-142">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d4ad6-143">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d4ad6-144">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="d4ad6-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="d4ad6-145">Példák a válaszokra</span><span class="sxs-lookup"><span data-stu-id="d4ad6-145">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="d4ad6-146">Approved</span><span class="sxs-lookup"><span data-stu-id="d4ad6-146">Approved</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Approved",
        }
    ]
}

```

#### <a name="in-review"></a><span data-ttu-id="d4ad6-147">In Review (Felülvizsgálat alatt)</span><span class="sxs-lookup"><span data-stu-id="d4ad6-147">In Review</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "InReview",
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

#### <a name="denied"></a><span data-ttu-id="d4ad6-148">Megtagadva</span><span class="sxs-lookup"><span data-stu-id="d4ad6-148">Denied</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Denied",
            "vettingReason": "Not an Education Customer", // example Vetting Reason
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

## <a name="related-articles"></a><span data-ttu-id="d4ad6-149">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="d4ad6-149">Related articles</span></span>

- [<span data-ttu-id="d4ad6-150">Ügyfél végzettségének frissítése</span><span class="sxs-lookup"><span data-stu-id="d4ad6-150">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)