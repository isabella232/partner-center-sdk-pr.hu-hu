---
title: Előfizetés regisztrációs állapotának lekérése
description: Lekéri egy olyan előfizetés állapotát, amely regisztrálva van a Azure Reserved VM Instancessal való használatra.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768440"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="11924-103">Előfizetés regisztrációs állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="11924-103">Get subscription registration status</span></span>

<span data-ttu-id="11924-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="11924-104">**Applies To**</span></span>

- <span data-ttu-id="11924-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="11924-105">Partner Center</span></span>

<span data-ttu-id="11924-106">Az előfizetés regisztrációs állapotának beszerzése olyan ügyfél-előfizetéshez, amely engedélyezve van a Azure Reserved VM Instances megvásárlására.</span><span class="sxs-lookup"><span data-stu-id="11924-106">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="11924-107">Ha egy Azure-beli fenntartott VM-példányt szeretne megvásárolni a partner Center API-val, rendelkeznie kell legalább egy meglévő CSP Azure-előfizetéssel.</span><span class="sxs-lookup"><span data-stu-id="11924-107">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="11924-108">Az [előfizetés regisztrálása](register-a-subscription.md) lehetővé teszi a meglévő CSP Azure-előfizetés regisztrálását, amely lehetővé teszi a Azure Reserved VM instances megvásárlását.</span><span class="sxs-lookup"><span data-stu-id="11924-108">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="11924-109">Ez a módszer lehetővé teszi az adott regisztráció állapotának beolvasását.</span><span class="sxs-lookup"><span data-stu-id="11924-109">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11924-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="11924-110">Prerequisites</span></span>

- <span data-ttu-id="11924-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="11924-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="11924-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="11924-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="11924-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="11924-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="11924-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="11924-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="11924-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="11924-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="11924-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="11924-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="11924-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="11924-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="11924-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="11924-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="11924-119">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="11924-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="11924-120">C\#</span><span class="sxs-lookup"><span data-stu-id="11924-120">C\#</span></span>

<span data-ttu-id="11924-121">Az előfizetés regisztrációs állapotának lekéréséhez először a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust használja az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="11924-121">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="11924-122">Ezután szerezzen be egy illesztőfelületet az előfizetési műveletekhez úgy, hogy meghívja az előfizetés [**. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust az előfizetés-azonosítóval az előfizetés azonosításához.</span><span class="sxs-lookup"><span data-stu-id="11924-122">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="11924-123">Ezután a RegistrationStatus tulajdonsággal szerezzen be egy felületet az aktuális előfizetés regisztrációs állapotára vonatkozó műveletekhez, és hívja meg a **Get** vagy a **GetAsync** metódust a **SubscriptionRegistrationStatus** objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="11924-123">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="11924-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="11924-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="11924-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="11924-125">Request syntax</span></span>

| <span data-ttu-id="11924-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="11924-126">Method</span></span>    | <span data-ttu-id="11924-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="11924-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="11924-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="11924-128">**GET**</span></span>  | <span data-ttu-id="11924-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrationstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="11924-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="11924-130">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="11924-130">URI parameters</span></span>

<span data-ttu-id="11924-131">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="11924-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="11924-132">Név</span><span class="sxs-lookup"><span data-stu-id="11924-132">Name</span></span>                    | <span data-ttu-id="11924-133">Típus</span><span class="sxs-lookup"><span data-stu-id="11924-133">Type</span></span>       | <span data-ttu-id="11924-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="11924-134">Required</span></span> | <span data-ttu-id="11924-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="11924-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="11924-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="11924-136">customer-id</span></span>             | <span data-ttu-id="11924-137">sztring</span><span class="sxs-lookup"><span data-stu-id="11924-137">string</span></span>     | <span data-ttu-id="11924-138">Igen</span><span class="sxs-lookup"><span data-stu-id="11924-138">Yes</span></span>      | <span data-ttu-id="11924-139">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="11924-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="11924-140">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="11924-140">subscription-id</span></span>         | <span data-ttu-id="11924-141">sztring</span><span class="sxs-lookup"><span data-stu-id="11924-141">string</span></span>     | <span data-ttu-id="11924-142">Igen</span><span class="sxs-lookup"><span data-stu-id="11924-142">Yes</span></span>      | <span data-ttu-id="11924-143">Egy GUID formátumú karakterlánc, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="11924-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="11924-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="11924-144">Request headers</span></span>

<span data-ttu-id="11924-145">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="11924-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="11924-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="11924-146">Request body</span></span>

<span data-ttu-id="11924-147">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="11924-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="11924-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="11924-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="11924-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="11924-149">REST response</span></span>

<span data-ttu-id="11924-150">Ha ez sikeres, a válasz törzse [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) -erőforrást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="11924-150">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="11924-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="11924-151">Response success and error codes</span></span>

<span data-ttu-id="11924-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="11924-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="11924-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="11924-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="11924-154">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="11924-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="11924-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="11924-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
