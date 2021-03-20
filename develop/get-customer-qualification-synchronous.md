---
title: Egy ügyfél végzettségének lekérése
description: Megtudhatja, hogyan használhatja a szinkron érvényesítést az ügyfél a partner Center API-n keresztüli minősítésének beszerzéséhez. A partnerek ezt az oktatási ügyfelek ellenőrzésére használhatják.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e39ace3b598736abed6ab22021a8b93d473486a3
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711885"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="37468-104">Az ügyfél minősítésének beszerzése szinkron ellenőrzés útján</span><span class="sxs-lookup"><span data-stu-id="37468-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="37468-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="37468-105">**Applies To**</span></span>

- <span data-ttu-id="37468-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="37468-106">Partner Center</span></span>

<span data-ttu-id="37468-107">Megtudhatja, hogyan lehet a partner Center API-kon keresztül szinkronban megszerezni az ügyfél képzettségét.</span><span class="sxs-lookup"><span data-stu-id="37468-107">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="37468-108">Ha szeretné megtudni, hogyan teheti meg ezt aszinkron módon, tekintse meg az [ügyfél minősítésének beszerzése aszinkron ellenőrzésen keresztül](get-customer-qualification-asynchronous.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="37468-108">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37468-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="37468-109">Prerequisites</span></span>

- <span data-ttu-id="37468-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="37468-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="37468-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="37468-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="37468-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="37468-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="37468-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="37468-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="37468-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="37468-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="37468-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="37468-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="37468-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="37468-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="37468-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="37468-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="37468-118">C\#</span><span class="sxs-lookup"><span data-stu-id="37468-118">C\#</span></span>

<span data-ttu-id="37468-119">Az ügyfél minősítésének beszerzéséhez hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="37468-119">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="37468-120">Ezután használja a [**minősítés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) tulajdonságot egy [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) felület lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="37468-120">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="37468-121">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) az ügyfél minősítésének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="37468-121">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="37468-122">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="37468-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="37468-123">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="37468-123">Request syntax</span></span>

| <span data-ttu-id="37468-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="37468-124">Method</span></span>  | <span data-ttu-id="37468-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="37468-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="37468-126">**GET**</span><span class="sxs-lookup"><span data-stu-id="37468-126">**GET**</span></span> | <span data-ttu-id="37468-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualification http/1.1</span><span class="sxs-lookup"><span data-stu-id="37468-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="37468-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="37468-128">URI parameter</span></span>

<span data-ttu-id="37468-129">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az összes minősítés beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="37468-129">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="37468-130">Név</span><span class="sxs-lookup"><span data-stu-id="37468-130">Name</span></span>               | <span data-ttu-id="37468-131">Típus</span><span class="sxs-lookup"><span data-stu-id="37468-131">Type</span></span>   | <span data-ttu-id="37468-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="37468-132">Required</span></span> | <span data-ttu-id="37468-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="37468-133">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="37468-134">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="37468-134">**customer-tenant-id**</span></span> | <span data-ttu-id="37468-135">sztring</span><span class="sxs-lookup"><span data-stu-id="37468-135">string</span></span> | <span data-ttu-id="37468-136">Yes</span><span class="sxs-lookup"><span data-stu-id="37468-136">Yes</span></span>      | <span data-ttu-id="37468-137">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="37468-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="37468-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="37468-138">Request headers</span></span>

<span data-ttu-id="37468-139">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="37468-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="37468-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="37468-140">Request body</span></span>

<span data-ttu-id="37468-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="37468-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="37468-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="37468-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="37468-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="37468-143">REST response</span></span>

<span data-ttu-id="37468-144">Ha ez sikeres, ez a metódus egy minősítési értéket ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="37468-144">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="37468-145">Alább látható egy példa arra, **hogy az ügyfél az** **oktatási** végzettséggel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="37468-145">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="37468-146">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="37468-146">Response success and error codes</span></span>

<span data-ttu-id="37468-147">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="37468-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="37468-148">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="37468-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="37468-149">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="37468-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="37468-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="37468-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="37468-151">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="37468-151">Related articles</span></span>

- [<span data-ttu-id="37468-152">Ügyfél végzettségének frissítése</span><span class="sxs-lookup"><span data-stu-id="37468-152">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)