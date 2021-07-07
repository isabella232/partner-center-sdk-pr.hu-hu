---
title: Egy ügyfél előfizetéseinek lekérése a partner MPN-azonosítója alapján
description: Egy adott partner által megadott előfizetések listájának lekérte egy adott ügyfélnek.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 857caa667245503f111b27379a5c8f93aa1fb0b0
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760657"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="80f51-103">Egy ügyfél előfizetéseinek lekérése a partner MPN-azonosítója alapján</span><span class="sxs-lookup"><span data-stu-id="80f51-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="80f51-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="80f51-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="80f51-105">Egy adott ügyfél (MPN) partner által biztosított előfizetések listájának Microsoft Partner Network adott ügyfélnek.</span><span class="sxs-lookup"><span data-stu-id="80f51-105">How to get a list of subscriptions provided by a given Microsoft Partner Network (MPN) partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80f51-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="80f51-106">Prerequisites</span></span>

- <span data-ttu-id="80f51-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="80f51-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80f51-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="80f51-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="80f51-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80f51-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80f51-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="80f51-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80f51-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="80f51-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80f51-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="80f51-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80f51-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="80f51-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80f51-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80f51-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="80f51-115">Egy partner MPN-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="80f51-115">A partner MPN identifier.</span></span>

## <a name="c"></a><span data-ttu-id="80f51-116">C\#</span><span class="sxs-lookup"><span data-stu-id="80f51-116">C\#</span></span>

<span data-ttu-id="80f51-117">Ha egy adott partner által megadott előfizetések listáját le kell kapnia egy adott ügyfélnek, először használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="80f51-117">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="80f51-118">Ezután szerezze be az ügyfél-előfizetések gyűjtési műveleteinek interfészét az [**Előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságból, és hívja meg a [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) metódust az MPN-azonosítóval a partner azonosításához és a partner-előfizetési műveletek interfészének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="80f51-118">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="80f51-119">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) vagy [**GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) a gyűjtemény lehíváshoz.</span><span class="sxs-lookup"><span data-stu-id="80f51-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="80f51-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="80f51-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80f51-121">**Project**: Partnerközpont SDK **Osztály:** GetSubscriptionsByMpnid.cs</span><span class="sxs-lookup"><span data-stu-id="80f51-121">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="80f51-122">Java</span><span class="sxs-lookup"><span data-stu-id="80f51-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="80f51-123">Ha egy adott partner által megadott előfizetések listáját le kell kapnia egy adott ügyfélnek, először használja az **IAggregatePartner.getCustomers.byId** függvényt az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="80f51-123">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="80f51-124">Ezután szerezze be az ügyfél-előfizetések gyűjtési műveleteinek interfészét a **getSubscriptions** függvényből, és hívja meg a **byPartner** függvényt az MPN-azonosítóval a partner azonosításához és a partner-előfizetési műveletek interfészének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="80f51-124">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="80f51-125">Végül hívja meg a **get** függvényt a gyűjtemény lehívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="80f51-125">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="80f51-126">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80f51-126">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="80f51-127">Ha le kell kapnia egy adott partner által egy adott ügyfélnek biztosított előfizetések listáját, hajtsa végre a [**Get-PartnerCustomerSubscription parancsot.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md)</span><span class="sxs-lookup"><span data-stu-id="80f51-127">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="80f51-128">Adja meg az ügyfél-azonosítót, amely a **CustomerId** paraméterrel azonosítja az ügyfelet, majd töltse fel az **MpnId** paramétert az MPN-azonosítóval a partner azonosításához.</span><span class="sxs-lookup"><span data-stu-id="80f51-128">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="80f51-129">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="80f51-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80f51-130">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="80f51-130">Request syntax</span></span>

| <span data-ttu-id="80f51-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="80f51-131">Method</span></span>  | <span data-ttu-id="80f51-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="80f51-132">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80f51-133">**Kap**</span><span class="sxs-lookup"><span data-stu-id="80f51-133">**GET**</span></span> | <span data-ttu-id="80f51-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/előfizetések?mpn \_ id={mpn-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="80f51-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="80f51-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="80f51-135">URI parameters</span></span>

<span data-ttu-id="80f51-136">Az ügyfél és a partner azonosításához használja az alábbi elérési utat és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="80f51-136">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="80f51-137">Név</span><span class="sxs-lookup"><span data-stu-id="80f51-137">Name</span></span>        | <span data-ttu-id="80f51-138">Típus</span><span class="sxs-lookup"><span data-stu-id="80f51-138">Type</span></span>   | <span data-ttu-id="80f51-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="80f51-139">Required</span></span> | <span data-ttu-id="80f51-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="80f51-140">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="80f51-141">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="80f51-141">customer-id</span></span> | <span data-ttu-id="80f51-142">sztring</span><span class="sxs-lookup"><span data-stu-id="80f51-142">string</span></span> | <span data-ttu-id="80f51-143">Igen</span><span class="sxs-lookup"><span data-stu-id="80f51-143">Yes</span></span>      | <span data-ttu-id="80f51-144">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="80f51-144">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="80f51-145">mpn-id</span><span class="sxs-lookup"><span data-stu-id="80f51-145">mpn-id</span></span>      | <span data-ttu-id="80f51-146">int</span><span class="sxs-lookup"><span data-stu-id="80f51-146">int</span></span>    | <span data-ttu-id="80f51-147">Igen</span><span class="sxs-lookup"><span data-stu-id="80f51-147">Yes</span></span>      | <span data-ttu-id="80f51-148">A Microsoft Partner Network azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="80f51-148">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80f51-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="80f51-149">Request headers</span></span>

<span data-ttu-id="80f51-150">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="80f51-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80f51-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="80f51-151">Request body</span></span>

<span data-ttu-id="80f51-152">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="80f51-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="80f51-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="80f51-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="80f51-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="80f51-154">REST response</span></span>

<span data-ttu-id="80f51-155">Ha a művelet sikeres, a válasz törzse tartalmazza az előfizetési [erőforrások gyűjteményét.](subscription-resources.md)</span><span class="sxs-lookup"><span data-stu-id="80f51-155">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80f51-156">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="80f51-156">Response success and error codes</span></span>

<span data-ttu-id="80f51-157">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="80f51-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80f51-158">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="80f51-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80f51-159">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="80f51-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80f51-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="80f51-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a><span data-ttu-id="80f51-161">Lásd még</span><span class="sxs-lookup"><span data-stu-id="80f51-161">See also</span></span>

- [<span data-ttu-id="80f51-162">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="80f51-162">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
