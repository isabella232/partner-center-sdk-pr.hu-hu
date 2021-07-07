---
title: Előfizetés regisztrációs állapotának lekérése
description: Le kell kapnia egy előfizetés állapotát, amely regisztrálva van a Azure Reserved VM Instances.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e39f94c0eac402a0be3afde84279aa637868f96
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445952"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="87901-103">Előfizetés regisztrációs állapotának lekérése</span><span class="sxs-lookup"><span data-stu-id="87901-103">Get subscription registration status</span></span>

<span data-ttu-id="87901-104">Hogyan lehet lekérte az előfizetés regisztrációs állapotát egy olyan ügyfél-előfizetéshez, amely számára engedélyezett a Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="87901-104">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="87901-105">Ha azure-beli fenntartott virtuálisgép-példányt a Partnerközpont API-val vásárolni, legalább egy meglévő CSP Azure-előfizetéssel kell lennie.</span><span class="sxs-lookup"><span data-stu-id="87901-105">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="87901-106">Az [Előfizetés regisztrálása](register-a-subscription.md) módszerrel regisztrálhatja meglévő CSP Azure-előfizetését, így megvásárolhatja Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="87901-106">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="87901-107">Ezzel a módszerrel lekérhető a regisztráció állapota.</span><span class="sxs-lookup"><span data-stu-id="87901-107">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87901-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="87901-108">Prerequisites</span></span>

- <span data-ttu-id="87901-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="87901-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="87901-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="87901-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="87901-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="87901-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="87901-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="87901-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="87901-113">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="87901-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="87901-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="87901-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="87901-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="87901-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="87901-116">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="87901-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="87901-117">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="87901-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="87901-118">C\#</span><span class="sxs-lookup"><span data-stu-id="87901-118">C\#</span></span>

<span data-ttu-id="87901-119">Az előfizetés regisztrációs állapotának leához először használja az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="87901-119">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="87901-120">Ezután szerezze be az előfizetési műveletek interfészét a [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódus az előfizetés azonosítójával való hívásával az előfizetés azonosításához.</span><span class="sxs-lookup"><span data-stu-id="87901-120">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="87901-121">Ezután a RegistrationStatus tulajdonság használatával szerezze be az aktuális előfizetés regisztrációs állapotműveletei interfészét, és hívja meg a **Get** vagy **GetAsync** metódust a **SubscriptionRegistrationStatus** objektum lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="87901-121">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="87901-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="87901-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="87901-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="87901-123">Request syntax</span></span>

| <span data-ttu-id="87901-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="87901-124">Method</span></span>    | <span data-ttu-id="87901-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="87901-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="87901-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="87901-126">**GET**</span></span>  | <span data-ttu-id="87901-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/registrationstatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="87901-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="87901-128">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="87901-128">URI parameters</span></span>

<span data-ttu-id="87901-129">Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="87901-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="87901-130">Név</span><span class="sxs-lookup"><span data-stu-id="87901-130">Name</span></span>                    | <span data-ttu-id="87901-131">Típus</span><span class="sxs-lookup"><span data-stu-id="87901-131">Type</span></span>       | <span data-ttu-id="87901-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="87901-132">Required</span></span> | <span data-ttu-id="87901-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="87901-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="87901-134">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="87901-134">customer-id</span></span>             | <span data-ttu-id="87901-135">sztring</span><span class="sxs-lookup"><span data-stu-id="87901-135">string</span></span>     | <span data-ttu-id="87901-136">Igen</span><span class="sxs-lookup"><span data-stu-id="87901-136">Yes</span></span>      | <span data-ttu-id="87901-137">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="87901-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="87901-138">subscription-id</span><span class="sxs-lookup"><span data-stu-id="87901-138">subscription-id</span></span>         | <span data-ttu-id="87901-139">sztring</span><span class="sxs-lookup"><span data-stu-id="87901-139">string</span></span>     | <span data-ttu-id="87901-140">Igen</span><span class="sxs-lookup"><span data-stu-id="87901-140">Yes</span></span>      | <span data-ttu-id="87901-141">Egy GUID formátumú sztring, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="87901-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="87901-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="87901-142">Request headers</span></span>

<span data-ttu-id="87901-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="87901-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="87901-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="87901-144">Request body</span></span>

<span data-ttu-id="87901-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="87901-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="87901-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="87901-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="87901-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="87901-147">REST response</span></span>

<span data-ttu-id="87901-148">Ha a művelet sikeres, a válasz törzse tartalmaz egy [SubscriptionRegistrationStatus erőforrást.](subscription-resources.md#subscriptionregistrationstatus)</span><span class="sxs-lookup"><span data-stu-id="87901-148">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="87901-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="87901-149">Response success and error codes</span></span>

<span data-ttu-id="87901-150">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="87901-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="87901-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="87901-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="87901-152">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="87901-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="87901-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="87901-153">Response example</span></span>

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
