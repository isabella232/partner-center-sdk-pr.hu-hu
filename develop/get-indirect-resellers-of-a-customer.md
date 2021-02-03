---
title: Egy ügyfél közvetett viszonteladóinak lekérése
description: Az adott ügyféllel kapcsolatban álló közvetett viszonteladók listájának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d69abf9530548f110820ca04fefb698e0e37556c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768335"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="50ce4-103">Egy ügyfél közvetett viszonteladóinak lekérése</span><span class="sxs-lookup"><span data-stu-id="50ce4-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="50ce4-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="50ce4-104">**Applies To**</span></span>

- <span data-ttu-id="50ce4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="50ce4-105">Partner Center</span></span>

<span data-ttu-id="50ce4-106">Az adott ügyféllel kapcsolatban álló közvetett viszonteladók listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="50ce4-106">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50ce4-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="50ce4-107">Prerequisites</span></span>

- <span data-ttu-id="50ce4-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="50ce4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="50ce4-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="50ce4-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="50ce4-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="50ce4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="50ce4-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="50ce4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="50ce4-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="50ce4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="50ce4-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="50ce4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="50ce4-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="50ce4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="50ce4-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="50ce4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="50ce4-116">C\#</span><span class="sxs-lookup"><span data-stu-id="50ce4-116">C\#</span></span>

<span data-ttu-id="50ce4-117">Azon közvetett viszonteladók listájának lekéréséhez, akikkel a megadott ügyfélnek van kapcsolata, először a [**partnerOperations.**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) Customers tulajdonságból szerezzen be egy felületet az ügyfél-gyűjtési műveletekhez az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="50ce4-117">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="50ce4-118">Ezután hívja meg a [**kapcsolatokat. Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) vagy [**Get \_ aszinkron**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) módszer a közvetett viszonteladók listájának lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="50ce4-118">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="50ce4-119">**Minta**: [Console test app](console-test-app.md)**Project**: a partner Center SDK Samples **osztálya**: GetIndirectResellersOfCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="50ce4-119">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="50ce4-120">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="50ce4-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="50ce4-121">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="50ce4-121">Request syntax</span></span>

| <span data-ttu-id="50ce4-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="50ce4-122">Method</span></span>  | <span data-ttu-id="50ce4-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="50ce4-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="50ce4-124">**GET**</span><span class="sxs-lookup"><span data-stu-id="50ce4-124">**GET**</span></span> | <span data-ttu-id="50ce4-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Relationships http/1.1</span><span class="sxs-lookup"><span data-stu-id="50ce4-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="50ce4-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="50ce4-126">URI parameter</span></span>

<span data-ttu-id="50ce4-127">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="50ce4-127">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="50ce4-128">Név</span><span class="sxs-lookup"><span data-stu-id="50ce4-128">Name</span></span>        | <span data-ttu-id="50ce4-129">Típus</span><span class="sxs-lookup"><span data-stu-id="50ce4-129">Type</span></span>   | <span data-ttu-id="50ce4-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="50ce4-130">Required</span></span> | <span data-ttu-id="50ce4-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="50ce4-131">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="50ce4-132">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="50ce4-132">customer-id</span></span> | <span data-ttu-id="50ce4-133">sztring</span><span class="sxs-lookup"><span data-stu-id="50ce4-133">string</span></span> | <span data-ttu-id="50ce4-134">Igen</span><span class="sxs-lookup"><span data-stu-id="50ce4-134">Yes</span></span>      | <span data-ttu-id="50ce4-135">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="50ce4-135">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="50ce4-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="50ce4-136">Request headers</span></span>

<span data-ttu-id="50ce4-137">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="50ce4-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="50ce4-138">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="50ce4-138">Request body</span></span>

<span data-ttu-id="50ce4-139">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="50ce4-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="50ce4-140">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="50ce4-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="50ce4-141">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="50ce4-141">REST response</span></span>

<span data-ttu-id="50ce4-142">Ha ez sikeres, a válasz törzse [PartnerRelationship](relationships-resources.md) -erőforrások gyűjteményét tartalmazza a viszonteladók azonosításához.</span><span class="sxs-lookup"><span data-stu-id="50ce4-142">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="50ce4-143">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="50ce4-143">Response success and error codes</span></span>

<span data-ttu-id="50ce4-144">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="50ce4-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="50ce4-145">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="50ce4-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="50ce4-146">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="50ce4-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="50ce4-147">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="50ce4-147">Response example</span></span>

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
