---
title: Egy előfizetés bővítménylistájának lekérése
description: Az ügyfél által az előfizetéshez hozzáadni választott bővítmények gyűjteményének lekért gyűjteménye.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: c627f595333a295048b02ec4326dcdc279d07b51
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874635"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="26e17-103">Egy előfizetés bővítménylistájának lekérése</span><span class="sxs-lookup"><span data-stu-id="26e17-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="26e17-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="26e17-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="26e17-105">Ez a cikk azt ismerteti, hogyan lehet olyan bővítmények gyűjteményét lekérte, amelyek hozzáadását az ügyfél az előfizetési **[erőforráshoz](subscription-resources.md)** választotta.</span><span class="sxs-lookup"><span data-stu-id="26e17-105">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26e17-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="26e17-106">Prerequisites</span></span>

- <span data-ttu-id="26e17-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="26e17-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="26e17-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="26e17-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="26e17-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="26e17-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="26e17-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="26e17-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="26e17-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="26e17-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="26e17-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="26e17-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="26e17-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="26e17-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="26e17-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="26e17-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="26e17-115">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="26e17-115">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="26e17-116">C\#</span><span class="sxs-lookup"><span data-stu-id="26e17-116">C\#</span></span>

<span data-ttu-id="26e17-117">Az ügyfél előfizetéséhez elérhető bővítmények listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="26e17-117">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="26e17-118">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="26e17-118">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="26e17-119">Hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="26e17-119">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="26e17-120">Hívja meg [**az Addons tulajdonságot,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) majd a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) a [**GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="26e17-120">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="26e17-121">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="26e17-121">For an example, see the following:</span></span>

- <span data-ttu-id="26e17-122">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="26e17-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="26e17-123">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="26e17-123">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="26e17-124">Osztály: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="26e17-124">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="26e17-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="26e17-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="26e17-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="26e17-126">Request syntax</span></span>

| <span data-ttu-id="26e17-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="26e17-127">Method</span></span>  | <span data-ttu-id="26e17-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="26e17-128">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="26e17-129">**Kap**</span><span class="sxs-lookup"><span data-stu-id="26e17-129">**GET**</span></span> | <span data-ttu-id="26e17-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="26e17-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="26e17-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="26e17-131">URI parameter</span></span>

<span data-ttu-id="26e17-132">Ez a táblázat felsorolja az előfizetés bővítményei listájának lekérdezhető lekérdezési paramétereit.</span><span class="sxs-lookup"><span data-stu-id="26e17-132">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="26e17-133">Név</span><span class="sxs-lookup"><span data-stu-id="26e17-133">Name</span></span>                    | <span data-ttu-id="26e17-134">Típus</span><span class="sxs-lookup"><span data-stu-id="26e17-134">Type</span></span>     | <span data-ttu-id="26e17-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="26e17-135">Required</span></span> | <span data-ttu-id="26e17-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="26e17-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="26e17-137">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="26e17-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="26e17-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="26e17-138">**guid**</span></span> | <span data-ttu-id="26e17-139">Y</span><span class="sxs-lookup"><span data-stu-id="26e17-139">Y</span></span>        | <span data-ttu-id="26e17-140">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="26e17-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="26e17-141">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="26e17-141">**id-for-subscription**</span></span> | <span data-ttu-id="26e17-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="26e17-142">**guid**</span></span> | <span data-ttu-id="26e17-143">Y</span><span class="sxs-lookup"><span data-stu-id="26e17-143">Y</span></span>        | <span data-ttu-id="26e17-144">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="26e17-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="26e17-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="26e17-145">Request headers</span></span>

<span data-ttu-id="26e17-146">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="26e17-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="26e17-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="26e17-147">Request body</span></span>

<span data-ttu-id="26e17-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="26e17-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="26e17-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="26e17-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="26e17-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="26e17-150">REST response</span></span>

<span data-ttu-id="26e17-151">Ha a művelet sikeres, ez a metódus a válasz törzsében egy erőforrás-gyűjteményt ad vissza.</span><span class="sxs-lookup"><span data-stu-id="26e17-151">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="26e17-152">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="26e17-152">Response success and error codes</span></span>

<span data-ttu-id="26e17-153">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="26e17-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="26e17-154">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="26e17-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="26e17-155">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="26e17-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="26e17-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="26e17-156">Response example</span></span>

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
        "entitlementId": "42226ed6-070a-4e0f-b80c-4cdfB3e97aa7",
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
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
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
