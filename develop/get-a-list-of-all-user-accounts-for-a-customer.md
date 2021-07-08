---
title: Egy ügyfél összes felhasználói fiókját tartalmazó lista lekérése
description: Az egyik ügyfélhez tartozó összes felhasználói fiók listájának lekért listája.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f3d5fcc610eae8c1bff056c1e4a9e7a74093c87d
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874567"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="6b53e-103">Egy ügyfél összes felhasználói fiókját tartalmazó lista lekérése</span><span class="sxs-lookup"><span data-stu-id="6b53e-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="6b53e-104">Ez a cikk azt ismerteti, hogyan lehet lekért lista az ügyfelek egyikének felhasználói fiókjairól.</span><span class="sxs-lookup"><span data-stu-id="6b53e-104">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="6b53e-105">Ha azonosító alapján keres egy felhasználói fiókot, tekintse meg a felhasználói fiók azonosító alapján [való lekért azonosítóját.](get-a-user-account-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="6b53e-105">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b53e-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6b53e-106">Prerequisites</span></span>

- <span data-ttu-id="6b53e-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6b53e-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6b53e-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="6b53e-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6b53e-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6b53e-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6b53e-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6b53e-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6b53e-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6b53e-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6b53e-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6b53e-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6b53e-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="6b53e-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6b53e-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6b53e-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6b53e-115">C\#</span><span class="sxs-lookup"><span data-stu-id="6b53e-115">C\#</span></span>

<span data-ttu-id="6b53e-116">Egy adott ügyfél összes felhasználói fiókja gyűjteményének lekérése:</span><span class="sxs-lookup"><span data-stu-id="6b53e-116">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="6b53e-117">Az ügyfél azonosításához hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="6b53e-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="6b53e-118">A [**gyűjtemény lekéréséhez hívja**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) meg a Users.Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="6b53e-118">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="6b53e-119">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="6b53e-119">For an example, see the following:</span></span>

- <span data-ttu-id="6b53e-120">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6b53e-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6b53e-121">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="6b53e-121">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="6b53e-122">Osztály: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="6b53e-122">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6b53e-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="6b53e-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6b53e-124">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6b53e-124">Request syntax</span></span>

| <span data-ttu-id="6b53e-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="6b53e-125">Method</span></span>  | <span data-ttu-id="6b53e-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6b53e-126">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="6b53e-127">**Kap**</span><span class="sxs-lookup"><span data-stu-id="6b53e-127">**GET**</span></span> | <span data-ttu-id="6b53e-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6b53e-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="6b53e-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="6b53e-129">URI parameter</span></span>

<span data-ttu-id="6b53e-130">A megfelelő ügyfél azonosításához használja a következő URI-paramétert.</span><span class="sxs-lookup"><span data-stu-id="6b53e-130">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="6b53e-131">Név</span><span class="sxs-lookup"><span data-stu-id="6b53e-131">Name</span></span>                   | <span data-ttu-id="6b53e-132">Típus</span><span class="sxs-lookup"><span data-stu-id="6b53e-132">Type</span></span>     | <span data-ttu-id="6b53e-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6b53e-133">Required</span></span> | <span data-ttu-id="6b53e-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="6b53e-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6b53e-135">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="6b53e-135">**customer-tenant-id**</span></span> | <span data-ttu-id="6b53e-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="6b53e-136">**guid**</span></span> | <span data-ttu-id="6b53e-137">Y</span><span class="sxs-lookup"><span data-stu-id="6b53e-137">Y</span></span>        | <span data-ttu-id="6b53e-138">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="6b53e-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6b53e-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6b53e-139">Request headers</span></span>

<span data-ttu-id="6b53e-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6b53e-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6b53e-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6b53e-141">Request body</span></span>

<span data-ttu-id="6b53e-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="6b53e-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6b53e-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6b53e-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6b53e-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6b53e-144">REST response</span></span>

<span data-ttu-id="6b53e-145">Ha ez a módszer sikeres, a rendszer felhasználói fiókok gyűjteményét adja vissza az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="6b53e-145">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6b53e-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6b53e-146">Response success and error codes</span></span>

<span data-ttu-id="6b53e-147">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="6b53e-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6b53e-148">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="6b53e-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6b53e-149">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6b53e-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6b53e-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6b53e-150">Response example</span></span>

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
