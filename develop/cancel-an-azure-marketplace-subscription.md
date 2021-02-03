---
title: Kereskedelmi piactéri előfizetés lemondása
description: Ismerje meg, hogy a partner Center API-k használatával hogyan vonhatja vissza a kereskedelmi piactér előfizetési erőforrásait, amely megfelel az ügyfél és az előfizetés AZONOSÍTÓjának.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38708c17b31e39a5e7c436e0d76b4ebabbc3a801
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768592"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="b3c7f-103">Kereskedelmi piactér-előfizetés megszakítása a partner Center API-kkal</span><span class="sxs-lookup"><span data-stu-id="b3c7f-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="b3c7f-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="b3c7f-104">**Applies to:**</span></span>

- <span data-ttu-id="b3c7f-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b3c7f-105">Partner Center</span></span>

<span data-ttu-id="b3c7f-106">Ez a cikk azt ismerteti, hogyan lehet a partner Center API használatával lemondani egy olyan kereskedelmi piactér- [előfizetési](subscription-resources.md) erőforrást, amely megfelel az ügyfél-és előfizetés-azonosítónak.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-106">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3c7f-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b3c7f-107">Prerequisites</span></span>

- <span data-ttu-id="b3c7f-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b3c7f-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b3c7f-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b3c7f-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b3c7f-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b3c7f-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b3c7f-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b3c7f-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b3c7f-116">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-116">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="b3c7f-117">A partner Center irányítópultjának metódusa</span><span class="sxs-lookup"><span data-stu-id="b3c7f-117">Partner Center dashboard method</span></span>

<span data-ttu-id="b3c7f-118">Kereskedelmi piactér-előfizetés megszakítása a partner Center irányítópultján:</span><span class="sxs-lookup"><span data-stu-id="b3c7f-118">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="b3c7f-119">[Válasszon ki egy ügyfelet](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-119">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="b3c7f-120">Válassza ki a megszüntetni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-120">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="b3c7f-121">Válassza az **előfizetés megszakítása** lehetőséget, majd kattintson a **Küldés** elemre.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-121">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="b3c7f-122">C\#</span><span class="sxs-lookup"><span data-stu-id="b3c7f-122">C\#</span></span>

<span data-ttu-id="b3c7f-123">Ügyfél előfizetésének megszakítása:</span><span class="sxs-lookup"><span data-stu-id="b3c7f-123">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="b3c7f-124">[Az előfizetés beszerzése azonosító alapján](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-124">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="b3c7f-125">Módosítsa az előfizetés [**status (állapot**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) ) tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-125">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="b3c7f-126">Az **állapotkódok** információit lásd: [SubscriptionStatus enumerálása](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-126">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="b3c7f-127">A módosítás után használja a **`IAggregatePartner.Customers`** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-127">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="b3c7f-128">Hívja meg az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-128">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="b3c7f-129">Hívja meg a **Patch ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-129">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="b3c7f-130">Minta-konzol tesztelési alkalmazás</span><span class="sxs-lookup"><span data-stu-id="b3c7f-130">Sample console test app</span></span>

<span data-ttu-id="b3c7f-131">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b3c7f-132">**Projekt**: PartnerSDK. FeatureSample **osztály**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="b3c7f-132">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b3c7f-133">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b3c7f-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b3c7f-134">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b3c7f-134">Request syntax</span></span>

| <span data-ttu-id="b3c7f-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="b3c7f-135">Method</span></span>    | <span data-ttu-id="b3c7f-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b3c7f-136">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b3c7f-137">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="b3c7f-137">**PATCH**</span></span> | <span data-ttu-id="b3c7f-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b3c7f-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b3c7f-139">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b3c7f-139">URI parameter</span></span>

<span data-ttu-id="b3c7f-140">Ez a táblázat felsorolja az előfizetés felfüggesztéséhez szükséges lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-140">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="b3c7f-141">Név</span><span class="sxs-lookup"><span data-stu-id="b3c7f-141">Name</span></span>                    | <span data-ttu-id="b3c7f-142">Típus</span><span class="sxs-lookup"><span data-stu-id="b3c7f-142">Type</span></span>     | <span data-ttu-id="b3c7f-143">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b3c7f-143">Required</span></span> | <span data-ttu-id="b3c7f-144">Leírás</span><span class="sxs-lookup"><span data-stu-id="b3c7f-144">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="b3c7f-145">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="b3c7f-145">**customer-tenant-id**</span></span>  | <span data-ttu-id="b3c7f-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="b3c7f-146">**guid**</span></span> | <span data-ttu-id="b3c7f-147">Y</span><span class="sxs-lookup"><span data-stu-id="b3c7f-147">Y</span></span>        | <span data-ttu-id="b3c7f-148">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="b3c7f-149">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="b3c7f-149">**id-for-subscription**</span></span> | <span data-ttu-id="b3c7f-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="b3c7f-150">**guid**</span></span> | <span data-ttu-id="b3c7f-151">Y</span><span class="sxs-lookup"><span data-stu-id="b3c7f-151">Y</span></span>        | <span data-ttu-id="b3c7f-152">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-152">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b3c7f-153">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b3c7f-153">Request headers</span></span>

<span data-ttu-id="b3c7f-154">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b3c7f-155">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b3c7f-155">Request body</span></span>

<span data-ttu-id="b3c7f-156">A kérelem törzsében teljes **előfizetési** erőforrás szükséges.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-156">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="b3c7f-157">Győződjön meg arról, hogy az **állapot** tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-157">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="b3c7f-158">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b3c7f-158">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b3c7f-159">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b3c7f-159">REST response</span></span>

<span data-ttu-id="b3c7f-160">Ha ez sikeres, a metódus a válasz törzsében a törölt [előfizetés](subscription-resources.md) erőforrás-tulajdonságokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-160">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b3c7f-161">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b3c7f-161">Response success and error codes</span></span>

<span data-ttu-id="b3c7f-162">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b3c7f-163">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b3c7f-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b3c7f-164">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b3c7f-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b3c7f-165">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b3c7f-165">Response example</span></span>

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
