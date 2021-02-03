---
title: Az előfizetések listájának lekérése megrendelés alapján
description: Egy adott rendeléshez tartozó előfizetési erőforrások gyűjteményét kapja meg.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 56b9c80021cace03976d410b2a6cd4c0eee18398
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768243"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="98d8f-103">Az előfizetések listájának lekérése megrendelés alapján</span><span class="sxs-lookup"><span data-stu-id="98d8f-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="98d8f-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="98d8f-104">**Applies To**</span></span>

- <span data-ttu-id="98d8f-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="98d8f-105">Partner Center</span></span>
- <span data-ttu-id="98d8f-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="98d8f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="98d8f-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="98d8f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="98d8f-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="98d8f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="98d8f-109">Egy adott rendeléshez tartozó [előfizetési](subscription-resources.md) erőforrások gyűjteményét kapja meg.</span><span class="sxs-lookup"><span data-stu-id="98d8f-109">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98d8f-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="98d8f-110">Prerequisites</span></span>

- <span data-ttu-id="98d8f-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="98d8f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="98d8f-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="98d8f-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="98d8f-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="98d8f-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="98d8f-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="98d8f-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="98d8f-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="98d8f-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="98d8f-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="98d8f-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="98d8f-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="98d8f-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="98d8f-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="98d8f-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="98d8f-119">Egy megrendelés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="98d8f-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="98d8f-120">C\#</span><span class="sxs-lookup"><span data-stu-id="98d8f-120">C\#</span></span>

<span data-ttu-id="98d8f-121">Az előfizetések sorrend szerinti listájának lekéréséhez használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="98d8f-121">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="98d8f-122">Ezután hívja meg az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a **ByOrder ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="98d8f-122">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="98d8f-123">Fejezze be a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync)metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="98d8f-123">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="98d8f-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="98d8f-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="98d8f-125">**Projekt**: PartnerSDK. FeatureSample **osztály**: SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="98d8f-125">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="98d8f-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="98d8f-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="98d8f-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="98d8f-127">Request syntax</span></span>

| <span data-ttu-id="98d8f-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="98d8f-128">Method</span></span>  | <span data-ttu-id="98d8f-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="98d8f-129">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="98d8f-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="98d8f-130">**GET**</span></span> | <span data-ttu-id="98d8f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions? rendelés \_ azonosítója = {azonosító-for-Order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="98d8f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="98d8f-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="98d8f-132">URI parameter</span></span>

<span data-ttu-id="98d8f-133">Ez a táblázat felsorolja az összes előfizetés lekéréséhez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="98d8f-133">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="98d8f-134">Név</span><span class="sxs-lookup"><span data-stu-id="98d8f-134">Name</span></span>                   | <span data-ttu-id="98d8f-135">Típus</span><span class="sxs-lookup"><span data-stu-id="98d8f-135">Type</span></span>     | <span data-ttu-id="98d8f-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="98d8f-136">Required</span></span> | <span data-ttu-id="98d8f-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="98d8f-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="98d8f-138">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="98d8f-138">**customer-tenant-id**</span></span> | <span data-ttu-id="98d8f-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="98d8f-139">**guid**</span></span> | <span data-ttu-id="98d8f-140">Y</span><span class="sxs-lookup"><span data-stu-id="98d8f-140">Y</span></span>        | <span data-ttu-id="98d8f-141">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="98d8f-141">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="98d8f-142">**azonosító – sorrend**</span><span class="sxs-lookup"><span data-stu-id="98d8f-142">**id-for-order**</span></span>       | <span data-ttu-id="98d8f-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="98d8f-143">**guid**</span></span> | <span data-ttu-id="98d8f-144">Y</span><span class="sxs-lookup"><span data-stu-id="98d8f-144">Y</span></span>        | <span data-ttu-id="98d8f-145">A sorrendnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="98d8f-145">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="98d8f-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="98d8f-146">Request headers</span></span>

<span data-ttu-id="98d8f-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="98d8f-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="98d8f-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="98d8f-148">Request body</span></span>

<span data-ttu-id="98d8f-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="98d8f-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="98d8f-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="98d8f-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="98d8f-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="98d8f-151">REST response</span></span>

<span data-ttu-id="98d8f-152">Ha ez sikeres, ez a metódus az [előfizetési](subscription-resources.md) erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="98d8f-152">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="98d8f-153">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="98d8f-153">Response success and error codes</span></span>

<span data-ttu-id="98d8f-154">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="98d8f-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="98d8f-155">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="98d8f-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="98d8f-156">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="98d8f-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="98d8f-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="98d8f-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "Myofferpurchase",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "{id-for-order}",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
