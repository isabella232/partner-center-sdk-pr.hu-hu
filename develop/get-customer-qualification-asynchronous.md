---
title: Ügyfél minősítésének lekértsége
description: Megtudhatja, hogyan használhatja az aszinkron érvényesítést az ügyfél minősítésének az API-n keresztüli Partnerközpont le. A partnerek ezzel ellenőrizhetik az oktatási ügyfeleket.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: df605e4d400d29e14fd0b44bef34f88bbc7ca8b2
ms.sourcegitcommit: 7d59c58ee36b217bd5cac089f918059e9dbb8a62
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2021
ms.locfileid: "110027928"
---
# <a name="get-a-customers-qualification-asynchronously"></a><span data-ttu-id="245c5-104">Ügyfél minősítésének aszinkron lekértsége</span><span class="sxs-lookup"><span data-stu-id="245c5-104">Get a customer's qualification asynchronously</span></span>

<span data-ttu-id="245c5-105">**A következőre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="245c5-105">**Applies To**</span></span>

- <span data-ttu-id="245c5-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="245c5-106">Partner Center</span></span>

<span data-ttu-id="245c5-107">Hogyan lehet aszinkron módon szerezni az ügyfelek minősítését.</span><span class="sxs-lookup"><span data-stu-id="245c5-107">How to get a customer's qualifications asynchronously.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="245c5-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="245c5-108">Prerequisites</span></span>

- <span data-ttu-id="245c5-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="245c5-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="245c5-110">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="245c5-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="245c5-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="245c5-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="245c5-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="245c5-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="245c5-113">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="245c5-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="245c5-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="245c5-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="245c5-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="245c5-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="245c5-116">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="245c5-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="245c5-117">C\#</span><span class="sxs-lookup"><span data-stu-id="245c5-117">C\#</span></span>

