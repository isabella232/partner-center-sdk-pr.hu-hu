---
title: Egy előfizetés lekérése azonosító alapján
description: Lekéri az ügyfél-AZONOSÍTÓval és az előfizetés-AZONOSÍTÓval megegyező előfizetési erőforrást.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6690a6886eeb31a78cdb556280d4bdc2b4beb124
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768292"
---
# <a name="get-a-subscription-by-id"></a><span data-ttu-id="d7f89-103">Egy előfizetés lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="d7f89-103">Get a subscription by ID</span></span>

<span data-ttu-id="d7f89-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="d7f89-104">**Applies To**</span></span>

- <span data-ttu-id="d7f89-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d7f89-105">Partner Center</span></span>
- <span data-ttu-id="d7f89-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="d7f89-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d7f89-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d7f89-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d7f89-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d7f89-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d7f89-109">Lekéri az ügyfél-AZONOSÍTÓval és az előfizetés-AZONOSÍTÓval megegyező [előfizetési](subscription-resources.md) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="d7f89-109">Gets a [Subscription](subscription-resources.md) resource that matches the customer ID and the subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7f89-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d7f89-110">Prerequisites</span></span>

- <span data-ttu-id="d7f89-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="d7f89-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d7f89-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="d7f89-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d7f89-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d7f89-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d7f89-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d7f89-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d7f89-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="d7f89-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d7f89-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="d7f89-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d7f89-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="d7f89-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d7f89-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d7f89-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d7f89-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="d7f89-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="d7f89-120">C\#</span><span class="sxs-lookup"><span data-stu-id="d7f89-120">C\#</span></span>

<span data-ttu-id="d7f89-121">Ha azonosító alapján szeretne előfizetést beszerezni, először egy illesztőfelületet kell beszereznie az előfizetési műveletekhez úgy, hogy meghívja a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához, valamint az [**előfizetések. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust az előfizetés azonosításához.</span><span class="sxs-lookup"><span data-stu-id="d7f89-121">To get a subscription by ID, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription.</span></span> <span data-ttu-id="d7f89-122">Ezzel a [**csatolóval**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) kérheti le az előfizetés részleteit a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)utasítás meghívásával.</span><span class="sxs-lookup"><span data-stu-id="d7f89-122">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionID;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionID).Get();
```

<span data-ttu-id="d7f89-123">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d7f89-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d7f89-124">**Projekt**: partner Center SDK Samples **osztály**: GetSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="d7f89-124">**Project**: Partner Center SDK Samples **Class**: GetSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d7f89-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="d7f89-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d7f89-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d7f89-126">Request syntax</span></span>

| <span data-ttu-id="d7f89-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="d7f89-127">Method</span></span>  | <span data-ttu-id="d7f89-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d7f89-128">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d7f89-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="d7f89-129">**GET**</span></span> | <span data-ttu-id="d7f89-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d7f89-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d7f89-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d7f89-131">URI parameter</span></span>

<span data-ttu-id="d7f89-132">Ez a táblázat felsorolja az előfizetés beszerzéséhez szükséges lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="d7f89-132">This table lists the required query parameters to get the subscription.</span></span>

| <span data-ttu-id="d7f89-133">Név</span><span class="sxs-lookup"><span data-stu-id="d7f89-133">Name</span></span>                    | <span data-ttu-id="d7f89-134">Típus</span><span class="sxs-lookup"><span data-stu-id="d7f89-134">Type</span></span>     | <span data-ttu-id="d7f89-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d7f89-135">Required</span></span> | <span data-ttu-id="d7f89-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="d7f89-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="d7f89-137">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="d7f89-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="d7f89-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="d7f89-138">**guid**</span></span> | <span data-ttu-id="d7f89-139">Y</span><span class="sxs-lookup"><span data-stu-id="d7f89-139">Y</span></span>        | <span data-ttu-id="d7f89-140">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="d7f89-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="d7f89-141">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="d7f89-141">**id-for-subscription**</span></span> | <span data-ttu-id="d7f89-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="d7f89-142">**guid**</span></span> | <span data-ttu-id="d7f89-143">Y</span><span class="sxs-lookup"><span data-stu-id="d7f89-143">Y</span></span>        | <span data-ttu-id="d7f89-144">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="d7f89-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d7f89-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d7f89-145">Request headers</span></span>

<span data-ttu-id="d7f89-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d7f89-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d7f89-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d7f89-147">Request body</span></span>

<span data-ttu-id="d7f89-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d7f89-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d7f89-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d7f89-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d7f89-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d7f89-150">REST response</span></span>

<span data-ttu-id="d7f89-151">Ha ez sikeres, ez a metódus egy [előfizetési](subscription-resources.md) erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="d7f89-151">If successful, this method returns a [Subscription](subscription-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d7f89-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d7f89-152">Response success and error codes</span></span>

<span data-ttu-id="d7f89-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="d7f89-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d7f89-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="d7f89-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d7f89-155">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="d7f89-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-a-standard-subscription"></a><span data-ttu-id="d7f89-156">Példa a standard előfizetésre</span><span class="sxs-lookup"><span data-stu-id="d7f89-156">Response example for a standard subscription</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 833
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CV: 7v11Wa//5EuGEo+A.0
MS-ServerId: 202010406
Date: Fri, 27 Jan 2017 21:51:40 GMT

{
    "id": "A356AC8C-E310-44F4-BF85-C7F29044AF99",
    "entitlementId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
    "offerId": "MS-AZR-0145P",
    "offerName": "Microsoft Azure",
    "friendlyName": "Microsoft Azure",
    "quantity": 1,
    "unitType": "Usage-based",
    "creationDate": "2016-05-10T07:30:05.427Z",
    "effectiveStartDate": "2016-05-10T00:00:00Z",
    "commitmentEndDate": "9999-12-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": false,
    "billingType": "usage",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/MS-AZR-0145P?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/A356AC8C-E310-44F4-BF85-C7F29044AF99",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "B23FDEDD-D6BD-415A-8B71-3624C81C9644",
    "attributes": {
        "etag": "eyJpZCI6ImEzNTZhYzhjLWUzMTAtNDRmNC1iZjg1LWM3ZjI5MDQ0YWY5OSIsInZlcnNpb24iOjJ9",
        "objectType": "Subscription"
    }
}
```

