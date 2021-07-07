---
title: Felhasználói fiók lekérése azonosító alapján
description: Egy adott felhasználói fiók lekérte az ügyfélhez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a7cac98a8081a8557dcadfb0724f5497be7d14c
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760266"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="58a53-103">Felhasználói fiók lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="58a53-103">Get a user account by ID</span></span>

<span data-ttu-id="58a53-104">Egy adott felhasználói fiók lekérte az ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="58a53-104">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="58a53-105">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="58a53-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="58a53-106">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="58a53-106">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="58a53-107">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="58a53-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="58a53-108">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="58a53-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="58a53-109">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="58a53-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="58a53-110">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="58a53-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="58a53-111">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="58a53-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="58a53-112">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="58a53-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="58a53-113">C\#</span><span class="sxs-lookup"><span data-stu-id="58a53-113">C\#</span></span>

<span data-ttu-id="58a53-114">Az ügyfél felhasználói fiókjának lekérése érdekében hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="58a53-114">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="58a53-115">Ezután hívja meg a [**Users.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) az adott felhasználó lekérésére.</span><span class="sxs-lookup"><span data-stu-id="58a53-115">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="58a53-116">Végül hívja meg a [**Users.Get vagy**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) metódust a felhasználói fiók lekérésére.</span><span class="sxs-lookup"><span data-stu-id="58a53-116">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="58a53-117">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="58a53-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="58a53-118">**Project**: Partnerközpont SDK **Osztály:** GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="58a53-118">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="58a53-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="58a53-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="58a53-120">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="58a53-120">Request syntax</span></span>

| <span data-ttu-id="58a53-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="58a53-121">Method</span></span>  | <span data-ttu-id="58a53-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="58a53-122">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="58a53-123">**Kap**</span><span class="sxs-lookup"><span data-stu-id="58a53-123">**GET**</span></span> | <span data-ttu-id="58a53-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{felhasználói azonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="58a53-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="58a53-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="58a53-125">URI parameter</span></span>

<span data-ttu-id="58a53-126">Az alábbi URI-paraméterekkel azonosíthatja a megfelelő ügyfelet és felhasználót.</span><span class="sxs-lookup"><span data-stu-id="58a53-126">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="58a53-127">Név</span><span class="sxs-lookup"><span data-stu-id="58a53-127">Name</span></span>                   | <span data-ttu-id="58a53-128">Típus</span><span class="sxs-lookup"><span data-stu-id="58a53-128">Type</span></span>     | <span data-ttu-id="58a53-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="58a53-129">Required</span></span> | <span data-ttu-id="58a53-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="58a53-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="58a53-131">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="58a53-131">**customer-tenant-id**</span></span> | <span data-ttu-id="58a53-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="58a53-132">**guid**</span></span> | <span data-ttu-id="58a53-133">Y</span><span class="sxs-lookup"><span data-stu-id="58a53-133">Y</span></span>        | <span data-ttu-id="58a53-134">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="58a53-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="58a53-135">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="58a53-135">**user-id**</span></span>            | <span data-ttu-id="58a53-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="58a53-136">**guid**</span></span> | <span data-ttu-id="58a53-137">Y</span><span class="sxs-lookup"><span data-stu-id="58a53-137">Y</span></span>        | <span data-ttu-id="58a53-138">Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="58a53-138">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="58a53-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="58a53-139">Request headers</span></span>

<span data-ttu-id="58a53-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="58a53-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="58a53-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="58a53-141">Request body</span></span>

<span data-ttu-id="58a53-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="58a53-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="58a53-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="58a53-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="58a53-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="58a53-144">REST response</span></span>

<span data-ttu-id="58a53-145">Ha ez a módszer sikeres, az ügyfél felhasználói fiókját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="58a53-145">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="58a53-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="58a53-146">Response success and error codes</span></span>

<span data-ttu-id="58a53-147">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="58a53-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="58a53-148">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="58a53-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="58a53-149">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="58a53-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="58a53-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="58a53-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 432
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CV: uWM1EGU7+0aI2MvV.0
MS-ServerId: 020021921
Date: Wed, 21 Dec 2016 22:59:10 GMT

{
    "usageLocation": "US",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Daniel",
    "lastName": "Tsai",
    "displayName": "Daniel Tsai",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
