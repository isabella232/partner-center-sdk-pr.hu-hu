---
title: Egy előfizetés bővítménylistájának lekérése
description: Olyan bővítmények gyűjteménye, amelyeket az ügyfél az előfizetéshez való hozzáadásra jelölt ki.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4e62ad22cf30c34dedfeb628003c695e33b78758
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768099"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="5db38-103">Egy előfizetés bővítménylistájának lekérése</span><span class="sxs-lookup"><span data-stu-id="5db38-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="5db38-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="5db38-104">**Applies to:**</span></span>

- <span data-ttu-id="5db38-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5db38-105">Partner Center</span></span>
- <span data-ttu-id="5db38-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="5db38-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5db38-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5db38-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5db38-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5db38-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5db38-109">Ez a cikk azt ismerteti, hogyan kérheti le az ügyfelek által az **[előfizetési](subscription-resources.md)** erőforráshoz hozzáadandó bővítmények gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="5db38-109">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5db38-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5db38-110">Prerequisites</span></span>

- <span data-ttu-id="5db38-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5db38-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5db38-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="5db38-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5db38-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5db38-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5db38-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="5db38-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5db38-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="5db38-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5db38-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="5db38-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5db38-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="5db38-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5db38-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5db38-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5db38-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="5db38-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="5db38-120">C\#</span><span class="sxs-lookup"><span data-stu-id="5db38-120">C\#</span></span>

<span data-ttu-id="5db38-121">Az ügyfél előfizetéséhez tartozó bővítmények listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="5db38-121">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="5db38-122">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="5db38-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="5db38-123">Hívja meg az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="5db38-123">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="5db38-124">Hívja meg az [**addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) tulajdonságot, majd a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync)metódust.</span><span class="sxs-lookup"><span data-stu-id="5db38-124">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="5db38-125">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="5db38-125">For an example, see the following:</span></span>

- <span data-ttu-id="5db38-126">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5db38-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5db38-127">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="5db38-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="5db38-128">Osztály: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="5db38-128">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5db38-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5db38-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5db38-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5db38-130">Request syntax</span></span>

| <span data-ttu-id="5db38-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="5db38-131">Method</span></span>  | <span data-ttu-id="5db38-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5db38-132">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5db38-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="5db38-133">**GET**</span></span> | <span data-ttu-id="5db38-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/addons http/1.1</span><span class="sxs-lookup"><span data-stu-id="5db38-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="5db38-135">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="5db38-135">URI parameter</span></span>

<span data-ttu-id="5db38-136">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az előfizetéshez tartozó bővítmények listájának lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="5db38-136">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="5db38-137">Név</span><span class="sxs-lookup"><span data-stu-id="5db38-137">Name</span></span>                    | <span data-ttu-id="5db38-138">Típus</span><span class="sxs-lookup"><span data-stu-id="5db38-138">Type</span></span>     | <span data-ttu-id="5db38-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5db38-139">Required</span></span> | <span data-ttu-id="5db38-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="5db38-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="5db38-141">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="5db38-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="5db38-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="5db38-142">**guid**</span></span> | <span data-ttu-id="5db38-143">Y</span><span class="sxs-lookup"><span data-stu-id="5db38-143">Y</span></span>        | <span data-ttu-id="5db38-144">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="5db38-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="5db38-145">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="5db38-145">**id-for-subscription**</span></span> | <span data-ttu-id="5db38-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="5db38-146">**guid**</span></span> | <span data-ttu-id="5db38-147">Y</span><span class="sxs-lookup"><span data-stu-id="5db38-147">Y</span></span>        | <span data-ttu-id="5db38-148">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="5db38-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5db38-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5db38-149">Request headers</span></span>

<span data-ttu-id="5db38-150">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5db38-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5db38-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5db38-151">Request body</span></span>

<span data-ttu-id="5db38-152">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="5db38-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5db38-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5db38-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="5db38-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5db38-154">REST response</span></span>

<span data-ttu-id="5db38-155">Ha ez sikeres, ez a metódus a válasz törzsében lévő erőforrások gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="5db38-155">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5db38-156">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5db38-156">Response success and error codes</span></span>

<span data-ttu-id="5db38-157">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5db38-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5db38-158">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5db38-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5db38-159">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5db38-159">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5db38-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5db38-160">Response example</span></span>

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
