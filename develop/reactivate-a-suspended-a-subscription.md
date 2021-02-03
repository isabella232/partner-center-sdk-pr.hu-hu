---
title: Felfüggesztett előfizetés újraaktiválása
description: Újraaktiválja az előfizetést, amelyet korábban nem fizettek fel. A partner Center irányítópultján ezt a műveletet a felhasználó kiválasztásával végezheti el.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17c63e9c6d4c9e111bfea28e97319696534fa122
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768284"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="95ca4-103">Felfüggesztett előfizetés újraaktiválása</span><span class="sxs-lookup"><span data-stu-id="95ca4-103">Reactivate a suspended subscription</span></span>

<span data-ttu-id="95ca4-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="95ca4-104">**Applies To**</span></span>

- <span data-ttu-id="95ca4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="95ca4-105">Partner Center</span></span>
- <span data-ttu-id="95ca4-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="95ca4-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="95ca4-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="95ca4-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="95ca4-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="95ca4-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="95ca4-109">Újraaktiválja az [előfizetést](subscription-resources.md) , amelyet korábban nem fizettek fel.</span><span class="sxs-lookup"><span data-stu-id="95ca4-109">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="95ca4-110">A partner Center irányítópultján ezt a műveletet a [felhasználó kiválasztásával](get-a-customer-by-name.md)végezheti el.</span><span class="sxs-lookup"><span data-stu-id="95ca4-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="95ca4-111">Ezután válassza ki az átnevezni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="95ca4-111">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="95ca4-112">A befejezéshez kattintson az **aktív** gombra, majd válassza a **Küldés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="95ca4-112">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95ca4-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="95ca4-113">Prerequisites</span></span>

- <span data-ttu-id="95ca4-114">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="95ca4-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="95ca4-115">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="95ca4-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="95ca4-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95ca4-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="95ca4-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="95ca4-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="95ca4-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="95ca4-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="95ca4-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="95ca4-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="95ca4-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="95ca4-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="95ca4-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="95ca4-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="95ca4-122">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="95ca4-122">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="95ca4-123">C\#</span><span class="sxs-lookup"><span data-stu-id="95ca4-123">C\#</span></span>

<span data-ttu-id="95ca4-124">Az ügyfél előfizetésének újraaktiválásához először [szerezze be az előfizetést](get-a-subscription-by-id.md), majd módosítsa az előfizetés [**status (állapot**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) ) tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="95ca4-124">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="95ca4-125">Az **állapotkódok** információit lásd: [SubscriptionStatus enumerálás/DotNet/API/Microsoft. Store. partnercenter. models. Subscriptions. SubscriptionStatus).</span><span class="sxs-lookup"><span data-stu-id="95ca4-125">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="95ca4-126">A módosítást követően használja a [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="95ca4-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="95ca4-127">Ezután hívja meg az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="95ca4-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="95ca4-128">Ezután fejezze be a [**Patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="95ca4-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

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

<span data-ttu-id="95ca4-129">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="95ca4-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="95ca4-130">**Projekt**: FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="95ca4-130">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="95ca4-131">**Osztály**: UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="95ca4-131">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="95ca4-132">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="95ca4-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="95ca4-133">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="95ca4-133">Request syntax</span></span>

| <span data-ttu-id="95ca4-134">Metódus</span><span class="sxs-lookup"><span data-stu-id="95ca4-134">Method</span></span>    | <span data-ttu-id="95ca4-135">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="95ca4-135">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="95ca4-136">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="95ca4-136">**PATCH**</span></span> | <span data-ttu-id="95ca4-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="95ca4-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="95ca4-138">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="95ca4-138">URI parameter</span></span>

<span data-ttu-id="95ca4-139">Ez a táblázat felsorolja az előfizetés újraaktiválásához szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="95ca4-139">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="95ca4-140">Név</span><span class="sxs-lookup"><span data-stu-id="95ca4-140">Name</span></span>                    | <span data-ttu-id="95ca4-141">Típus</span><span class="sxs-lookup"><span data-stu-id="95ca4-141">Type</span></span>     | <span data-ttu-id="95ca4-142">Kötelező</span><span class="sxs-lookup"><span data-stu-id="95ca4-142">Required</span></span> | <span data-ttu-id="95ca4-143">Leírás</span><span class="sxs-lookup"><span data-stu-id="95ca4-143">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="95ca4-144">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="95ca4-144">**customer-tenant-id**</span></span>  | <span data-ttu-id="95ca4-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="95ca4-145">**guid**</span></span> | <span data-ttu-id="95ca4-146">Y</span><span class="sxs-lookup"><span data-stu-id="95ca4-146">Y</span></span>        | <span data-ttu-id="95ca4-147">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="95ca4-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="95ca4-148">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="95ca4-148">**id-for-subscription**</span></span> | <span data-ttu-id="95ca4-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="95ca4-149">**guid**</span></span> | <span data-ttu-id="95ca4-150">Y</span><span class="sxs-lookup"><span data-stu-id="95ca4-150">Y</span></span>        | <span data-ttu-id="95ca4-151">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="95ca4-151">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="95ca4-152">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="95ca4-152">Request headers</span></span>

<span data-ttu-id="95ca4-153">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="95ca4-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="95ca4-154">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="95ca4-154">Request body</span></span>

<span data-ttu-id="95ca4-155">A kérelem törzsében teljes **előfizetési** erőforrás szükséges.</span><span class="sxs-lookup"><span data-stu-id="95ca4-155">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="95ca4-156">Győződjön meg arról, hogy az **állapot** tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="95ca4-156">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="95ca4-157">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="95ca4-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="95ca4-158">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="95ca4-158">REST response</span></span>

<span data-ttu-id="95ca4-159">Ha ez sikeres, a metódus a válasz törzsében a frissített [előfizetés](subscription-resources.md) erőforrás-tulajdonságokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="95ca4-159">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="95ca4-160">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="95ca4-160">Response success and error codes</span></span>

<span data-ttu-id="95ca4-161">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="95ca4-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="95ca4-162">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="95ca4-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="95ca4-163">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="95ca4-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="95ca4-164">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="95ca4-164">Response example</span></span>

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
