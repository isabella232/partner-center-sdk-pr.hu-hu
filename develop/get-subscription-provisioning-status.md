---
title: Előfizetés kiépítési állapotának lekérése
description: Hogyan lehet lekérte az előfizetés kiépítési állapotát egy ügyfél-előfizetéshez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8797fa494cd77f11a1179d6406ca021f0d7788c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548702"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="73d6b-103">Előfizetés kiépítési állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="73d6b-103">Get subscription provisioning status</span></span>

<span data-ttu-id="73d6b-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="73d6b-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="73d6b-105">Hogyan lehet lekérte az előfizetés kiépítési állapotát egy ügyfél-előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="73d6b-105">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73d6b-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="73d6b-106">Prerequisites</span></span>

- <span data-ttu-id="73d6b-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="73d6b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="73d6b-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="73d6b-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="73d6b-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73d6b-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="73d6b-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="73d6b-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="73d6b-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="73d6b-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="73d6b-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="73d6b-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="73d6b-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="73d6b-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="73d6b-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="73d6b-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="73d6b-115">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="73d6b-115">A subscription identifier.</span></span>

- <span data-ttu-id="73d6b-116">A művelet végrehajtásához delegált rendszergazdai engedélyek szükségesek az előfizetésen.</span><span class="sxs-lookup"><span data-stu-id="73d6b-116">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="73d6b-117">C\#</span><span class="sxs-lookup"><span data-stu-id="73d6b-117">C\#</span></span>

<span data-ttu-id="73d6b-118">Az előfizetés kiépítési állapotának lehöz először használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="73d6b-118">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="73d6b-119">Ezután az előfizetési műveletek interfészének lehívásához hívja meg a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust az előfizetés azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="73d6b-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="73d6b-120">Ezután a [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) tulajdonság használatával szerezzen be egy felületet az aktuális előfizetés kiépítési állapotműveletéhez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) metódust a [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="73d6b-120">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="73d6b-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="73d6b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="73d6b-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="73d6b-122">Request syntax</span></span>

| <span data-ttu-id="73d6b-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="73d6b-123">Method</span></span>  | <span data-ttu-id="73d6b-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="73d6b-124">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="73d6b-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="73d6b-125">**GET**</span></span> | <span data-ttu-id="73d6b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/provisioningstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="73d6b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="73d6b-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="73d6b-127">URI parameters</span></span>

<span data-ttu-id="73d6b-128">Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="73d6b-128">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="73d6b-129">Név</span><span class="sxs-lookup"><span data-stu-id="73d6b-129">Name</span></span>            | <span data-ttu-id="73d6b-130">Típus</span><span class="sxs-lookup"><span data-stu-id="73d6b-130">Type</span></span>   | <span data-ttu-id="73d6b-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="73d6b-131">Required</span></span> | <span data-ttu-id="73d6b-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="73d6b-132">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="73d6b-133">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="73d6b-133">customer-id</span></span>     | <span data-ttu-id="73d6b-134">sztring</span><span class="sxs-lookup"><span data-stu-id="73d6b-134">string</span></span> | <span data-ttu-id="73d6b-135">Igen</span><span class="sxs-lookup"><span data-stu-id="73d6b-135">Yes</span></span>      | <span data-ttu-id="73d6b-136">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="73d6b-136">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="73d6b-137">subscription-id (előfizetés-azonosító)</span><span class="sxs-lookup"><span data-stu-id="73d6b-137">subscription-id</span></span> | <span data-ttu-id="73d6b-138">sztring</span><span class="sxs-lookup"><span data-stu-id="73d6b-138">string</span></span> | <span data-ttu-id="73d6b-139">Igen</span><span class="sxs-lookup"><span data-stu-id="73d6b-139">Yes</span></span>      | <span data-ttu-id="73d6b-140">Egy GUID formátumú sztring, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="73d6b-140">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="73d6b-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="73d6b-141">Request headers</span></span>

<span data-ttu-id="73d6b-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="73d6b-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="73d6b-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="73d6b-143">Request body</span></span>

<span data-ttu-id="73d6b-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="73d6b-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="73d6b-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="73d6b-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="73d6b-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="73d6b-146">REST response</span></span>

<span data-ttu-id="73d6b-147">Ha ez sikeres, a válasz törzse tartalmaz egy [SubscriptionProvisioningStatus erőforrást.](subscription-resources.md#subscriptionprovisioningstatus)</span><span class="sxs-lookup"><span data-stu-id="73d6b-147">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="73d6b-148">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="73d6b-148">Response success and error codes</span></span>

<span data-ttu-id="73d6b-149">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="73d6b-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="73d6b-150">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="73d6b-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="73d6b-151">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="73d6b-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="73d6b-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="73d6b-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a><span data-ttu-id="73d6b-153">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="73d6b-153">Remarks</span></span>

- <span data-ttu-id="73d6b-154">Licenc módosításakor a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) állapotmezője "pending" (függőben) lesz.</span><span class="sxs-lookup"><span data-stu-id="73d6b-154">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="73d6b-155">Az állapot mező 15 percenként frissül.</span><span class="sxs-lookup"><span data-stu-id="73d6b-155">The status field is updated every 15 minutes.</span></span>
