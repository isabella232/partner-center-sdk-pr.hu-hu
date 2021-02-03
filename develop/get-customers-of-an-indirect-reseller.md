---
title: Közvetett viszonteladó ügyfeleinek lekérése
description: Hogyan kérhető le egy közvetett viszonteladó ügyfeleinek listája.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e4219f544a74bb3f34ec3aefe08cf18eed77fd42
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768332"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="55496-103">Közvetett viszonteladó ügyfeleinek lekérése</span><span class="sxs-lookup"><span data-stu-id="55496-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="55496-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="55496-104">**Applies To**</span></span>

- <span data-ttu-id="55496-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="55496-105">Partner Center</span></span>

<span data-ttu-id="55496-106">Hogyan kérhető le egy közvetett viszonteladó ügyfeleinek listája.</span><span class="sxs-lookup"><span data-stu-id="55496-106">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55496-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="55496-107">Prerequisites</span></span>

- <span data-ttu-id="55496-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="55496-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="55496-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="55496-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="55496-110">A közvetett viszonteladó bérlői azonosítója.</span><span class="sxs-lookup"><span data-stu-id="55496-110">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="55496-111">C\#</span><span class="sxs-lookup"><span data-stu-id="55496-111">C\#</span></span>

<span data-ttu-id="55496-112">A megadott közvetett viszonteladóval fennálló kapcsolattal rendelkező ügyfelek gyűjteményének beszerzéséhez először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot a szűrő létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="55496-112">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="55496-113">Át kell adnia a [**CustomerSearchField. IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumerálási tagot egy karakterlánccá, és jeleznie kell a [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) karakterláncot a szűrési művelet típusaként.</span><span class="sxs-lookup"><span data-stu-id="55496-113">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="55496-114">Emellett meg kell adnia a közvetett viszonteladó bérlői azonosítóját is a szűréshez.</span><span class="sxs-lookup"><span data-stu-id="55496-114">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="55496-115">Ezután hozza létre a [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) objektumot a lekérdezésnek való átadáshoz. ehhez hívja meg a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódust, és adja át a szűrőt.</span><span class="sxs-lookup"><span data-stu-id="55496-115">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="55496-116">A BuildSimplyQuery csak az [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztály által támogatott lekérdezések egyike.</span><span class="sxs-lookup"><span data-stu-id="55496-116">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="55496-117">A szűrő végrehajtásához és az eredmény beszerzéséhez először használja a [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) felületet a partner felhasználói műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="55496-117">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="55496-118">Ezután hívja meg a [**lekérdezés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy a [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="55496-118">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="55496-119">Ha enumerálást szeretne létrehozni a lapozható eredmények átjárásához, szerezze be a Customer Collection enumerálási gyári felületét a [**IAggregatePartner. enumerálások.**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) Customers tulajdonságból, majd hívja meg a [**create (létrehozás**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)) függvényt, ahogy az az alábbi kódban is látható, az ügyfél gyűjteményét birtokló változó átadásával.</span><span class="sxs-lookup"><span data-stu-id="55496-119">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

<span data-ttu-id="55496-120">**Minta**: [Console test app](console-test-app.md)**Project**: a partner Center SDK Samples **osztálya**: GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="55496-120">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="55496-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="55496-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="55496-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="55496-122">Request syntax</span></span>

| <span data-ttu-id="55496-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="55496-123">Method</span></span>  | <span data-ttu-id="55496-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="55496-124">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="55496-125">**GET**</span><span class="sxs-lookup"><span data-stu-id="55496-125">**GET**</span></span> | <span data-ttu-id="55496-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? méret = {size}? szűrő = {Filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="55496-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="55496-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="55496-127">URI parameter</span></span>

<span data-ttu-id="55496-128">A kérelem létrehozásához használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="55496-128">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="55496-129">Név</span><span class="sxs-lookup"><span data-stu-id="55496-129">Name</span></span>   | <span data-ttu-id="55496-130">Típus</span><span class="sxs-lookup"><span data-stu-id="55496-130">Type</span></span>   | <span data-ttu-id="55496-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="55496-131">Required</span></span> | <span data-ttu-id="55496-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="55496-132">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="55496-133">size</span><span class="sxs-lookup"><span data-stu-id="55496-133">size</span></span>   | <span data-ttu-id="55496-134">int</span><span class="sxs-lookup"><span data-stu-id="55496-134">int</span></span>    | <span data-ttu-id="55496-135">Nem</span><span class="sxs-lookup"><span data-stu-id="55496-135">No</span></span>       | <span data-ttu-id="55496-136">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="55496-136">The number of results to be displayed at one time.</span></span> <span data-ttu-id="55496-137">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="55496-137">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="55496-138">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="55496-138">filter</span></span> | <span data-ttu-id="55496-139">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="55496-139">filter</span></span> | <span data-ttu-id="55496-140">Igen</span><span class="sxs-lookup"><span data-stu-id="55496-140">Yes</span></span>      | <span data-ttu-id="55496-141">A keresést szűrő lekérdezés.</span><span class="sxs-lookup"><span data-stu-id="55496-141">The query that filters the search.</span></span> <span data-ttu-id="55496-142">Egy adott közvetett viszonteladó ügyfeleinek lekéréséhez be kell szúrnia a közvetett viszonteladó azonosítóját, és tartalmaznia kell a következő karakterláncot: {"Field": "IndirectReseller", "value": "{közvetett viszonteladói azonosító}", "operátor": "kezdődik \_ "}.</span><span class="sxs-lookup"><span data-stu-id="55496-142">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="55496-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="55496-143">Request headers</span></span>

<span data-ttu-id="55496-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="55496-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="55496-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="55496-145">Request body</span></span>

<span data-ttu-id="55496-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="55496-146">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="55496-147">Példa kérésre (kódolt)</span><span class="sxs-lookup"><span data-stu-id="55496-147">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="55496-148">Példa kérésre (dekódolást)</span><span class="sxs-lookup"><span data-stu-id="55496-148">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="55496-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="55496-149">REST response</span></span>

<span data-ttu-id="55496-150">Ha ez sikeres, a válasz törzse információkat tartalmaz a viszonteladó ügyfeleiről.</span><span class="sxs-lookup"><span data-stu-id="55496-150">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="55496-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="55496-151">Response success and error codes</span></span>

<span data-ttu-id="55496-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="55496-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="55496-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="55496-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="55496-154">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="55496-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="55496-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="55496-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
