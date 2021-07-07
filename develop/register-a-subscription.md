---
title: Előfizetés regisztrálása
description: Regisztráljon egy meglévő előfizetést, hogy engedélyezve legyen az Azure Reservations megrendelése.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d26a7c77f60e6ef817cde80b9e97c88bd8bdc786
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446615"
---
# <a name="register-a-subscription"></a><span data-ttu-id="b8303-103">Előfizetés regisztrálása</span><span class="sxs-lookup"><span data-stu-id="b8303-103">Register a subscription</span></span>

<span data-ttu-id="b8303-104">Regisztráljon egy meglévő [előfizetést,](subscription-resources.md) hogy engedélyezve legyen az Azure Reservations megrendelése.</span><span class="sxs-lookup"><span data-stu-id="b8303-104">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="b8303-105">Azure-foglalás vásárlásához legalább egy meglévő CSP Azure-előfizetéssel kell lennie.</span><span class="sxs-lookup"><span data-stu-id="b8303-105">To purchase an Azure reservation, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="b8303-106">Ezzel a módszerrel regisztrálhatja meglévő CSP Azure-előfizetését, így azure-foglalásokat is megvásárolhat.</span><span class="sxs-lookup"><span data-stu-id="b8303-106">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8303-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b8303-107">Prerequisites</span></span>

- <span data-ttu-id="b8303-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b8303-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b8303-109">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="b8303-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b8303-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b8303-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b8303-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b8303-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b8303-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b8303-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b8303-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b8303-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b8303-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="b8303-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b8303-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b8303-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b8303-116">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="b8303-116">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="b8303-117">C\#</span><span class="sxs-lookup"><span data-stu-id="b8303-117">C\#</span></span>

<span data-ttu-id="b8303-118">Az ügyfél előfizetésének regisztrálásához az ügyfél azonosításához hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy lekérje az előfizetési műveletek felületét.</span><span class="sxs-lookup"><span data-stu-id="b8303-118">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b8303-119">Ezután hívja meg a [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust az előfizetés azonosítójával a regisztrálni használt előfizetés azonosításához.</span><span class="sxs-lookup"><span data-stu-id="b8303-119">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="b8303-120">Végül hívja meg a **Registration.Register()** metódust az előfizetés regisztrálásához és az előfizetés regisztrációs állapotának lekéréséhez használható URI lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="b8303-120">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="b8303-121">További információ: [Előfizetés regisztrációs állapotának lekért állapota.](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="b8303-121">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="b8303-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="b8303-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b8303-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b8303-123">Request syntax</span></span>

| <span data-ttu-id="b8303-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="b8303-124">Method</span></span>    | <span data-ttu-id="b8303-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b8303-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b8303-126">**Post**</span><span class="sxs-lookup"><span data-stu-id="b8303-126">**POST**</span></span>  | <span data-ttu-id="b8303-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/registrations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b8303-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b8303-128">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="b8303-128">URI parameters</span></span>

<span data-ttu-id="b8303-129">Az ügyfél és az előfizetés azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="b8303-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="b8303-130">Név</span><span class="sxs-lookup"><span data-stu-id="b8303-130">Name</span></span>                    | <span data-ttu-id="b8303-131">Típus</span><span class="sxs-lookup"><span data-stu-id="b8303-131">Type</span></span>       | <span data-ttu-id="b8303-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b8303-132">Required</span></span> | <span data-ttu-id="b8303-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="b8303-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="b8303-134">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="b8303-134">customer-id</span></span>             | <span data-ttu-id="b8303-135">sztring</span><span class="sxs-lookup"><span data-stu-id="b8303-135">string</span></span>     | <span data-ttu-id="b8303-136">Igen</span><span class="sxs-lookup"><span data-stu-id="b8303-136">Yes</span></span>      | <span data-ttu-id="b8303-137">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="b8303-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="b8303-138">subscription-id (előfizetés-azonosító)</span><span class="sxs-lookup"><span data-stu-id="b8303-138">subscription-id</span></span>         | <span data-ttu-id="b8303-139">sztring</span><span class="sxs-lookup"><span data-stu-id="b8303-139">string</span></span>     | <span data-ttu-id="b8303-140">Igen</span><span class="sxs-lookup"><span data-stu-id="b8303-140">Yes</span></span>      | <span data-ttu-id="b8303-141">Egy GUID formátumú sztring, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="b8303-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="b8303-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b8303-142">Request headers</span></span>

<span data-ttu-id="b8303-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b8303-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b8303-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b8303-144">Request body</span></span>

<span data-ttu-id="b8303-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b8303-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b8303-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b8303-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="b8303-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b8303-147">REST response</span></span>

<span data-ttu-id="b8303-148">Ha a válasz sikeres, a válasz tartalmaz egy **Location** fejlécet egy URI-val, amely az előfizetés regisztrációs állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="b8303-148">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="b8303-149">Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz.</span><span class="sxs-lookup"><span data-stu-id="b8303-149">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="b8303-150">Az állapot lekérésével kapcsolatos példáért lásd: [Előfizetés regisztrációs állapotának lekérése.](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="b8303-150">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b8303-151">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b8303-151">Response success and error codes</span></span>

<span data-ttu-id="b8303-152">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="b8303-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b8303-153">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="b8303-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b8303-154">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b8303-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b8303-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b8303-155">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
