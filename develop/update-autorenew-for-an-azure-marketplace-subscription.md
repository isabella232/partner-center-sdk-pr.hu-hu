---
title: Kereskedelmi piactéri előfizetés automatikus megújításának frissítése
description: Frissítse az ügyfél-és előfizetés-AZONOSÍTÓval egyező előfizetési erőforráshoz tartozó autorenew tulajdonságot.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dccec57901ea4ea429b74044e3b6c28178c43f6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768264"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="88604-103">Kereskedelmi piactéri előfizetés automatikus megújításának frissítése</span><span class="sxs-lookup"><span data-stu-id="88604-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="88604-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="88604-104">**Applies To**</span></span>

- <span data-ttu-id="88604-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="88604-105">Partner Center</span></span>

<span data-ttu-id="88604-106">Frissítse az ügyfél-és előfizetés-AZONOSÍTÓval egyező kereskedelmi piactér- [előfizetési](subscription-resources.md) erőforráshoz tartozó autorenew tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="88604-106">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="88604-107">A partner Center irányítópultján a művelet végrehajtásához először válasszon ki [egy ügyfelet](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="88604-107">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="88604-108">Ezután válassza ki a frissíteni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="88604-108">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="88604-109">Végül kapcsolja be az **automatikus megújítás** lehetőséget, majd kattintson a **Küldés** elemre.</span><span class="sxs-lookup"><span data-stu-id="88604-109">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88604-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="88604-110">Prerequisites</span></span>

- <span data-ttu-id="88604-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="88604-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="88604-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="88604-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="88604-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="88604-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="88604-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="88604-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="88604-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="88604-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="88604-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="88604-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="88604-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="88604-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="88604-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="88604-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="88604-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="88604-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="88604-120">C\#</span><span class="sxs-lookup"><span data-stu-id="88604-120">C\#</span></span>

<span data-ttu-id="88604-121">Az ügyfél előfizetésének frissítéséhez először [szerezze be az előfizetést](get-a-subscription-by-id.md), majd állítsa be az előfizetés [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="88604-121">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="88604-122">A módosítást követően használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="88604-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="88604-123">Ezután hívja meg az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="88604-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="88604-124">Ezután fejezze be a **Patch ()** metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="88604-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="88604-125">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="88604-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="88604-126">**Projekt**: PartnerSDK. FeatureSample **osztály**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="88604-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="88604-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="88604-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="88604-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="88604-128">Request syntax</span></span>

| <span data-ttu-id="88604-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="88604-129">Method</span></span>    | <span data-ttu-id="88604-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="88604-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="88604-131">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="88604-131">**PATCH**</span></span> | <span data-ttu-id="88604-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="88604-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="88604-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="88604-133">URI parameter</span></span>

<span data-ttu-id="88604-134">Ez a táblázat felsorolja az előfizetés felfüggesztéséhez szükséges lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="88604-134">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="88604-135">Név</span><span class="sxs-lookup"><span data-stu-id="88604-135">Name</span></span>                    | <span data-ttu-id="88604-136">Típus</span><span class="sxs-lookup"><span data-stu-id="88604-136">Type</span></span>     | <span data-ttu-id="88604-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="88604-137">Required</span></span> | <span data-ttu-id="88604-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="88604-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="88604-139">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="88604-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="88604-140">**GUID**</span><span class="sxs-lookup"><span data-stu-id="88604-140">**GUID**</span></span> | <span data-ttu-id="88604-141">Y</span><span class="sxs-lookup"><span data-stu-id="88604-141">Y</span></span>        | <span data-ttu-id="88604-142">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="88604-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="88604-143">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="88604-143">**id-for-subscription**</span></span> | <span data-ttu-id="88604-144">**GUID**</span><span class="sxs-lookup"><span data-stu-id="88604-144">**GUID**</span></span> | <span data-ttu-id="88604-145">Y</span><span class="sxs-lookup"><span data-stu-id="88604-145">Y</span></span>        | <span data-ttu-id="88604-146">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="88604-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="88604-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="88604-147">Request headers</span></span>

<span data-ttu-id="88604-148">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="88604-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="88604-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="88604-149">Request body</span></span>

<span data-ttu-id="88604-150">A kérelem törzsében teljes kereskedelmi piactér- **előfizetési** erőforrás szükséges.</span><span class="sxs-lookup"><span data-stu-id="88604-150">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="88604-151">Győződjön meg arról, hogy a **AutoRenewEnabled** tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="88604-151">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="88604-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="88604-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="88604-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="88604-153">REST response</span></span>

<span data-ttu-id="88604-154">Ha ez sikeres, a metódus a válasz törzsében a frissített [előfizetés](subscription-resources.md) erőforrás-tulajdonságokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="88604-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="88604-155">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="88604-155">Response success and error codes</span></span>

<span data-ttu-id="88604-156">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="88604-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="88604-157">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="88604-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="88604-158">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="88604-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="88604-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="88604-159">Response example</span></span>

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
