---
title: Egy ügyfél végzettségének lekérése
description: Megtudhatja, hogyan használhatja a szinkron érvényesítést az ügyfél minősítésének az API-n keresztüli Partnerközpont le. A partnerek ezzel ellenőrizhetik az oktatási ügyfeleket.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d215ddb105efe3acd1182c4ff4bb25b045b121f0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446343"
---
# <a name="get-a-customers-qualification-via-synchronous-validation"></a><span data-ttu-id="a5394-104">Ügyfél minősítésének lekértsége szinkron ellenőrzéssel</span><span class="sxs-lookup"><span data-stu-id="a5394-104">Get a customer's qualification via synchronous validation</span></span>

<span data-ttu-id="a5394-105">Megtudhatja, hogyan szerezhető be az ügyfél minősítése szinkron módon az Partnerközpont API-kon keresztül.</span><span class="sxs-lookup"><span data-stu-id="a5394-105">Learn how to get a customer's qualification synchronously via Partner Center APIs.</span></span> <span data-ttu-id="a5394-106">Ennek aszinkron módon történő érvényre jutásról lásd: Ügyfél minősítésének lekértsége [aszinkron ellenőrzéssel.](get-customer-qualification-asynchronous.md)</span><span class="sxs-lookup"><span data-stu-id="a5394-106">To learn how to do this asynchronously, see [Get a customer's qualification via asynchronous validation](get-customer-qualification-asynchronous.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5394-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a5394-107">Prerequisites</span></span>

- <span data-ttu-id="a5394-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a5394-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a5394-109">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="a5394-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a5394-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a5394-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a5394-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a5394-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a5394-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a5394-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a5394-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a5394-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a5394-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="a5394-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a5394-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a5394-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="a5394-116">C\#</span><span class="sxs-lookup"><span data-stu-id="a5394-116">C\#</span></span>

<span data-ttu-id="a5394-117">Az ügyfél minősítésének megszerzéséhez hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="a5394-117">To get a customer's qualification, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="a5394-118">Ezután a [**Minősítés tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) használatával lekér egy [**ICustomerQualification felületet.**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification)</span><span class="sxs-lookup"><span data-stu-id="a5394-118">Then use the [**Qualification**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.qualification) property to retrieve a [**ICustomerQualification**](/dotnet/api/microsoft.store.partnercenter.qualification.icustomerqualification) interface.</span></span> <span data-ttu-id="a5394-119">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) vagy [**a GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) az ügyfél minősítésének lekérésére.</span><span class="sxs-lookup"><span data-stu-id="a5394-119">Finally, call [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) to retrieve the customer's qualification.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerQualification = partnerOperations.Customers.ById(customerId).Qualification.Get();
```

## <a name="rest-request"></a><span data-ttu-id="a5394-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="a5394-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a5394-121">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a5394-121">Request syntax</span></span>

| <span data-ttu-id="a5394-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="a5394-122">Method</span></span>  | <span data-ttu-id="a5394-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a5394-123">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a5394-124">**Kap**</span><span class="sxs-lookup"><span data-stu-id="a5394-124">**GET**</span></span> | <span data-ttu-id="a5394-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a5394-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/qualification HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a5394-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a5394-126">URI parameter</span></span>

<span data-ttu-id="a5394-127">Ez a táblázat felsorolja az összes minősítéshez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="a5394-127">This table lists the required query parameter to get all the qualification.</span></span>

| <span data-ttu-id="a5394-128">Név</span><span class="sxs-lookup"><span data-stu-id="a5394-128">Name</span></span>               | <span data-ttu-id="a5394-129">Típus</span><span class="sxs-lookup"><span data-stu-id="a5394-129">Type</span></span>   | <span data-ttu-id="a5394-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a5394-130">Required</span></span> | <span data-ttu-id="a5394-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="a5394-131">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="a5394-132">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="a5394-132">**customer-tenant-id**</span></span> | <span data-ttu-id="a5394-133">sztring</span><span class="sxs-lookup"><span data-stu-id="a5394-133">string</span></span> | <span data-ttu-id="a5394-134">Igen</span><span class="sxs-lookup"><span data-stu-id="a5394-134">Yes</span></span>      | <span data-ttu-id="a5394-135">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="a5394-135">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a5394-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a5394-136">Request headers</span></span>

<span data-ttu-id="a5394-137">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a5394-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a5394-138">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a5394-138">Request body</span></span>

<span data-ttu-id="a5394-139">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="a5394-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a5394-140">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a5394-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualification HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a><span data-ttu-id="a5394-141">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a5394-141">REST response</span></span>

<span data-ttu-id="a5394-142">Ha sikeres, ez a metódus egy minősítési értéket ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="a5394-142">If successful, this method returns a qualification value in the response body.</span></span>  <span data-ttu-id="a5394-143">Az alábbi példa egy **GET** hívást mutat be egy oktatási jogosultsággal **rendelkező ügyfélhez.**</span><span class="sxs-lookup"><span data-stu-id="a5394-143">Below is an example of the **GET** call on a customer with the **education** qualification.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a5394-144">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a5394-144">Response success and error codes</span></span>

<span data-ttu-id="a5394-145">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="a5394-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a5394-146">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="a5394-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a5394-147">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a5394-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a5394-148">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a5394-148">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

    "education"

```

## <a name="related-articles"></a><span data-ttu-id="a5394-149">Kapcsolódó cikkek</span><span class="sxs-lookup"><span data-stu-id="a5394-149">Related articles</span></span>

- [<span data-ttu-id="a5394-150">Ügyfél végzettségének frissítése</span><span class="sxs-lookup"><span data-stu-id="a5394-150">Update a customer's qualification</span></span>](./update-customer-qualification-synchronous.md)