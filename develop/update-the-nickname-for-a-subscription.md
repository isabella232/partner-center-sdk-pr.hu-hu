---
title: Egy előfizetés becenevének frissítése
description: Frissíti az ügyfél előfizetésének rövid nevét vagy becenevét.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 195a85fcf29b3e4c9fe0e578d4d8cb80ca068c40
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530004"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="83e28-103">Egy előfizetés becenevének frissítése</span><span class="sxs-lookup"><span data-stu-id="83e28-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="83e28-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="83e28-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="83e28-105">Frissíti az ügyfél előfizetésének rövid nevét vagy [becenevét.](subscription-resources.md)</span><span class="sxs-lookup"><span data-stu-id="83e28-105">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="83e28-106">Ez a név a Partnerközpont segít megkülönböztetni az ügyfél fiókjában az előfizetéseket.</span><span class="sxs-lookup"><span data-stu-id="83e28-106">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="83e28-107">Az Partnerközpont irányítópulton ez a művelet úgy hajtható végre, hogy először [kiválaszt egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="83e28-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="83e28-108">Ezután válassza ki az átnevezni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="83e28-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="83e28-109">A befejezéshez módosítsa a nevet az Előfizetés becenév **mezőjében,** majd válassza a Küldés **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="83e28-109">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83e28-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="83e28-110">Prerequisites</span></span>

- <span data-ttu-id="83e28-111">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="83e28-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="83e28-112">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="83e28-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="83e28-113">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="83e28-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="83e28-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="83e28-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="83e28-115">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="83e28-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="83e28-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="83e28-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="83e28-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="83e28-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="83e28-118">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="83e28-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="83e28-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="83e28-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="83e28-120">C\#</span><span class="sxs-lookup"><span data-stu-id="83e28-120">C\#</span></span>

<span data-ttu-id="83e28-121">Az ügyfél előfizetésének becenevének [](get-a-subscription-by-id.md)frissítéséhez először szerezze be az előfizetést, majd módosítsa az előfizetés [**FriendlyName tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname)</span><span class="sxs-lookup"><span data-stu-id="83e28-121">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="83e28-122">A módosítás után használja az [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="83e28-122">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="83e28-123">Ezután hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="83e28-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="83e28-124">Végül hívja meg a [**Patch() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="83e28-124">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="83e28-125">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="83e28-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="83e28-126">**Project:** PartnerSDK.FeatureSamples **osztály:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="83e28-126">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="83e28-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="83e28-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="83e28-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="83e28-128">Request syntax</span></span>

| <span data-ttu-id="83e28-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="83e28-129">Method</span></span>    | <span data-ttu-id="83e28-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="83e28-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="83e28-131">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="83e28-131">**PATCH**</span></span> | <span data-ttu-id="83e28-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="83e28-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="83e28-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="83e28-133">URI parameter</span></span>

<span data-ttu-id="83e28-134">Ez a táblázat felsorolja az előfizetés becenevének frissítéséhez szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="83e28-134">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="83e28-135">Név</span><span class="sxs-lookup"><span data-stu-id="83e28-135">Name</span></span>                    | <span data-ttu-id="83e28-136">Típus</span><span class="sxs-lookup"><span data-stu-id="83e28-136">Type</span></span>     | <span data-ttu-id="83e28-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="83e28-137">Required</span></span> | <span data-ttu-id="83e28-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="83e28-138">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="83e28-139">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="83e28-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="83e28-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="83e28-140">**guid**</span></span> | <span data-ttu-id="83e28-141">Y</span><span class="sxs-lookup"><span data-stu-id="83e28-141">Y</span></span>        | <span data-ttu-id="83e28-142">Az **ügyfél-bérlő azonosítója** (GUID).</span><span class="sxs-lookup"><span data-stu-id="83e28-142">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="83e28-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="83e28-143">**id-for-subscription**</span></span> | <span data-ttu-id="83e28-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="83e28-144">**guid**</span></span> | <span data-ttu-id="83e28-145">Y</span><span class="sxs-lookup"><span data-stu-id="83e28-145">Y</span></span>        | <span data-ttu-id="83e28-146">Az előfizetés azonosítója (GUID).</span><span class="sxs-lookup"><span data-stu-id="83e28-146">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="83e28-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="83e28-147">Request headers</span></span>

<span data-ttu-id="83e28-148">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="83e28-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="83e28-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="83e28-149">Request body</span></span>

<span data-ttu-id="83e28-150">A kérelem **törzsében** teljes előfizetési erőforrásra van szükség.</span><span class="sxs-lookup"><span data-stu-id="83e28-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="83e28-151">Győződjön meg **arról, hogy** a FriendlyName tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="83e28-151">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="83e28-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="83e28-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="83e28-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="83e28-153">REST response</span></span>

<span data-ttu-id="83e28-154">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza az előfizetés [frissített](subscription-resources.md) erőforrás-tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="83e28-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="83e28-155">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="83e28-155">Response success and error codes</span></span>

<span data-ttu-id="83e28-156">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="83e28-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="83e28-157">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="83e28-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="83e28-158">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="83e28-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="83e28-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="83e28-159">Response example</span></span>

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
