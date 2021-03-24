---
title: Ügyfél képzettségének beszerzése
description: Megtudhatja, hogyan használhatja az aszinkron érvényesítést az ügyfél a partner Center API-n keresztüli minősítésének beszerzéséhez. A partnerek ezt az oktatási ügyfelek ellenőrzésére használhatják.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 09801792c059873b9f6b842e99286eda09d38b1a
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030567"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="47f8f-104">Ügyfél-képesítés aszinkron beszerzése</span><span class="sxs-lookup"><span data-stu-id="47f8f-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="47f8f-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="47f8f-105">**Applies To**</span></span>

- <span data-ttu-id="47f8f-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="47f8f-106">Partner Center</span></span>

<span data-ttu-id="47f8f-107">Az ügyfél képzettségének aszinkron beszerzése.</span><span class="sxs-lookup"><span data-stu-id="47f8f-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47f8f-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="47f8f-108">Prerequisites</span></span>

- <span data-ttu-id="47f8f-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="47f8f-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="47f8f-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="47f8f-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="47f8f-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="47f8f-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="47f8f-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="47f8f-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="47f8f-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="47f8f-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="47f8f-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="47f8f-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="47f8f-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="47f8f-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="47f8f-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="47f8f-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="47f8f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="47f8f-117">C\#</span></span>

<span data-ttu-id="47f8f-118">Az ügyfél képzettségének beszerzéséhez hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="47f8f-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="47f8f-119">Ezután használja a [**minősítés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) tulajdonságot egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felület lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="47f8f-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="47f8f-120">Végül hívja `GetQualifications()` meg vagy kérje `GetQualificationsAsync()` le az ügyfél képzettségét.</span><span class="sxs-lookup"><span data-stu-id="47f8f-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="47f8f-121">**Példa**: [konzolos minta alkalmazás](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="47f8f-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="47f8f-122">**Projekt**: SdkSamples **osztály**: GetCustomerQualifications. cs</span><span class="sxs-lookup"><span data-stu-id="47f8f-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="47f8f-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="47f8f-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="47f8f-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="47f8f-124">Request syntax</span></span>

| <span data-ttu-id="47f8f-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="47f8f-125">Method</span></span>  | <span data-ttu-id="47f8f-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="47f8f-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="47f8f-127">**GET**</span><span class="sxs-lookup"><span data-stu-id="47f8f-127">**GET**</span></span> | <span data-ttu-id="47f8f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1</span><span class="sxs-lookup"><span data-stu-id="47f8f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="47f8f-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="47f8f-129">URI parameter</span></span>

<span data-ttu-id="47f8f-130">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az összes minősítés beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="47f8f-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="47f8f-131">Név</span><span class="sxs-lookup"><span data-stu-id="47f8f-131">Name</span></span>               | <span data-ttu-id="47f8f-132">Típus</span><span class="sxs-lookup"><span data-stu-id="47f8f-132">Type</span></span>   | <span data-ttu-id="47f8f-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="47f8f-133">Required</span></span> | <span data-ttu-id="47f8f-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="47f8f-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="47f8f-135">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="47f8f-135">**customer-tenant-id**</span></span> | <span data-ttu-id="47f8f-136">sztring</span><span class="sxs-lookup"><span data-stu-id="47f8f-136">string</span></span> | <span data-ttu-id="47f8f-137">Igen</span><span class="sxs-lookup"><span data-stu-id="47f8f-137">Yes</span></span>      | <span data-ttu-id="47f8f-138">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="47f8f-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="47f8f-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="47f8f-139">Request headers</span></span>

<span data-ttu-id="47f8f-140">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="47f8f-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="47f8f-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="47f8f-141">Request body</span></span>

<span data-ttu-id="47f8f-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="47f8f-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="47f8f-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="47f8f-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="47f8f-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="47f8f-144">REST response</span></span>

<span data-ttu-id="47f8f-145">Ha a művelet sikeres, ez a módszer képesítések gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="47f8f-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="47f8f-146">Az alábbi példák az **oktatási** végzettséggel rendelkező ügyfelekre vonatkozó **Get** hívásra vonatkoznak.</span><span class="sxs-lookup"><span data-stu-id="47f8f-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="47f8f-147">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="47f8f-147">Response success and error codes</span></span>

<span data-ttu-id="47f8f-148">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="47f8f-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="47f8f-149">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="47f8f-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="47f8f-150">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="47f8f-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="47f8f-151">Példák a válaszokra</span><span class="sxs-lookup"><span data-stu-id="47f8f-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="47f8f-152">Approved</span><span class="sxs-lookup"><span data-stu-id="47f8f-152">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="47f8f-153">In Review (Felülvizsgálat alatt)</span><span class="sxs-lookup"><span data-stu-id="47f8f-153">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="47f8f-154">Megtagadva</span><span class="sxs-lookup"><span data-stu-id="47f8f-154">Denied</span></span>

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

## <a name="related-articles"></a><span data-ttu-id="47f8f-155">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="47f8f-155">Related articles</span></span>

- [<span data-ttu-id="47f8f-156">Ügyfél végzettségének frissítése</span><span class="sxs-lookup"><span data-stu-id="47f8f-156">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
