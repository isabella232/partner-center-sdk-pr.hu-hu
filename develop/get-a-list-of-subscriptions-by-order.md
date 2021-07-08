---
title: Az előfizetések listájának lekérése megrendelés alapján
description: Lekért egy adott rendelésnek megfelelő előfizetési erőforrások gyűjteményét.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 011a92500d0c7ed44f86030febd1ea83be2c6474
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873955"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="d7fde-103">Az előfizetések listájának lekérése megrendelés alapján</span><span class="sxs-lookup"><span data-stu-id="d7fde-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="d7fde-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d7fde-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d7fde-105">Lekért egy [adott](subscription-resources.md) rendelésnek megfelelő előfizetési erőforrások gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="d7fde-105">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7fde-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d7fde-106">Prerequisites</span></span>

- <span data-ttu-id="d7fde-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d7fde-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d7fde-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d7fde-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d7fde-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d7fde-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d7fde-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d7fde-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d7fde-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d7fde-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d7fde-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d7fde-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d7fde-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d7fde-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d7fde-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d7fde-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d7fde-115">Egy rendelésazonosító.</span><span class="sxs-lookup"><span data-stu-id="d7fde-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="d7fde-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d7fde-116">C\#</span></span>

<span data-ttu-id="d7fde-117">Az előfizetések megrendelési listájának lehívásához használja **az IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="d7fde-117">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="d7fde-118">Ezután hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a **ByOrder() metódust.**</span><span class="sxs-lookup"><span data-stu-id="d7fde-118">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="d7fde-119">Befejezésként hívja meg a [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) vagy [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync)</span><span class="sxs-lookup"><span data-stu-id="d7fde-119">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="d7fde-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d7fde-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d7fde-121">**Project:** PartnerSDK.FeatureSample **osztály:** SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="d7fde-121">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d7fde-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d7fde-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d7fde-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d7fde-123">Request syntax</span></span>

| <span data-ttu-id="d7fde-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="d7fde-124">Method</span></span>  | <span data-ttu-id="d7fde-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d7fde-125">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d7fde-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d7fde-126">**GET**</span></span> | <span data-ttu-id="d7fde-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order \_ id={id-for-order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d7fde-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d7fde-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d7fde-128">URI parameter</span></span>

<span data-ttu-id="d7fde-129">Ez a táblázat felsorolja az összes előfizetés lekérdezhető lekérdezési paraméterét.</span><span class="sxs-lookup"><span data-stu-id="d7fde-129">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="d7fde-130">Név</span><span class="sxs-lookup"><span data-stu-id="d7fde-130">Name</span></span>                   | <span data-ttu-id="d7fde-131">Típus</span><span class="sxs-lookup"><span data-stu-id="d7fde-131">Type</span></span>     | <span data-ttu-id="d7fde-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d7fde-132">Required</span></span> | <span data-ttu-id="d7fde-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="d7fde-133">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="d7fde-134">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="d7fde-134">**customer-tenant-id**</span></span> | <span data-ttu-id="d7fde-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="d7fde-135">**guid**</span></span> | <span data-ttu-id="d7fde-136">Y</span><span class="sxs-lookup"><span data-stu-id="d7fde-136">Y</span></span>        | <span data-ttu-id="d7fde-137">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="d7fde-137">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="d7fde-138">**id-for-order**</span><span class="sxs-lookup"><span data-stu-id="d7fde-138">**id-for-order**</span></span>       | <span data-ttu-id="d7fde-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="d7fde-139">**guid**</span></span> | <span data-ttu-id="d7fde-140">Y</span><span class="sxs-lookup"><span data-stu-id="d7fde-140">Y</span></span>        | <span data-ttu-id="d7fde-141">A rendelésnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="d7fde-141">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="d7fde-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d7fde-142">Request headers</span></span>

<span data-ttu-id="d7fde-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d7fde-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d7fde-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d7fde-144">Request body</span></span>

<span data-ttu-id="d7fde-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d7fde-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d7fde-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d7fde-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d7fde-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d7fde-147">REST response</span></span>

<span data-ttu-id="d7fde-148">Ha a művelet sikeres, ez a metódus [előfizetési](subscription-resources.md) erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="d7fde-148">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d7fde-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d7fde-149">Response success and error codes</span></span>

<span data-ttu-id="d7fde-150">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d7fde-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d7fde-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d7fde-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d7fde-152">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d7fde-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d7fde-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d7fde-153">Response example</span></span>

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
