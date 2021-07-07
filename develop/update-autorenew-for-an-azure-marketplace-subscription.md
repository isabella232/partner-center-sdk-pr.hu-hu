---
title: Kereskedelmi piactéri előfizetés automatikus megújításának frissítése
description: Frissítse egy előfizetési erőforrás autorenew tulajdonságát, amely megfelel az ügyfél és az előfizetés azonosítójának.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cc0b4c4bff5e8762ffcc2552b2e9e36bcf93686c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446666"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="38325-103">Kereskedelmi piactéri előfizetés automatikus megújításának frissítése</span><span class="sxs-lookup"><span data-stu-id="38325-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="38325-104">Frissítse egy kereskedelmi piactéri előfizetési erőforrás autorenew [tulajdonságát,](subscription-resources.md) amely megfelel az ügyfél és az előfizetés azonosítójának.</span><span class="sxs-lookup"><span data-stu-id="38325-104">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="38325-105">A Partnerközpont a műveletet úgy hajtjuk végre, hogy először [kiválasztunk egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="38325-105">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="38325-106">Ezután válassza ki a frissíteni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="38325-106">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="38325-107">Végül válthat az Automatikus **megújítás lehetőséggel,** majd válassza a **Küldés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="38325-107">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38325-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="38325-108">Prerequisites</span></span>

- <span data-ttu-id="38325-109">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="38325-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="38325-110">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="38325-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="38325-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="38325-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="38325-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="38325-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="38325-113">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="38325-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="38325-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="38325-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="38325-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="38325-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="38325-116">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="38325-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="38325-117">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="38325-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="38325-118">C\#</span><span class="sxs-lookup"><span data-stu-id="38325-118">C\#</span></span>

<span data-ttu-id="38325-119">Az ügyfél előfizetésének frissítéséhez [](get-a-subscription-by-id.md)először szerezze be az előfizetést, majd állítsa be az [**előfizetés autoRenewEnabled tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled)</span><span class="sxs-lookup"><span data-stu-id="38325-119">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="38325-120">A módosítás után használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="38325-120">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="38325-121">Ezután hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="38325-121">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="38325-122">Végül hívja meg a **Patch() metódust.**</span><span class="sxs-lookup"><span data-stu-id="38325-122">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="38325-123">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="38325-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="38325-124">**Project:** PartnerSDK.FeatureSample **osztály:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="38325-124">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="38325-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="38325-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="38325-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="38325-126">Request syntax</span></span>

| <span data-ttu-id="38325-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="38325-127">Method</span></span>    | <span data-ttu-id="38325-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="38325-128">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="38325-129">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="38325-129">**PATCH**</span></span> | <span data-ttu-id="38325-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="38325-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="38325-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="38325-131">URI parameter</span></span>

<span data-ttu-id="38325-132">Ez a táblázat felsorolja az előfizetés felfüggesztéséhez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="38325-132">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="38325-133">Név</span><span class="sxs-lookup"><span data-stu-id="38325-133">Name</span></span>                    | <span data-ttu-id="38325-134">Típus</span><span class="sxs-lookup"><span data-stu-id="38325-134">Type</span></span>     | <span data-ttu-id="38325-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="38325-135">Required</span></span> | <span data-ttu-id="38325-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="38325-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="38325-137">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="38325-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="38325-138">**Guid**</span><span class="sxs-lookup"><span data-stu-id="38325-138">**GUID**</span></span> | <span data-ttu-id="38325-139">Y</span><span class="sxs-lookup"><span data-stu-id="38325-139">Y</span></span>        | <span data-ttu-id="38325-140">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="38325-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="38325-141">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="38325-141">**id-for-subscription**</span></span> | <span data-ttu-id="38325-142">**Guid**</span><span class="sxs-lookup"><span data-stu-id="38325-142">**GUID**</span></span> | <span data-ttu-id="38325-143">Y</span><span class="sxs-lookup"><span data-stu-id="38325-143">Y</span></span>        | <span data-ttu-id="38325-144">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="38325-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="38325-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="38325-145">Request headers</span></span>

<span data-ttu-id="38325-146">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="38325-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="38325-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="38325-147">Request body</span></span>

<span data-ttu-id="38325-148">A kérelem törzsében egy teljes **kereskedelmi** piactéri előfizetési erőforrásra van szükség.</span><span class="sxs-lookup"><span data-stu-id="38325-148">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="38325-149">Győződjön meg arról, hogy az **AutoRenewEnabled tulajdonság** frissült.</span><span class="sxs-lookup"><span data-stu-id="38325-149">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="38325-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="38325-150">Request example</span></span>

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
    "status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="38325-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="38325-151">REST response</span></span>

<span data-ttu-id="38325-152">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza az előfizetés [frissített](subscription-resources.md) erőforrás-tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="38325-152">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="38325-153">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="38325-153">Response success and error codes</span></span>

<span data-ttu-id="38325-154">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="38325-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="38325-155">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="38325-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="38325-156">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="38325-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="38325-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="38325-157">Response example</span></span>

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
    "status": "active",
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
