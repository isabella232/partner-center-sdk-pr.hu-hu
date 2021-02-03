---
title: Egy ügyfél előfizetéseinek lekérése a partner MPN-azonosítója alapján
description: Egy adott partner által biztosított előfizetések listájának lekérése egy adott ügyfél számára.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c95488b62449e1ab6bd2eeefea58d6686c291f4c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768348"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="90148-103">Egy ügyfél előfizetéseinek lekérése a partner MPN-azonosítója alapján</span><span class="sxs-lookup"><span data-stu-id="90148-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="90148-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="90148-104">**Applies To**</span></span>

- <span data-ttu-id="90148-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="90148-105">Partner Center</span></span>
- <span data-ttu-id="90148-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="90148-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="90148-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="90148-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="90148-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="90148-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="90148-109">Egy adott partner által biztosított előfizetések listájának lekérése egy adott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="90148-109">How to get a list of subscriptions provided by a given partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90148-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="90148-110">Prerequisites</span></span>

- <span data-ttu-id="90148-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="90148-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="90148-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="90148-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="90148-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="90148-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="90148-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="90148-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="90148-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="90148-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="90148-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="90148-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="90148-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="90148-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="90148-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="90148-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="90148-119">A partner Microsoft Partner Network (MPN) azonosítója.</span><span class="sxs-lookup"><span data-stu-id="90148-119">A partner Microsoft Partner Network (MPN) identifier.</span></span>

## <a name="c"></a><span data-ttu-id="90148-120">C\#</span><span class="sxs-lookup"><span data-stu-id="90148-120">C\#</span></span>

<span data-ttu-id="90148-121">Ha egy adott partner által megadott előfizetések listáját szeretné lekérni, először használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="90148-121">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="90148-122">Ezután szerezzen be egy felületet az ügyfél-előfizetés gyűjtési műveleteihez az [**előfizetések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) tulajdonságból, és hívja meg a [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) metódust az MPN-azonosítóval a partner azonosításához, és kérjen le egy felületet a partner előfizetési műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="90148-122">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="90148-123">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) metódust a gyűjtemény beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="90148-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="90148-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="90148-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="90148-125">**Projekt**: partner Center SDK Samples **osztály**: GetSubscriptionsByMpnid.cs</span><span class="sxs-lookup"><span data-stu-id="90148-125">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="90148-126">Java</span><span class="sxs-lookup"><span data-stu-id="90148-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="90148-127">Ha egy adott partner által biztosított előfizetések listáját szeretné lekérni egy adott ügyfél számára, először a **IAggregatePartner. getCustomers. byId** függvényt használja az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="90148-127">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="90148-128">Ezután szerezzen be egy felületet az ügyfél-előfizetés gyűjtési műveleteihez a **getSubscriptions** függvényből, és hívja meg a **byPartner** függvényt az MPN-azonosítóval a partner azonosításához, és kérjen le egy felületet a partner-előfizetési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="90148-128">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="90148-129">Végül hívja meg a **Get** függvényt a gyűjtemény beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="90148-129">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="90148-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90148-130">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="90148-131">Ha egy adott partner által megadott előfizetések listáját szeretné lekérni egy adott ügyfél számára, hajtsa végre a [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="90148-131">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="90148-132">Adja meg az ügyfél AZONOSÍTÓját, hogy azonosítsa az ügyfelet a **Vevőkód** paraméterrel, majd töltse fel a **MpnId** paramétert az MPN-azonosítóval a partner azonosításához.</span><span class="sxs-lookup"><span data-stu-id="90148-132">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="90148-133">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="90148-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="90148-134">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="90148-134">Request syntax</span></span>

| <span data-ttu-id="90148-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="90148-135">Method</span></span>  | <span data-ttu-id="90148-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="90148-136">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="90148-137">**GET**</span><span class="sxs-lookup"><span data-stu-id="90148-137">**GET**</span></span> | <span data-ttu-id="90148-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions? MPN \_ -azonosító = {MPN-azonosító} http/1.1</span><span class="sxs-lookup"><span data-stu-id="90148-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="90148-139">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="90148-139">URI parameters</span></span>

<span data-ttu-id="90148-140">Az ügyfél és a partner azonosításához használja a következő elérési utat és a lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="90148-140">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="90148-141">Név</span><span class="sxs-lookup"><span data-stu-id="90148-141">Name</span></span>        | <span data-ttu-id="90148-142">Típus</span><span class="sxs-lookup"><span data-stu-id="90148-142">Type</span></span>   | <span data-ttu-id="90148-143">Kötelező</span><span class="sxs-lookup"><span data-stu-id="90148-143">Required</span></span> | <span data-ttu-id="90148-144">Leírás</span><span class="sxs-lookup"><span data-stu-id="90148-144">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="90148-145">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="90148-145">customer-id</span></span> | <span data-ttu-id="90148-146">sztring</span><span class="sxs-lookup"><span data-stu-id="90148-146">string</span></span> | <span data-ttu-id="90148-147">Igen</span><span class="sxs-lookup"><span data-stu-id="90148-147">Yes</span></span>      | <span data-ttu-id="90148-148">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="90148-148">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="90148-149">MPN-azonosító</span><span class="sxs-lookup"><span data-stu-id="90148-149">mpn-id</span></span>      | <span data-ttu-id="90148-150">int</span><span class="sxs-lookup"><span data-stu-id="90148-150">int</span></span>    | <span data-ttu-id="90148-151">Igen</span><span class="sxs-lookup"><span data-stu-id="90148-151">Yes</span></span>      | <span data-ttu-id="90148-152">A partnert azonosító Microsoft Partner Network-azonosító.</span><span class="sxs-lookup"><span data-stu-id="90148-152">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="90148-153">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="90148-153">Request headers</span></span>

<span data-ttu-id="90148-154">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="90148-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="90148-155">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="90148-155">Request body</span></span>

<span data-ttu-id="90148-156">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="90148-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="90148-157">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="90148-157">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="90148-158">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="90148-158">REST response</span></span>

<span data-ttu-id="90148-159">Ha ez sikeres, a válasz törzse tartalmazza az [előfizetés](subscription-resources.md) erőforrásainak gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="90148-159">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="90148-160">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="90148-160">Response success and error codes</span></span>

<span data-ttu-id="90148-161">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="90148-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="90148-162">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="90148-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="90148-163">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="90148-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="90148-164">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="90148-164">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="90148-165">Lásd még</span><span class="sxs-lookup"><span data-stu-id="90148-165">See also</span></span>

- [<span data-ttu-id="90148-166">Partnerközpont-elemzések – forrásanyagok</span><span class="sxs-lookup"><span data-stu-id="90148-166">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
