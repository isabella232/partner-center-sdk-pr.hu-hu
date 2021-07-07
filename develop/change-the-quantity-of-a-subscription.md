---
title: Egy előfizetés mennyiségének módosítása
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat az ügyfél-előfizetések licencszámának módosításakor. Ezt az irányítópulton Partnerközpont is.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d57ece4dd19ef2852f39130916222c54a9ccc85a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974097"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="388b0-104">Az ügyfél-előfizetésben szereplő licencek mennyiségének módosítása</span><span class="sxs-lookup"><span data-stu-id="388b0-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="388b0-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="388b0-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="388b0-106">Frissíti az [előfizetést](subscription-resources.md) a licencek mennyiségének növeléséhez vagy csökkentéséhez.</span><span class="sxs-lookup"><span data-stu-id="388b0-106">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="388b0-107">Az Partnerközpont irányítópulton ez a művelet úgy hajtható végre, hogy először [kiválaszt egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="388b0-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="388b0-108">Ezután válassza ki az átnevezni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="388b0-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="388b0-109">A befejezéshez módosítsa a **Quantity** (Mennyiség) mező értékét, majd válassza a Submit (Küldés) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="388b0-109">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="388b0-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="388b0-110">Prerequisites</span></span>

- <span data-ttu-id="388b0-111">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="388b0-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="388b0-112">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="388b0-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="388b0-113">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="388b0-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="388b0-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="388b0-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="388b0-115">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="388b0-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="388b0-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="388b0-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="388b0-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="388b0-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="388b0-118">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="388b0-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="388b0-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="388b0-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="388b0-120">C\#</span><span class="sxs-lookup"><span data-stu-id="388b0-120">C\#</span></span>

<span data-ttu-id="388b0-121">Az ügyfél előfizetésének mennyiségének változásához [](get-a-subscription-by-id.md)először szerezze be az előfizetést, majd módosítsa az előfizetés [**Quantity (Mennyiség) tulajdonságát.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity)</span><span class="sxs-lookup"><span data-stu-id="388b0-121">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="388b0-122">A módosítás után használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="388b0-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="388b0-123">Ezután hívja meg [**a Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid)</span><span class="sxs-lookup"><span data-stu-id="388b0-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="388b0-124">Végül hívja meg a **Patch() metódust.**</span><span class="sxs-lookup"><span data-stu-id="388b0-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="388b0-125">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="388b0-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="388b0-126">**Project:** PartnerSDK.FeatureSample **osztály:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="388b0-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="388b0-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="388b0-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="388b0-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="388b0-128">Request syntax</span></span>

| <span data-ttu-id="388b0-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="388b0-129">Method</span></span>    | <span data-ttu-id="388b0-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="388b0-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="388b0-131">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="388b0-131">**PATCH**</span></span> | <span data-ttu-id="388b0-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="388b0-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="388b0-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="388b0-133">URI parameter</span></span>

<span data-ttu-id="388b0-134">Ez a táblázat felsorolja az előfizetés mennyiségének változásához szükséges lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="388b0-134">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="388b0-135">Név</span><span class="sxs-lookup"><span data-stu-id="388b0-135">Name</span></span>                    | <span data-ttu-id="388b0-136">Típus</span><span class="sxs-lookup"><span data-stu-id="388b0-136">Type</span></span>     | <span data-ttu-id="388b0-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="388b0-137">Required</span></span> | <span data-ttu-id="388b0-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="388b0-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="388b0-139">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="388b0-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="388b0-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="388b0-140">**guid**</span></span> | <span data-ttu-id="388b0-141">Y</span><span class="sxs-lookup"><span data-stu-id="388b0-141">Y</span></span>        | <span data-ttu-id="388b0-142">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="388b0-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="388b0-143">**id-for-subscription**</span><span class="sxs-lookup"><span data-stu-id="388b0-143">**id-for-subscription**</span></span> | <span data-ttu-id="388b0-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="388b0-144">**guid**</span></span> | <span data-ttu-id="388b0-145">Y</span><span class="sxs-lookup"><span data-stu-id="388b0-145">Y</span></span>        | <span data-ttu-id="388b0-146">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="388b0-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="388b0-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="388b0-147">Request headers</span></span>

<span data-ttu-id="388b0-148">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="388b0-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="388b0-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="388b0-149">Request body</span></span>

<span data-ttu-id="388b0-150">A kérelem **törzsében** teljes előfizetési erőforrásra van szükség.</span><span class="sxs-lookup"><span data-stu-id="388b0-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="388b0-151">Győződjön meg **arról, hogy** a Quantity tulajdonság frissült.</span><span class="sxs-lookup"><span data-stu-id="388b0-151">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="388b0-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="388b0-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="388b0-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="388b0-153">REST response</span></span>

<span data-ttu-id="388b0-154">Ha ez a módszer sikeres, a **200-as HTTP-állapotkódot** és a válasz törzsében frissített előfizetési erőforrás-tulajdonságokat ad vissza. [](subscription-resources.md)</span><span class="sxs-lookup"><span data-stu-id="388b0-154">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="388b0-155">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="388b0-155">Response success and error codes</span></span>

<span data-ttu-id="388b0-156">Minden válasz egy HTTP-állapotkódot ad vissza, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="388b0-156">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="388b0-157">Egy hálózati nyomkövetési eszközzel olvassa be az állapotkódot, a hiba típusát és a további paramétereket.</span><span class="sxs-lookup"><span data-stu-id="388b0-157">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="388b0-158">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="388b0-158">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="388b0-159">Ha a javítási művelet a vártnál több időt vesz igénybe, a Partnerközpont **egy 202-es** HTTP-állapotkódot és egy helyfejlécet küld, amely az előfizetés lekérési helyére mutat.</span><span class="sxs-lookup"><span data-stu-id="388b0-159">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="388b0-160">Rendszeres időközönként lekérdezheti az előfizetést az állapot- és mennyiségváltozások figyelése érdekében.</span><span class="sxs-lookup"><span data-stu-id="388b0-160">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="388b0-161">Példák válaszra</span><span class="sxs-lookup"><span data-stu-id="388b0-161">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="388b0-162">1. válasz példa</span><span class="sxs-lookup"><span data-stu-id="388b0-162">Response example 1</span></span>

<span data-ttu-id="388b0-163">Sikeres kérés **200-as HTTP-állapotkóddal:**</span><span class="sxs-lookup"><span data-stu-id="388b0-163">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="388b0-164">2. válasz példa</span><span class="sxs-lookup"><span data-stu-id="388b0-164">Response example 2</span></span>

<span data-ttu-id="388b0-165">Sikeres kérés **202-es HTTP-állapotkóddal:**</span><span class="sxs-lookup"><span data-stu-id="388b0-165">Successful request with an **HTTP status 202** status code:</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
