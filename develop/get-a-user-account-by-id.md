---
title: Felhasználói fiók lekérése azonosító alapján
description: Egy adott felhasználói fiók beolvasása az ügyfelek számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a2f42001365324a65376318cb1f2d57dc123df0c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768055"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="b7924-103">Felhasználói fiók lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="b7924-103">Get a user account by ID</span></span>

<span data-ttu-id="b7924-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="b7924-104">**Applies To**</span></span>

- <span data-ttu-id="b7924-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b7924-105">Partner Center</span></span>

<span data-ttu-id="b7924-106">Egy adott felhasználói fiók beolvasása az ügyfelek számára.</span><span class="sxs-lookup"><span data-stu-id="b7924-106">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="b7924-107">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b7924-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b7924-108">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b7924-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b7924-109">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b7924-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b7924-110">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="b7924-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b7924-111">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="b7924-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b7924-112">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b7924-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b7924-113">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="b7924-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b7924-114">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b7924-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b7924-115">C\#</span><span class="sxs-lookup"><span data-stu-id="b7924-115">C\#</span></span>

<span data-ttu-id="b7924-116">Az ügyfél felhasználói fiókjának lekéréséhez hívja meg a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="b7924-116">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b7924-117">Ezután hívja meg a [**Users. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust az adott felhasználó lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="b7924-117">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="b7924-118">Végül hívja meg a Users [**. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) metódust a felhasználói fiók beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="b7924-118">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="b7924-119">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b7924-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b7924-120">**Projekt**: partner Center SDK Samples **osztály**: GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="b7924-120">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b7924-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b7924-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b7924-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b7924-122">Request syntax</span></span>

| <span data-ttu-id="b7924-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="b7924-123">Method</span></span>  | <span data-ttu-id="b7924-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b7924-124">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b7924-125">**GET**</span><span class="sxs-lookup"><span data-stu-id="b7924-125">**GET**</span></span> | <span data-ttu-id="b7924-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b7924-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b7924-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b7924-127">URI parameter</span></span>

<span data-ttu-id="b7924-128">A megfelelő ügyfél és felhasználó azonosításához használja a következő URI-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="b7924-128">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="b7924-129">Név</span><span class="sxs-lookup"><span data-stu-id="b7924-129">Name</span></span>                   | <span data-ttu-id="b7924-130">Típus</span><span class="sxs-lookup"><span data-stu-id="b7924-130">Type</span></span>     | <span data-ttu-id="b7924-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b7924-131">Required</span></span> | <span data-ttu-id="b7924-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="b7924-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b7924-133">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="b7924-133">**customer-tenant-id**</span></span> | <span data-ttu-id="b7924-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="b7924-134">**guid**</span></span> | <span data-ttu-id="b7924-135">Y</span><span class="sxs-lookup"><span data-stu-id="b7924-135">Y</span></span>        | <span data-ttu-id="b7924-136">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="b7924-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b7924-137">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="b7924-137">**user-id**</span></span>            | <span data-ttu-id="b7924-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="b7924-138">**guid**</span></span> | <span data-ttu-id="b7924-139">Y</span><span class="sxs-lookup"><span data-stu-id="b7924-139">Y</span></span>        | <span data-ttu-id="b7924-140">Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="b7924-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="b7924-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b7924-141">Request headers</span></span>

<span data-ttu-id="b7924-142">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b7924-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b7924-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b7924-143">Request body</span></span>

<span data-ttu-id="b7924-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b7924-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b7924-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b7924-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="b7924-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b7924-146">REST response</span></span>

<span data-ttu-id="b7924-147">Ha ez sikeres, ez a módszer az ügyfél felhasználói fiókját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="b7924-147">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b7924-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b7924-148">Response success and error codes</span></span>

<span data-ttu-id="b7924-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b7924-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b7924-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b7924-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b7924-151">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="b7924-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b7924-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b7924-152">Response example</span></span>

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
