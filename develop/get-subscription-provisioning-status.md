---
title: Előfizetés kiépítési állapotának lekérése
description: Az előfizetés kiépítési állapotának lekérése egy ügyfél-előfizetéshez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38544aa380ba0a6a8804ae45f7d8ae7cb431d3ba
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768436"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="2ffdf-103">Előfizetés kiépítési állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="2ffdf-103">Get subscription provisioning status</span></span>

<span data-ttu-id="2ffdf-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="2ffdf-104">**Applies To**</span></span>

- <span data-ttu-id="2ffdf-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="2ffdf-105">Partner Center</span></span>
- <span data-ttu-id="2ffdf-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="2ffdf-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2ffdf-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2ffdf-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2ffdf-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2ffdf-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2ffdf-109">Az előfizetés kiépítési állapotának lekérése egy ügyfél-előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-109">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ffdf-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2ffdf-110">Prerequisites</span></span>

- <span data-ttu-id="2ffdf-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2ffdf-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2ffdf-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2ffdf-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2ffdf-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2ffdf-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2ffdf-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2ffdf-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2ffdf-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2ffdf-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2ffdf-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2ffdf-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-119">A subscription identifier.</span></span>

- <span data-ttu-id="2ffdf-120">A művelet végrehajtásához delegált rendszergazdai engedélyek szükségesek az előfizetéshez.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-120">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="2ffdf-121">C\#</span><span class="sxs-lookup"><span data-stu-id="2ffdf-121">C\#</span></span>

<span data-ttu-id="2ffdf-122">Az előfizetés kiépítési állapotának lekéréséhez először a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust használja az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-122">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="2ffdf-123">Ezután kérjen meg egy illesztőfelületet az előfizetési műveletekhez az [**előfizetések. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus meghívásával az előfizetés-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-123">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="2ffdf-124">Ezután a [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) tulajdonsággal szerezzen be egy felületet az aktuális előfizetés kiépítési állapotának műveleteihez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) metódust a [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-124">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="2ffdf-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="2ffdf-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2ffdf-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2ffdf-126">Request syntax</span></span>

| <span data-ttu-id="2ffdf-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="2ffdf-127">Method</span></span>  | <span data-ttu-id="2ffdf-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2ffdf-128">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ffdf-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="2ffdf-129">**GET**</span></span> | <span data-ttu-id="2ffdf-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/provisioningstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="2ffdf-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="2ffdf-131">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="2ffdf-131">URI parameters</span></span>

<span data-ttu-id="2ffdf-132">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="2ffdf-133">Név</span><span class="sxs-lookup"><span data-stu-id="2ffdf-133">Name</span></span>            | <span data-ttu-id="2ffdf-134">Típus</span><span class="sxs-lookup"><span data-stu-id="2ffdf-134">Type</span></span>   | <span data-ttu-id="2ffdf-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2ffdf-135">Required</span></span> | <span data-ttu-id="2ffdf-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="2ffdf-136">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="2ffdf-137">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="2ffdf-137">customer-id</span></span>     | <span data-ttu-id="2ffdf-138">sztring</span><span class="sxs-lookup"><span data-stu-id="2ffdf-138">string</span></span> | <span data-ttu-id="2ffdf-139">Igen</span><span class="sxs-lookup"><span data-stu-id="2ffdf-139">Yes</span></span>      | <span data-ttu-id="2ffdf-140">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-140">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="2ffdf-141">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="2ffdf-141">subscription-id</span></span> | <span data-ttu-id="2ffdf-142">sztring</span><span class="sxs-lookup"><span data-stu-id="2ffdf-142">string</span></span> | <span data-ttu-id="2ffdf-143">Igen</span><span class="sxs-lookup"><span data-stu-id="2ffdf-143">Yes</span></span>      | <span data-ttu-id="2ffdf-144">Egy GUID formátumú karakterlánc, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-144">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2ffdf-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2ffdf-145">Request headers</span></span>

<span data-ttu-id="2ffdf-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2ffdf-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2ffdf-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2ffdf-147">Request body</span></span>

<span data-ttu-id="2ffdf-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2ffdf-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2ffdf-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2ffdf-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2ffdf-150">REST response</span></span>

<span data-ttu-id="2ffdf-151">Ha ez sikeres, a válasz törzse [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-151">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2ffdf-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2ffdf-152">Response success and error codes</span></span>

<span data-ttu-id="2ffdf-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2ffdf-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2ffdf-155">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2ffdf-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2ffdf-156">Response example</span></span>

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

## <a name="remarks"></a><span data-ttu-id="2ffdf-157">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="2ffdf-157">Remarks</span></span>

- <span data-ttu-id="2ffdf-158">A licenc módosításakor a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) állapot mezőjében a "függő" értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-158">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="2ffdf-159">Az állapot mező tizenöt percenként frissül.</span><span class="sxs-lookup"><span data-stu-id="2ffdf-159">The status field is updated every fifteen minutes.</span></span>