### <a name="response-example-for-an-add-on-subscription"></a><span data-ttu-id="d7f89-157">Példa kiegészítő előfizetésre</span><span class="sxs-lookup"><span data-stu-id="d7f89-157">Response example for an add-on subscription</span></span>

<span data-ttu-id="d7f89-158">A bővítmény előfizetésre adott válasz tartalmazza a szülő előfizetés AZONOSÍTÓját a törzsben és a hivatkozásokban.</span><span class="sxs-lookup"><span data-stu-id="d7f89-158">The response for an add-on subscription includes the parent subscription ID in the body and in the links.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1132
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6eacec93-852d-4167-9d96-c57809bea7ed
MS-RequestId: 22bfd0fb-d1e6-4a8f-aa1a-124b7c820d80
MS-CV: cmde2DtbuUWi8JLq.0
MS-ServerId: 201022015
Date: Fri, 27 Jan 2017 00:12:53 GMT

{
    "id": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
    "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
    "offerName": "Exchange Online Archiving for Exchange Online",
    "friendlyName": "Some friendly name",
    "quantity": 2,
    "unitType": "Licenses",
    "parentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
    "creationDate": "2017-01-25T23:01:08.693Z",
    "effectiveStartDate": "2017-01-25T00:00:00Z",
    "commitmentEndDate": "2018-02-10T00:00:00Z",
    "status": "active",
    "autoRenewEnabled": true,
    "billingType": "license",
    "contractType": "subscription",
    "links": {
        "offer": {
            "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
            "method": "GET",
            "headers": []
        },
        "parentSubscription": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "method": "GET",
            "headers": []
        }
    },
    "orderId": "CF3B0E37-BE0B-4CDD-B584-D1A97D98A922",
    "attributes": {
        "etag": "eyJpZCI6Ijk2OGJhMWNmLWMxNDYtNGFkZi1hMzAwLTMwOGRjZjcxOGVlZSIsInZlcnNpb24iOjF9",
        "objectType": "Subscription"
    }
}
```
