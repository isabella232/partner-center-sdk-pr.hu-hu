---
title: Egy előfizetés mennyiségének módosítása
description: Ismerje meg, hogyan módosíthatja az ügyfél-előfizetések licenceit a partner Center API-k használatával. Ezt a partner Center irányítópultján is megteheti.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768588"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="c8101-104">Az ügyfél-előfizetésben lévő licencek mennyiségének módosítása</span><span class="sxs-lookup"><span data-stu-id="c8101-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="c8101-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="c8101-105">**Applies to:**</span></span>

- <span data-ttu-id="c8101-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c8101-106">Partner Center</span></span>
- <span data-ttu-id="c8101-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="c8101-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c8101-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c8101-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c8101-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c8101-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c8101-110">Frissíti az [előfizetést](subscription-resources.md) a licencek mennyiségének növeléséhez vagy csökkentéséhez.</span><span class="sxs-lookup"><span data-stu-id="c8101-110">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="c8101-111">A partner Center irányítópultján ezt a műveletet a [felhasználó kiválasztásával](get-a-customer-by-name.md)végezheti el.</span><span class="sxs-lookup"><span data-stu-id="c8101-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="c8101-112">Ezután válassza ki az átnevezni kívánt előfizetést.</span><span class="sxs-lookup"><span data-stu-id="c8101-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="c8101-113">A befejezéshez módosítsa a **mennyiség** mező értékét, majd válassza a **Küldés lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="c8101-113">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8101-114">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c8101-114">Prerequisites</span></span>

- <span data-ttu-id="c8101-115">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c8101-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c8101-116">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="c8101-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c8101-117">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8101-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c8101-118">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="c8101-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c8101-119">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="c8101-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c8101-120">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="c8101-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c8101-121">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="c8101-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c8101-122">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8101-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c8101-123">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="c8101-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="c8101-124">C\#</span><span class="sxs-lookup"><span data-stu-id="c8101-124">C\#</span></span>

<span data-ttu-id="c8101-125">Ha módosítani szeretné az ügyfél előfizetésének mennyiségét, először [szerezze be az előfizetést](get-a-subscription-by-id.md), majd módosítsa az előfizetés [**mennyiségi**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="c8101-125">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="c8101-126">A módosítást követően használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="c8101-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="c8101-127">Ezután hívja meg az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságot, majd a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="c8101-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="c8101-128">Ezután fejezze be a **Patch ()** metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="c8101-128">Then, finish by calling the **Patch()** method.</span></span>

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

<span data-ttu-id="c8101-129">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c8101-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c8101-130">**Projekt**: PartnerSDK. FeatureSample **osztály**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="c8101-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c8101-131">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c8101-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c8101-132">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c8101-132">Request syntax</span></span>

| <span data-ttu-id="c8101-133">Metódus</span><span class="sxs-lookup"><span data-stu-id="c8101-133">Method</span></span>    | <span data-ttu-id="c8101-134">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c8101-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c8101-135">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="c8101-135">**PATCH**</span></span> | <span data-ttu-id="c8101-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c8101-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c8101-137">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c8101-137">URI parameter</span></span>

<span data-ttu-id="c8101-138">Ez a táblázat felsorolja a szükséges lekérdezési paramétert az előfizetés mennyiségének módosításához.</span><span class="sxs-lookup"><span data-stu-id="c8101-138">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="c8101-139">Név</span><span class="sxs-lookup"><span data-stu-id="c8101-139">Name</span></span>                    | <span data-ttu-id="c8101-140">Típus</span><span class="sxs-lookup"><span data-stu-id="c8101-140">Type</span></span>     | <span data-ttu-id="c8101-141">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c8101-141">Required</span></span> | <span data-ttu-id="c8101-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="c8101-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="c8101-143">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="c8101-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="c8101-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="c8101-144">**guid**</span></span> | <span data-ttu-id="c8101-145">Y</span><span class="sxs-lookup"><span data-stu-id="c8101-145">Y</span></span>        | <span data-ttu-id="c8101-146">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="c8101-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="c8101-147">**azonosító – előfizetés**</span><span class="sxs-lookup"><span data-stu-id="c8101-147">**id-for-subscription**</span></span> | <span data-ttu-id="c8101-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="c8101-148">**guid**</span></span> | <span data-ttu-id="c8101-149">Y</span><span class="sxs-lookup"><span data-stu-id="c8101-149">Y</span></span>        | <span data-ttu-id="c8101-150">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="c8101-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c8101-151">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c8101-151">Request headers</span></span>

<span data-ttu-id="c8101-152">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c8101-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c8101-153">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c8101-153">Request body</span></span>

<span data-ttu-id="c8101-154">A kérelem törzsében teljes **előfizetési** erőforrás szükséges.</span><span class="sxs-lookup"><span data-stu-id="c8101-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="c8101-155">Győződjön meg arról, hogy a **mennyiségi** tulajdonság frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="c8101-155">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="c8101-156">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c8101-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c8101-157">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c8101-157">REST response</span></span>

<span data-ttu-id="c8101-158">Ha ez sikeres, a metódus egy **200-as http-állapotot** ad vissza, és frissítette az [előfizetési erőforrás](subscription-resources.md)  tulajdonságait a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="c8101-158">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c8101-159">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c8101-159">Response success and error codes</span></span>

<span data-ttu-id="c8101-160">Minden válasz egy HTTP-állapotkódot ad vissza, amely a sikeres vagy sikertelen műveletekre és a további hibakeresési információkra utal.</span><span class="sxs-lookup"><span data-stu-id="c8101-160">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c8101-161">Hálózati nyomkövetési eszköz használata az állapotkód, a hiba típusa és a további paraméterek olvasásához.</span><span class="sxs-lookup"><span data-stu-id="c8101-161">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="c8101-162">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c8101-162">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="c8101-163">Ha a javítási művelet a várt időpontnál hosszabb időt vesz igénybe, a partner Center egy 202-as **http-állapotot** küld, és egy olyan hely fejlécét, amely az előfizetés lekérésének helyét mutat.</span><span class="sxs-lookup"><span data-stu-id="c8101-163">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="c8101-164">Rendszeres időközönként lekérdezheti az előfizetést az állapot és a mennyiség változásának figyeléséhez.</span><span class="sxs-lookup"><span data-stu-id="c8101-164">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="c8101-165">Példák a válaszokra</span><span class="sxs-lookup"><span data-stu-id="c8101-165">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="c8101-166">1. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="c8101-166">Response example 1</span></span>

<span data-ttu-id="c8101-167">Sikeres kérelem http- **állapottal 200** -as állapotkód esetén:</span><span class="sxs-lookup"><span data-stu-id="c8101-167">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="c8101-168">2. válasz – példa</span><span class="sxs-lookup"><span data-stu-id="c8101-168">Response example 2</span></span>

<span data-ttu-id="c8101-169">Sikeres kérelem http- **állapottal 202** -as állapotkód esetén:</span><span class="sxs-lookup"><span data-stu-id="c8101-169">Successful request with an **HTTP status 202** status code:</span></span>

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