<span data-ttu-id="245c5-118">Az ügyfél minősítésének megszerzéséhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="245c5-118">To get a customer's qualifications, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="245c5-119">Ezután a [**Minősítés tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) használatával lekér egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felületet.</span><span class="sxs-lookup"><span data-stu-id="245c5-119">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="245c5-120">Végül hívja meg a vagy a et az `GetQualifications()` ügyfél `GetQualificationsAsync()` minősítésének lekérésére.</span><span class="sxs-lookup"><span data-stu-id="245c5-120">Finally, call `GetQualifications()` or `GetQualificationsAsync()` to retrieve the customer's qualifications.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerQualifications = partnerOperations.Customers.ById(customerId).Qualification.GetQualifications();
```

<span data-ttu-id="245c5-121">**Minta:** [Konzol mintaalkalmazás.](https://github.com/microsoft/Partner-Center-DotNet-Samples)</span><span class="sxs-lookup"><span data-stu-id="245c5-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="245c5-122">**Projekt:** SdkSamples **osztály:** GetCustomerQualifications.cs</span><span class="sxs-lookup"><span data-stu-id="245c5-122">**Project**: SdkSamples **Class**: GetCustomerQualifications.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="245c5-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="245c5-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="245c5-124">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="245c5-124">Request syntax</span></span>

| <span data-ttu-id="245c5-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="245c5-125">Method</span></span>  | <span data-ttu-id="245c5-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="245c5-126">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="245c5-127">**Kap**</span><span class="sxs-lookup"><span data-stu-id="245c5-127">**GET**</span></span> | <span data-ttu-id="245c5-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="245c5-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualifications HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="245c5-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="245c5-129">URI parameter</span></span>

<span data-ttu-id="245c5-130">Ez a táblázat felsorolja az összes minősítéshez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="245c5-130">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="245c5-131">Név</span><span class="sxs-lookup"><span data-stu-id="245c5-131">Name</span></span>               | <span data-ttu-id="245c5-132">Típus</span><span class="sxs-lookup"><span data-stu-id="245c5-132">Type</span></span>   | <span data-ttu-id="245c5-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="245c5-133">Required</span></span> | <span data-ttu-id="245c5-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="245c5-134">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="245c5-135">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="245c5-135">**customer-tenant-id**</span></span> | <span data-ttu-id="245c5-136">sztring</span><span class="sxs-lookup"><span data-stu-id="245c5-136">string</span></span> | <span data-ttu-id="245c5-137">Yes</span><span class="sxs-lookup"><span data-stu-id="245c5-137">Yes</span></span>      | <span data-ttu-id="245c5-138">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="245c5-138">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="245c5-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="245c5-139">Request headers</span></span>

<span data-ttu-id="245c5-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="245c5-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="245c5-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="245c5-141">Request body</span></span>

<span data-ttu-id="245c5-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="245c5-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="245c5-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="245c5-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="245c5-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="245c5-144">REST response</span></span>

<span data-ttu-id="245c5-145">Ha ez a módszer sikeres, a válasz törzsében minősítések gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="245c5-145">If successful, this method returns a collection of qualifications in the response body.</span></span>  <span data-ttu-id="245c5-146">Az alábbiakban példákat talál az Oktatási minősítéssel rendelkező ügyfelek **GET** **hívására.**</span><span class="sxs-lookup"><span data-stu-id="245c5-146">Below are examples of the **GET** call on a customer with the **Education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="245c5-147">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="245c5-147">Response success and error codes</span></span>

<span data-ttu-id="245c5-148">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="245c5-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="245c5-149">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="245c5-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="245c5-150">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="245c5-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-examples"></a><span data-ttu-id="245c5-151">Példák válaszra</span><span class="sxs-lookup"><span data-stu-id="245c5-151">Response examples</span></span>

#### <a name="approved"></a><span data-ttu-id="245c5-152">Approved</span><span class="sxs-lookup"><span data-stu-id="245c5-152">Approved</span></span>

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

#### <a name="in-review"></a><span data-ttu-id="245c5-153">In Review (Felülvizsgálat alatt)</span><span class="sxs-lookup"><span data-stu-id="245c5-153">In Review</span></span>

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

#### <a name="denied"></a><span data-ttu-id="245c5-154">Megtagadva</span><span class="sxs-lookup"><span data-stu-id="245c5-154">Denied</span></span>

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

#### <a name="state-owned-entity-samples"></a><span data-ttu-id="245c5-155">Állam tulajdonú entitások mintái</span><span class="sxs-lookup"><span data-stu-id="245c5-155">State Owned Entity Samples</span></span>

<span data-ttu-id="245c5-156">**Állam tulajdonú entitás POST-mintán keresztül**</span><span class="sxs-lookup"><span data-stu-id="245c5-156">**State Owned Entity via POST sample**</span></span>

```csharp

//SOE
POST {customer_id}/qualifications
{
“qualification”: “StateOwnedEntity”
}

//

```

<span data-ttu-id="245c5-157">**State Owned Entity via Get Qualifications sample**</span><span class="sxs-lookup"><span data-stu-id="245c5-157">**State Owned Entity via Get Qualifications sample**</span></span>

```csharp

//SOE:
GET {customer_id}/qualifications
[
    {
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="245c5-158">**State Owned Entity via Get Qualifications with Education**</span><span class="sxs-lookup"><span data-stu-id="245c5-158">**State Owned Entity via Get Qualifications with Education**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “Education”,
        “vettingStatus”: “Approved”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

<span data-ttu-id="245c5-159">**State Owned Entity via Get Qualifications with GCC**</span><span class="sxs-lookup"><span data-stu-id="245c5-159">**State Owned Entity via Get Qualifications with GCC**</span></span>

```csharp

GET {customer_id}/qualifications
[
    {
        “qualification”: “GovernmentCommunityCloud”,
        “vettingStatus”: “Approved”,
        “vettingCreateDate”: “2021-05-06T19:59:56.6832021+00:00”
    },
{
        “qualification”: “StateOwnedEntity”
    }
]

```

## <a name="related-articles"></a><span data-ttu-id="245c5-160">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="245c5-160">Related articles</span></span>

- [<span data-ttu-id="245c5-161">Ügyfél végzettségének frissítése</span><span class="sxs-lookup"><span data-stu-id="245c5-161">Update a customer's qualifications</span></span>](./update-customer-qualification-asynchronous.md)
