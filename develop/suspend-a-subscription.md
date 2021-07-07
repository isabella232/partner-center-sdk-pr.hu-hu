---
title: Előfizetés felfüggesztése
description: Felfüggeszt egy előfizetési erőforrást, amely csalás vagy fizetés meg nem fizetés miatt megfelel az ügyfélnek és az előfizetés azonosítójának. Az Partnerközpont irányítópulton ez a művelet az ügyfél kiválasztásával hajtható végre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dae7c3422a403c48a2b10424c4ae5dbdbc498ea
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547342"
---
# <a name="suspend-a-subscription"></a><span data-ttu-id="73d22-104">Előfizetés felfüggesztése</span><span class="sxs-lookup"><span data-stu-id="73d22-104">Suspend a subscription</span></span>

<span data-ttu-id="73d22-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="73d22-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="73d22-106">Felfüggeszt egy [előfizetési erőforrást,](subscription-resources.md) amely csalás vagy fizetés meg nem fizetés miatt megfelel az ügyfélnek és az előfizetés azonosítójának.</span><span class="sxs-lookup"><span data-stu-id="73d22-106">Suspends a [Subscription](subscription-resources.md) resource that matches the customer and subscription ID due to fraud or non-payment.</span></span>

<span data-ttu-id="73d22-107">Az Partnerközpont irányítópulton ez a művelet úgy hajtható végre, hogy először [kiválaszt egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="73d22-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="73d22-108">Ezután válassza ki az átnevezni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="73d22-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="73d22-109">A befejezéshez kattintson a **Felfüggesztve gombra,** majd válassza a Küldés **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="73d22-109">To finish, choose the **Suspended** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73d22-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="73d22-110">Prerequisites</span></span>

- <span data-ttu-id="73d22-111">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="73d22-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="73d22-112">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="73d22-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="73d22-113">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73d22-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="73d22-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="73d22-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="73d22-115">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="73d22-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="73d22-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="73d22-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="73d22-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="73d22-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="73d22-118">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73d22-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="73d22-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="73d22-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="73d22-120">C\#</span><span class="sxs-lookup"><span data-stu-id="73d22-120">C\#</span></span>

<span data-ttu-id="73d22-121">Az ügyfél előfizetésének felfüggesztéséhez [](get-a-subscription-by-id.md)először szerezze be az előfizetést, majd módosítsa az előfizetés [**Status (Állapot) tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)</span><span class="sxs-lookup"><span data-stu-id="73d22-121">To suspend a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="73d22-122">Az **állapotkódokkal** kapcsolatos információkért lásd: [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="73d22-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="73d22-123">A módosítás után használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="73d22-123">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="73d22-124">Ezután hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="73d22-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="73d22-125">Végül hívja meg a **Patch() metódust.**</span><span class="sxs-lookup"><span data-stu-id="73d22-125">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Suspended
   });
```

<span data-ttu-id="73d22-126">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="73d22-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="73d22-127">**Project:** PartnerSDK.FeatureSample **osztály:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="73d22-127">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="73d22-128">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="73d22-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="73d22-129">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="73d22-129">Request syntax</span></span>

| <span data-ttu-id="73d22-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="73d22-130">Method</span></span>    | <span data-ttu-id="73d22-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="73d22-131">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="73d22-132">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="73d22-132">**PATCH**</span></span> | <span data-ttu-id="73d22-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="73d22-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="73d22-134">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="73d22-134">URI parameter</span></span>

<span data-ttu-id="73d22-135">Ez a táblázat felsorolja az előfizetés felfüggesztéséhez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="73d22-135">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="73d22-136">Név</span><span class="sxs-lookup"><span data-stu-id="73d22-136">Name</span></span>                    | <span data-ttu-id="73d22-137">Típus</span><span class="sxs-lookup"><span data-stu-id="73d22-137">Type</span></span>     | <span data-ttu-id="73d22-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="73d22-138">Required</span></span> | <span data-ttu-id="73d22-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="73d22-139">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="73d22-140">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="73d22-140">**customer-tenant-id**</span></span>  | <span data-ttu-id="73d22-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="73d22-141">**guid**</span></span> | <span data-ttu-id="73d22-142">Y</span><span class="sxs-lookup"><span data-stu-id="73d22-142">Y</span></span>        | <span data-ttu-id="73d22-143">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="73d22-143">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="73d22-144">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="73d22-144">**id-for-subscription**</span></span> | <span data-ttu-id="73d22-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="73d22-145">**guid**</span></span> | <span data-ttu-id="73d22-146">Y</span><span class="sxs-lookup"><span data-stu-id="73d22-146">Y</span></span>        | <span data-ttu-id="73d22-147">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="73d22-147">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="73d22-148">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="73d22-148">Request headers</span></span>

<span data-ttu-id="73d22-149">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="73d22-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="73d22-150">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="73d22-150">Request body</span></span>

<span data-ttu-id="73d22-151">A kérelem **törzsében** teljes előfizetési erőforrásra van szükség.</span><span class="sxs-lookup"><span data-stu-id="73d22-151">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="73d22-152">Győződjön meg **arról, hogy** az Állapot tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="73d22-152">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="73d22-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="73d22-153">Request example</span></span>

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
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="73d22-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="73d22-154">REST response</span></span>

<span data-ttu-id="73d22-155">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza az előfizetés [frissített](subscription-resources.md) erőforrás-tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="73d22-155">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="73d22-156">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="73d22-156">Response success and error codes</span></span>

<span data-ttu-id="73d22-157">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="73d22-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="73d22-158">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="73d22-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="73d22-159">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="73d22-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="73d22-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="73d22-160">Response example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
