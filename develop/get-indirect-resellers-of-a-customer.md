---
title: Egy ügyfél közvetett viszonteladóinak lekérése
description: Azon közvetett viszonteladók listájának lekérte, akik kapcsolatban vannak egy adott ügyféllel.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 8697c40c22d5c19979c066b8d3a1de733e211f71
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446241"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="4df64-103">Egy ügyfél közvetett viszonteladóinak lekérése</span><span class="sxs-lookup"><span data-stu-id="4df64-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="4df64-104">Azon közvetett viszonteladók listájának lekérte, akik kapcsolatban vannak egy adott ügyféllel.</span><span class="sxs-lookup"><span data-stu-id="4df64-104">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4df64-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4df64-105">Prerequisites</span></span>

- <span data-ttu-id="4df64-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4df64-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4df64-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="4df64-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4df64-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4df64-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4df64-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4df64-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4df64-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4df64-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4df64-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4df64-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4df64-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="4df64-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4df64-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4df64-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="4df64-114">C\#</span><span class="sxs-lookup"><span data-stu-id="4df64-114">C\#</span></span>

<span data-ttu-id="4df64-115">Azon közvetett viszonteladók listájának lekéréséhez, akikkel a megadott ügyfél kapcsolatban áll, először szerezze be a [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) tulajdonságból az ügyfél azonosítóját az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="4df64-115">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="4df64-116">Ezután hívja meg [**a Relationships.Get vagy**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) [**a Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) metódust a közvetett viszonteladók listájának lehívásához.</span><span class="sxs-lookup"><span data-stu-id="4df64-116">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="4df64-117">**Minta:** [Konzoltesztelő](console-test-app.md)**alkalmazás Project:** Partnerközpont SDK Samples **Class:** GetIndirectResellersOfCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="4df64-117">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4df64-118">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4df64-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4df64-119">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4df64-119">Request syntax</span></span>

| <span data-ttu-id="4df64-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="4df64-120">Method</span></span>  | <span data-ttu-id="4df64-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4df64-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="4df64-122">**Kap**</span><span class="sxs-lookup"><span data-stu-id="4df64-122">**GET**</span></span> | <span data-ttu-id="4df64-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/kapcsolatok HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4df64-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4df64-124">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4df64-124">URI parameter</span></span>

<span data-ttu-id="4df64-125">Az ügyfél azonosításához használja a következő elérésiút-paramétert.</span><span class="sxs-lookup"><span data-stu-id="4df64-125">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="4df64-126">Név</span><span class="sxs-lookup"><span data-stu-id="4df64-126">Name</span></span>        | <span data-ttu-id="4df64-127">Típus</span><span class="sxs-lookup"><span data-stu-id="4df64-127">Type</span></span>   | <span data-ttu-id="4df64-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4df64-128">Required</span></span> | <span data-ttu-id="4df64-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="4df64-129">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="4df64-130">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="4df64-130">customer-id</span></span> | <span data-ttu-id="4df64-131">sztring</span><span class="sxs-lookup"><span data-stu-id="4df64-131">string</span></span> | <span data-ttu-id="4df64-132">Igen</span><span class="sxs-lookup"><span data-stu-id="4df64-132">Yes</span></span>      | <span data-ttu-id="4df64-133">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="4df64-133">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4df64-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4df64-134">Request headers</span></span>

<span data-ttu-id="4df64-135">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4df64-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4df64-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4df64-136">Request body</span></span>

<span data-ttu-id="4df64-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="4df64-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4df64-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4df64-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4df64-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4df64-139">REST response</span></span>

<span data-ttu-id="4df64-140">Ha a válasz törzse sikeres, a [partnerreláció](relationships-resources.md) erőforrásainak gyűjteményét tartalmazza a viszonteladók azonosításához.</span><span class="sxs-lookup"><span data-stu-id="4df64-140">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4df64-141">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4df64-141">Response success and error codes</span></span>

<span data-ttu-id="4df64-142">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4df64-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4df64-143">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4df64-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4df64-144">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4df64-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4df64-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4df64-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
