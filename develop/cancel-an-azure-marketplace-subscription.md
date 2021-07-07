---
title: Kereskedelmi piactéri előfizetés lemondása
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat kereskedelmi piactéri előfizetés erőforrásának lemondásához, amely megfelel egy ügyfélnek és egy előfizetés-azonosítónak.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 95fa265a3c103d1ec55066f12a3ede7fdb2d0170
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974284"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="1ee16-103">Kereskedelmi piactér-előfizetés lemondása Partnerközpont API-k használatával</span><span class="sxs-lookup"><span data-stu-id="1ee16-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="1ee16-104">Ez a cikk azt ismerteti, hogyan használhatja a [](subscription-resources.md) Partnerközpont API-t egy kereskedelmi piactéri előfizetés erőforrásának lemondására, amely megfelel az ügyfél és az előfizetés azonosítójának.</span><span class="sxs-lookup"><span data-stu-id="1ee16-104">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ee16-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1ee16-105">Prerequisites</span></span>

- <span data-ttu-id="1ee16-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1ee16-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ee16-107">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="1ee16-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1ee16-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ee16-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1ee16-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1ee16-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1ee16-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1ee16-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1ee16-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1ee16-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1ee16-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="1ee16-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1ee16-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ee16-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1ee16-114">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="1ee16-114">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="1ee16-115">Partnerközpont irányítópult metódusa</span><span class="sxs-lookup"><span data-stu-id="1ee16-115">Partner Center dashboard method</span></span>

<span data-ttu-id="1ee16-116">Kereskedelmi piactér-előfizetés lemondása az Partnerközpont irányítópulton:</span><span class="sxs-lookup"><span data-stu-id="1ee16-116">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="1ee16-117">[Válasszon ki egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="1ee16-117">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="1ee16-118">Válassza ki a megszüntetni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="1ee16-118">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="1ee16-119">Válassza az **Előfizetés lemondása** lehetőséget, majd válassza a **Küldés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="1ee16-119">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="1ee16-120">C\#</span><span class="sxs-lookup"><span data-stu-id="1ee16-120">C\#</span></span>

<span data-ttu-id="1ee16-121">Ügyfél előfizetésének lemondása:</span><span class="sxs-lookup"><span data-stu-id="1ee16-121">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="1ee16-122">[Szerezze be az előfizetést azonosító alapján.](get-a-subscription-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="1ee16-122">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="1ee16-123">Módosítsa az előfizetés [**Status (Állapot) tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)</span><span class="sxs-lookup"><span data-stu-id="1ee16-123">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="1ee16-124">Az **állapotkódokkal kapcsolatos információkért** [lásd: SubscriptionStatus enumerálás.](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="1ee16-124">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="1ee16-125">A módosítás után használja a gyűjteményt, **`IAggregatePartner.Customers`** és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="1ee16-125">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="1ee16-126">Hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="1ee16-126">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="1ee16-127">Hívja meg **a Patch() metódust.**</span><span class="sxs-lookup"><span data-stu-id="1ee16-127">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="1ee16-128">Mintakonzol-tesztalkalmazás</span><span class="sxs-lookup"><span data-stu-id="1ee16-128">Sample console test app</span></span>

<span data-ttu-id="1ee16-129">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1ee16-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1ee16-130">**Project**: PartnerSDK.FeatureSample **osztály:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="1ee16-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1ee16-131">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="1ee16-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1ee16-132">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1ee16-132">Request syntax</span></span>

| <span data-ttu-id="1ee16-133">Metódus</span><span class="sxs-lookup"><span data-stu-id="1ee16-133">Method</span></span>    | <span data-ttu-id="1ee16-134">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1ee16-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ee16-135">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="1ee16-135">**PATCH**</span></span> | <span data-ttu-id="1ee16-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1ee16-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1ee16-137">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="1ee16-137">URI parameter</span></span>

<span data-ttu-id="1ee16-138">Ez a táblázat felsorolja az előfizetés felfüggesztéséhez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="1ee16-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="1ee16-139">Név</span><span class="sxs-lookup"><span data-stu-id="1ee16-139">Name</span></span>                    | <span data-ttu-id="1ee16-140">Típus</span><span class="sxs-lookup"><span data-stu-id="1ee16-140">Type</span></span>     | <span data-ttu-id="1ee16-141">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1ee16-141">Required</span></span> | <span data-ttu-id="1ee16-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="1ee16-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="1ee16-143">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="1ee16-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="1ee16-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="1ee16-144">**guid**</span></span> | <span data-ttu-id="1ee16-145">Y</span><span class="sxs-lookup"><span data-stu-id="1ee16-145">Y</span></span>        | <span data-ttu-id="1ee16-146">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="1ee16-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="1ee16-147">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="1ee16-147">**id-for-subscription**</span></span> | <span data-ttu-id="1ee16-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="1ee16-148">**guid**</span></span> | <span data-ttu-id="1ee16-149">Y</span><span class="sxs-lookup"><span data-stu-id="1ee16-149">Y</span></span>        | <span data-ttu-id="1ee16-150">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="1ee16-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1ee16-151">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="1ee16-151">Request headers</span></span>

<span data-ttu-id="1ee16-152">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1ee16-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1ee16-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1ee16-153">Request body</span></span>

<span data-ttu-id="1ee16-154">A kérelem **törzsében** teljes előfizetési erőforrásra van szükség.</span><span class="sxs-lookup"><span data-stu-id="1ee16-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="1ee16-155">Győződjön meg **arról, hogy** az Állapot tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="1ee16-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="1ee16-156">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1ee16-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [{
        "type": "Full",
        "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
    }],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "publisherName": "publisher Name",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {"objectType": "Subscription"},
}
```

## <a name="rest-response"></a><span data-ttu-id="1ee16-157">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1ee16-157">REST response</span></span>

<span data-ttu-id="1ee16-158">Ha ez a módszer sikeres, a törölt [előfizetés](subscription-resources.md) erőforrás-tulajdonságait adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="1ee16-158">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1ee16-159">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1ee16-159">Response success and error codes</span></span>

<span data-ttu-id="1ee16-160">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="1ee16-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1ee16-161">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="1ee16-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1ee16-162">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1ee16-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1ee16-163">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1ee16-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1322
Content-Type: application/json; charset=utf-8
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
X-Locale: en-US

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [
        {
            "type": "Full",
            "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
        }
    ],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "links": {
        "product": {
            "uri": "/products/DZH318Z0BXWC?country=US",
            "method": "GET",
            "headers": []
        },
        "sku": {
            "uri": "/products/DZH318Z0BXWC/skus/0001?country=US",
            "method": "GET",
            "headers": []
        },
        "availability": {
            "uri": "/products/DZH318Z0BXWC/skus/0001/availabilities/DZH318Z0BMJX?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/5921f00a-32c0-4457-aaa1-e8018c650895/subscriptions/6e7aa601-629e-461b-8933-0898c3cc3c7c",
            "method": "GET",
            "headers": []
        }
    },
    "publisherName": "publishe rName",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {
        "etag": "",
        "objectType": "Subscription"
    }
}
```
