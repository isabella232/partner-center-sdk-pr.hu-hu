---
title: Ügyfél képzettségének beszerzése
description: Megtudhatja, hogyan használhatja az aszinkron érvényesítést az ügyfél a partner Center API-n keresztüli minősítésének beszerzéséhez. A partnerek ezt az oktatási ügyfelek ellenőrzésére használhatják.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 9f9b9aaddde0d66caf9c7ef32e8fba6d5e3aba36
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768645"
---
# <a name="get-a-customers-qualifications-via-asynchronous-validation"></a><span data-ttu-id="a4b54-104">Ügyfél képzettségének beszerzése aszinkron ellenőrzés útján</span><span class="sxs-lookup"><span data-stu-id="a4b54-104">Get a customer's qualifications via asynchronous validation</span></span>

<span data-ttu-id="a4b54-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="a4b54-105">**Applies To**</span></span>

- <span data-ttu-id="a4b54-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="a4b54-106">Partner Center</span></span>

<span data-ttu-id="a4b54-107">Megtudhatja, hogyan kérhet aszinkron módon ügyfél-képesítést a partner Center API-kon keresztül.</span><span class="sxs-lookup"><span data-stu-id="a4b54-107">Learn how to get a customer's qualifications asynchronously via Partner Center APIs.</span></span> <span data-ttu-id="a4b54-108">Ha szeretné megtudni, hogyan teheti meg ezt a szinkron módon, tekintse meg [az ügyfél minősítésének beszerzése szinkron ellenőrzés útján](get-customer-qualification-synchronous.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="a4b54-108">To learn how to do this synchronously, see [Get a customer's qualification via synchronous validation](get-customer-qualification-synchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4b54-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a4b54-109">Prerequisites</span></span>

- <span data-ttu-id="a4b54-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="a4b54-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a4b54-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="a4b54-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a4b54-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a4b54-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a4b54-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="a4b54-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a4b54-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="a4b54-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a4b54-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="a4b54-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a4b54-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="a4b54-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a4b54-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a4b54-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="a4b54-118">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="a4b54-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a4b54-119">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a4b54-119">Request syntax</span></span>

| <span data-ttu-id="a4b54-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="a4b54-120">Method</span></span>  | <span data-ttu-id="a4b54-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a4b54-121">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a4b54-122">**GET**</span><span class="sxs-lookup"><span data-stu-id="a4b54-122">**GET**</span></span> | <span data-ttu-id="a4b54-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="a4b54-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a4b54-124">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a4b54-124">URI parameter</span></span>

<span data-ttu-id="a4b54-125">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az összes minősítés beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="a4b54-125">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="a4b54-126">Név</span><span class="sxs-lookup"><span data-stu-id="a4b54-126">Name</span></span>               | <span data-ttu-id="a4b54-127">Típus</span><span class="sxs-lookup"><span data-stu-id="a4b54-127">Type</span></span>   | <span data-ttu-id="a4b54-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a4b54-128">Required</span></span> | <span data-ttu-id="a4b54-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="a4b54-129">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="a4b54-130">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="a4b54-130">**customer-tenant-id**</span></span> | <span data-ttu-id="a4b54-131">sztring</span><span class="sxs-lookup"><span data-stu-id="a4b54-131">string</span></span> | <span data-ttu-id="a4b54-132">Igen</span><span class="sxs-lookup"><span data-stu-id="a4b54-132">Yes</span></span>      | <span data-ttu-id="a4b54-133">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="a4b54-133">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a4b54-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a4b54-134">Request headers</span></span>

<span data-ttu-id="a4b54-135">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a4b54-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a4b54-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a4b54-136">Request body</span></span>

<span data-ttu-id="a4b54-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="a4b54-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a4b54-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a4b54-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="a4b54-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a4b54-139">REST response</span></span>

<span data-ttu-id="a4b54-140">Ha a művelet sikeres, ez a módszer képesítések gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="a4b54-140">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="a4b54-141">Az alábbi példák az **oktatási** végzettséggel rendelkező ügyfelekre vonatkozó **Get** hívásra vonatkoznak.</span><span class="sxs-lookup"><span data-stu-id="a4b54-141">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a4b54-142">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a4b54-142">Response success and error codes</span></span>

<span data-ttu-id="a4b54-143">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="a4b54-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a4b54-144">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="a4b54-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a4b54-145">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="a4b54-145">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="a4b54-146">Példák a válaszokra</span><span class="sxs-lookup"><span data-stu-id="a4b54-146">Response examples</span></span>

<span data-ttu-id="a4b54-147">Ez a szakasz azokat a válaszokat mutatja be, amelyeket az ügyfél a következő esetekben kaphat `vettingStatus` :</span><span class="sxs-lookup"><span data-stu-id="a4b54-147">This section shows responses you might receive when a customer's `vettingStatus` is:</span></span>

- <span data-ttu-id="a4b54-148">Approved</span><span class="sxs-lookup"><span data-stu-id="a4b54-148">Approved</span></span>
- <span data-ttu-id="a4b54-149">In Review (Felülvizsgálat alatt)</span><span class="sxs-lookup"><span data-stu-id="a4b54-149">In Review</span></span>
- <span data-ttu-id="a4b54-150">Megtagadva</span><span class="sxs-lookup"><span data-stu-id="a4b54-150">Denied</span></span>

<span data-ttu-id="a4b54-151">**Jóváhagyott** példa:</span><span class="sxs-lookup"><span data-stu-id="a4b54-151">**Approved** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Approved",
    }
]

```

<span data-ttu-id="a4b54-152">**A felülvizsgálati** példa:</span><span class="sxs-lookup"><span data-stu-id="a4b54-152">**In Review** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "InReview",
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

<span data-ttu-id="a4b54-153">**Elutasított** példa:</span><span class="sxs-lookup"><span data-stu-id="a4b54-153">**Denied** example:</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
[
    {
        "qualification": "Education",
        "vettingStatus": "Denied",
        "vettingReason": "Not an Education Customer", // example Vetting Reason
        "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="a4b54-154">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="a4b54-154">Related articles</span></span>

- [<span data-ttu-id="a4b54-155">Ügyfél képzettségének frissítése</span><span class="sxs-lookup"><span data-stu-id="a4b54-155">Update a customer's qualifications</span></span>](update-a-customer-s-qualifications.md)