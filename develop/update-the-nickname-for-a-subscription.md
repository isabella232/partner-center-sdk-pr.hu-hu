---
title: Egy előfizetés becenevének frissítése
description: Frissíti az ügyfél előfizetésének rövid nevét vagy becenevét.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 57a9fec4b69d4a64128425ea58b4bb84d0d7dd54
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768304"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="4ee5c-103">Egy előfizetés becenevének frissítése</span><span class="sxs-lookup"><span data-stu-id="4ee5c-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="4ee5c-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="4ee5c-104">**Applies To**</span></span>

- <span data-ttu-id="4ee5c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="4ee5c-105">Partner Center</span></span>
- <span data-ttu-id="4ee5c-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="4ee5c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4ee5c-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4ee5c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4ee5c-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4ee5c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4ee5c-109">Frissíti az ügyfél [előfizetésének](subscription-resources.md)rövid nevét vagy becenevét.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-109">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="4ee5c-110">Ez a név jelenik meg a partner Centerben, és segít az ügyfelek fiókjában lévő előfizetések megkülönböztetésében.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-110">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="4ee5c-111">A partner Center irányítópultján ezt a műveletet a [felhasználó kiválasztásával](get-a-customer-by-name.md)végezheti el.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="4ee5c-112">Ezután válassza ki az átnevezni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="4ee5c-113">A befejezéshez módosítsa a nevet az **előfizetés beceneve** mezőben, majd válassza a **Küldés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4ee5c-113">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ee5c-114">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4ee5c-114">Prerequisites</span></span>

- <span data-ttu-id="4ee5c-115">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4ee5c-116">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4ee5c-117">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4ee5c-118">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4ee5c-119">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4ee5c-120">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4ee5c-121">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4ee5c-122">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4ee5c-123">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="4ee5c-124">C\#</span><span class="sxs-lookup"><span data-stu-id="4ee5c-124">C\#</span></span>

<span data-ttu-id="4ee5c-125">Az ügyfél előfizetésének becenevének frissítéséhez először [szerezze be az előfizetést](get-a-subscription-by-id.md), majd módosítsa az előfizetés [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-125">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="4ee5c-126">A módosítást követően használja a [**IPartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="4ee5c-127">Ezután hívja meg az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="4ee5c-128">Ezután fejezze be a [**Patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="4ee5c-129">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4ee5c-130">**Projekt**: PartnerSDK. FeatureSamples **osztály**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="4ee5c-130">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4ee5c-131">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="4ee5c-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4ee5c-132">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4ee5c-132">Request syntax</span></span>

| <span data-ttu-id="4ee5c-133">Metódus</span><span class="sxs-lookup"><span data-stu-id="4ee5c-133">Method</span></span>    | <span data-ttu-id="4ee5c-134">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4ee5c-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4ee5c-135">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="4ee5c-135">**PATCH**</span></span> | <span data-ttu-id="4ee5c-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4ee5c-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4ee5c-137">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4ee5c-137">URI parameter</span></span>

<span data-ttu-id="4ee5c-138">Ez a táblázat felsorolja a szükséges lekérdezési paramétert az előfizetés-becenév frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-138">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="4ee5c-139">Név</span><span class="sxs-lookup"><span data-stu-id="4ee5c-139">Name</span></span>                    | <span data-ttu-id="4ee5c-140">Típus</span><span class="sxs-lookup"><span data-stu-id="4ee5c-140">Type</span></span>     | <span data-ttu-id="4ee5c-141">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4ee5c-141">Required</span></span> | <span data-ttu-id="4ee5c-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="4ee5c-142">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="4ee5c-143">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="4ee5c-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="4ee5c-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="4ee5c-144">**guid**</span></span> | <span data-ttu-id="4ee5c-145">Y</span><span class="sxs-lookup"><span data-stu-id="4ee5c-145">Y</span></span>        | <span data-ttu-id="4ee5c-146">Az **ügyfél-bérlő-azonosító** (GUID).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-146">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="4ee5c-147">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="4ee5c-147">**id-for-subscription**</span></span> | <span data-ttu-id="4ee5c-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="4ee5c-148">**guid**</span></span> | <span data-ttu-id="4ee5c-149">Y</span><span class="sxs-lookup"><span data-stu-id="4ee5c-149">Y</span></span>        | <span data-ttu-id="4ee5c-150">Az előfizetés azonosítója (GUID).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-150">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="4ee5c-151">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4ee5c-151">Request headers</span></span>

<span data-ttu-id="4ee5c-152">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4ee5c-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4ee5c-153">Request body</span></span>

<span data-ttu-id="4ee5c-154">A kérelem törzsében teljes **előfizetési** erőforrás szükséges.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="4ee5c-155">Győződjön meg arról, hogy a **FriendlyName** tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-155">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="4ee5c-156">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4ee5c-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
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
    OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="4ee5c-157">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4ee5c-157">REST response</span></span>

<span data-ttu-id="4ee5c-158">Ha ez sikeres, a metódus a válasz törzsében a frissített [előfizetés](subscription-resources.md) erőforrás-tulajdonságokat adja vissza.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4ee5c-159">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4ee5c-159">Response success and error codes</span></span>

<span data-ttu-id="4ee5c-160">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4ee5c-161">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="4ee5c-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4ee5c-162">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4ee5c-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4ee5c-163">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4ee5c-163">Response example</span></span>

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
    "Id": "<subscriptionID>",
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
