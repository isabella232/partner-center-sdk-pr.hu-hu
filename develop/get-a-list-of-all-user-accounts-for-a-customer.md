---
title: Egy ügyfél összes felhasználói fiókját tartalmazó lista lekérése
description: Az egyik ügyfélhez tartozó összes felhasználói fiók listájának beolvasása.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f2b1bcf9926e02232b6e2cc68b71e992b015324
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768096"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="daa70-103">Egy ügyfél összes felhasználói fiókját tartalmazó lista lekérése</span><span class="sxs-lookup"><span data-stu-id="daa70-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="daa70-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="daa70-104">**Applies to:**</span></span>

- <span data-ttu-id="daa70-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="daa70-105">Partner Center</span></span>

<span data-ttu-id="daa70-106">Ez a cikk azt ismerteti, hogyan kérhető le az egyik ügyfélhez tartozó összes felhasználói fiók listája.</span><span class="sxs-lookup"><span data-stu-id="daa70-106">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="daa70-107">Ha egyetlen felhasználói fiókot szeretne megkeresni azonosító alapján, olvassa el [a felhasználói fiók beolvasása azonosító alapján](get-a-user-account-by-id.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="daa70-107">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="daa70-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="daa70-108">Prerequisites</span></span>

- <span data-ttu-id="daa70-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="daa70-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="daa70-110">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="daa70-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="daa70-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="daa70-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="daa70-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="daa70-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="daa70-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="daa70-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="daa70-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="daa70-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="daa70-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="daa70-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="daa70-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="daa70-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="daa70-117">C\#</span><span class="sxs-lookup"><span data-stu-id="daa70-117">C\#</span></span>

<span data-ttu-id="daa70-118">Egy adott ügyfélhez tartozó összes felhasználói fiók gyűjteményének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="daa70-118">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="daa70-119">Hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="daa70-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="daa70-120">A gyűjtemény beolvasásához hívja meg a [**Users. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="daa70-120">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="daa70-121">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="daa70-121">For an example, see the following:</span></span>

- <span data-ttu-id="daa70-122">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="daa70-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="daa70-123">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="daa70-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="daa70-124">Osztály: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="daa70-124">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="daa70-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="daa70-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="daa70-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="daa70-126">Request syntax</span></span>

| <span data-ttu-id="daa70-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="daa70-127">Method</span></span>  | <span data-ttu-id="daa70-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="daa70-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="daa70-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="daa70-129">**GET**</span></span> | <span data-ttu-id="daa70-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="daa70-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="daa70-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="daa70-131">URI parameter</span></span>

<span data-ttu-id="daa70-132">A megfelelő ügyfél azonosításához használja a következő URI-paramétert.</span><span class="sxs-lookup"><span data-stu-id="daa70-132">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="daa70-133">Név</span><span class="sxs-lookup"><span data-stu-id="daa70-133">Name</span></span>                   | <span data-ttu-id="daa70-134">Típus</span><span class="sxs-lookup"><span data-stu-id="daa70-134">Type</span></span>     | <span data-ttu-id="daa70-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="daa70-135">Required</span></span> | <span data-ttu-id="daa70-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="daa70-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="daa70-137">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="daa70-137">**customer-tenant-id**</span></span> | <span data-ttu-id="daa70-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="daa70-138">**guid**</span></span> | <span data-ttu-id="daa70-139">Y</span><span class="sxs-lookup"><span data-stu-id="daa70-139">Y</span></span>        | <span data-ttu-id="daa70-140">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="daa70-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="daa70-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="daa70-141">Request headers</span></span>

<span data-ttu-id="daa70-142">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="daa70-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="daa70-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="daa70-143">Request body</span></span>

<span data-ttu-id="daa70-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="daa70-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="daa70-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="daa70-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="daa70-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="daa70-146">REST response</span></span>

<span data-ttu-id="daa70-147">Ha ez sikeres, ez a metódus egy ügyfél felhasználói fiókjainak gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="daa70-147">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="daa70-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="daa70-148">Response success and error codes</span></span>

<span data-ttu-id="daa70-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="daa70-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="daa70-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="daa70-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="daa70-151">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="daa70-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="daa70-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="daa70-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1030
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CV: 6zmKqrSFB0+t7m3y.0
MS-ServerId: 101112616
Date: Wed, 21 Dec 2016 21:13:24 GMT

 {
    "totalCount": 2,
    "items": [{
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
        }, {
            "id": "6e668259-1f09-479d-bcb8-d9b03e826b8d",
            "userPrincipalName": "admin@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "DT Demo CSP Customer 005",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/6e668259-1f09-479d-bcb8-d9b03e826b8d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
