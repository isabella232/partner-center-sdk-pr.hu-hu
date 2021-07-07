---
title: Felfüggesztett előfizetés újraaktiválása
description: Újraaktivál egy olyan előfizetést, amelyet korábban felfüggesztettek fizetés nélkül. Az Partnerközpont irányítópulton ez a művelet az ügyfél kiválasztásával hajtható végre.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b6e3574119f9c645cc3f730047d2a23484ad8a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547710"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="e647d-104">Felfüggesztett előfizetés újraaktiválása</span><span class="sxs-lookup"><span data-stu-id="e647d-104">Reactivate a suspended subscription</span></span>

<span data-ttu-id="e647d-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e647d-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e647d-106">Újraaktivál egy [olyan előfizetést,](subscription-resources.md) amelyet korábban felfüggesztettek fizetés nélkül.</span><span class="sxs-lookup"><span data-stu-id="e647d-106">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="e647d-107">Az Partnerközpont irányítópulton ez a művelet úgy hajtható végre, hogy először [kiválaszt egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="e647d-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="e647d-108">Ezután válassza ki az átnevezni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="e647d-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="e647d-109">A befejezéshez kattintson az **Aktív gombra,** majd válassza a Küldés **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e647d-109">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e647d-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e647d-110">Prerequisites</span></span>

- <span data-ttu-id="e647d-111">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e647d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e647d-112">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="e647d-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e647d-113">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e647d-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e647d-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e647d-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e647d-115">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e647d-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e647d-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="e647d-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e647d-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="e647d-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e647d-118">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e647d-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e647d-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="e647d-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="e647d-120">C\#</span><span class="sxs-lookup"><span data-stu-id="e647d-120">C\#</span></span>

<span data-ttu-id="e647d-121">Az ügyfél előfizetésének újraaktiválához [](get-a-subscription-by-id.md)először szerezze be az előfizetést, majd módosítsa az előfizetés [**Status (Állapot) tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status)</span><span class="sxs-lookup"><span data-stu-id="e647d-121">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="e647d-122">Az **állapotkódokkal** kapcsolatos információkért lásd: [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="e647d-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="e647d-123">A módosítás után használja az [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="e647d-123">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="e647d-124">Ezután hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="e647d-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="e647d-125">Végül hívja meg a [**Patch() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="e647d-125">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

<span data-ttu-id="e647d-126">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="e647d-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e647d-127">**Project:** FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="e647d-127">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="e647d-128">**Osztály:** UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="e647d-128">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="e647d-129">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="e647d-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e647d-130">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e647d-130">Request syntax</span></span>

| <span data-ttu-id="e647d-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="e647d-131">Method</span></span>    | <span data-ttu-id="e647d-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e647d-132">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e647d-133">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="e647d-133">**PATCH**</span></span> | <span data-ttu-id="e647d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e647d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e647d-135">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="e647d-135">URI parameter</span></span>

<span data-ttu-id="e647d-136">Ez a táblázat felsorolja az előfizetés újraaktiválához szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="e647d-136">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="e647d-137">Név</span><span class="sxs-lookup"><span data-stu-id="e647d-137">Name</span></span>                    | <span data-ttu-id="e647d-138">Típus</span><span class="sxs-lookup"><span data-stu-id="e647d-138">Type</span></span>     | <span data-ttu-id="e647d-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e647d-139">Required</span></span> | <span data-ttu-id="e647d-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="e647d-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="e647d-141">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="e647d-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="e647d-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="e647d-142">**guid**</span></span> | <span data-ttu-id="e647d-143">Y</span><span class="sxs-lookup"><span data-stu-id="e647d-143">Y</span></span>        | <span data-ttu-id="e647d-144">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="e647d-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="e647d-145">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="e647d-145">**id-for-subscription**</span></span> | <span data-ttu-id="e647d-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="e647d-146">**guid**</span></span> | <span data-ttu-id="e647d-147">Y</span><span class="sxs-lookup"><span data-stu-id="e647d-147">Y</span></span>        | <span data-ttu-id="e647d-148">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="e647d-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e647d-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e647d-149">Request headers</span></span>

<span data-ttu-id="e647d-150">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e647d-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e647d-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e647d-151">Request body</span></span>

<span data-ttu-id="e647d-152">A kérelem **törzsében** teljes előfizetési erőforrásra van szükség.</span><span class="sxs-lookup"><span data-stu-id="e647d-152">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="e647d-153">Győződjön meg **arról, hogy** az Állapot tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="e647d-153">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="e647d-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e647d-154">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
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
    "Status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="e647d-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e647d-155">REST response</span></span>

<span data-ttu-id="e647d-156">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza az előfizetés [frissített](subscription-resources.md) erőforrás-tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="e647d-156">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e647d-157">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e647d-157">Response success and error codes</span></span>

<span data-ttu-id="e647d-158">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="e647d-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e647d-159">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="e647d-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e647d-160">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e647d-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e647d-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e647d-161">Response example</span></span>

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
    "Status": "active",
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
