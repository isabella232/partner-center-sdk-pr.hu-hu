---
title: Előfizetés regisztrálása
description: Regisztráljon egy meglévő előfizetést, hogy engedélyezve legyen az Azure-foglalások rendezése.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768308"
---
# <a name="register-a-subscription"></a><span data-ttu-id="ddc0c-103">Előfizetés regisztrálása</span><span class="sxs-lookup"><span data-stu-id="ddc0c-103">Register a subscription</span></span>

<span data-ttu-id="ddc0c-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="ddc0c-104">**Applies To**</span></span>

- <span data-ttu-id="ddc0c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="ddc0c-105">Partner Center</span></span>

<span data-ttu-id="ddc0c-106">Regisztráljon egy meglévő [előfizetést](subscription-resources.md) , hogy engedélyezve legyen az Azure-foglalások rendezése.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-106">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="ddc0c-107">Azure-foglalás megvásárlásához legalább egy meglévő CSP Azure-előfizetéssel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-107">To purchase an Azure reservation you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="ddc0c-108">Ez a módszer lehetővé teszi a meglévő CSP Azure-előfizetés regisztrálását, amely lehetővé teszi az Azure-foglalások megvásárlását.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-108">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddc0c-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ddc0c-109">Prerequisites</span></span>

- <span data-ttu-id="ddc0c-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ddc0c-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ddc0c-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ddc0c-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ddc0c-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="ddc0c-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ddc0c-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ddc0c-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ddc0c-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ddc0c-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ddc0c-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ddc0c-118">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-118">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="ddc0c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="ddc0c-119">C\#</span></span>

<span data-ttu-id="ddc0c-120">Az ügyfél előfizetésének regisztrálásához kérje le az [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosítására.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-120">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ddc0c-121">Ezután hívja meg az [**előfizetés. ById ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) metódust az előfizetés-azonosítóval a regisztrálni kívánt előfizetés azonosításához.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-121">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="ddc0c-122">Végül hívja meg a **regisztrációs. Register ()** metódust az előfizetés regisztrálásához és az előfizetés regisztrációs állapotának lekéréséhez használható URI beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-122">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="ddc0c-123">További információ: előfizetés- [regisztráció állapotának beolvasása](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="ddc0c-123">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="ddc0c-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="ddc0c-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ddc0c-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ddc0c-125">Request syntax</span></span>

| <span data-ttu-id="ddc0c-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="ddc0c-126">Method</span></span>    | <span data-ttu-id="ddc0c-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ddc0c-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ddc0c-128">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="ddc0c-128">**POST**</span></span>  | <span data-ttu-id="ddc0c-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/registrations http/1.1</span><span class="sxs-lookup"><span data-stu-id="ddc0c-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="ddc0c-130">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="ddc0c-130">URI parameters</span></span>

<span data-ttu-id="ddc0c-131">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="ddc0c-132">Név</span><span class="sxs-lookup"><span data-stu-id="ddc0c-132">Name</span></span>                    | <span data-ttu-id="ddc0c-133">Típus</span><span class="sxs-lookup"><span data-stu-id="ddc0c-133">Type</span></span>       | <span data-ttu-id="ddc0c-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="ddc0c-134">Required</span></span> | <span data-ttu-id="ddc0c-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="ddc0c-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="ddc0c-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="ddc0c-136">customer-id</span></span>             | <span data-ttu-id="ddc0c-137">sztring</span><span class="sxs-lookup"><span data-stu-id="ddc0c-137">string</span></span>     | <span data-ttu-id="ddc0c-138">Igen</span><span class="sxs-lookup"><span data-stu-id="ddc0c-138">Yes</span></span>      | <span data-ttu-id="ddc0c-139">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="ddc0c-140">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="ddc0c-140">subscription-id</span></span>         | <span data-ttu-id="ddc0c-141">sztring</span><span class="sxs-lookup"><span data-stu-id="ddc0c-141">string</span></span>     | <span data-ttu-id="ddc0c-142">Igen</span><span class="sxs-lookup"><span data-stu-id="ddc0c-142">Yes</span></span>      | <span data-ttu-id="ddc0c-143">Egy GUID formátumú karakterlánc, amely azonosítja az előfizetést.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="ddc0c-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ddc0c-144">Request headers</span></span>

<span data-ttu-id="ddc0c-145">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ddc0c-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ddc0c-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ddc0c-146">Request body</span></span>

<span data-ttu-id="ddc0c-147">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ddc0c-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ddc0c-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="ddc0c-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ddc0c-149">REST response</span></span>

<span data-ttu-id="ddc0c-150">Ha ez sikeres, a válasz tartalmaz egy URI-t tartalmazó **Location** fejlécet, amely az előfizetés regisztrációs állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-150">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="ddc0c-151">Mentse ezt az URI-t más kapcsolódó REST API-kkal való használatra.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-151">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="ddc0c-152">Az állapot beolvasására vonatkozó példát az [előfizetés regisztrációs állapotának beolvasása](get-subscription-registration-status.md)című témakörben talál.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-152">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ddc0c-153">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ddc0c-153">Response success and error codes</span></span>

<span data-ttu-id="ddc0c-154">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ddc0c-155">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="ddc0c-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ddc0c-156">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ddc0c-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ddc0c-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ddc0c-157">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
