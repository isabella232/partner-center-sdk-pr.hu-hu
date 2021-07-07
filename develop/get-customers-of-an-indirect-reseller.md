---
title: Közvetett viszonteladó ügyfeleinek lekérése
description: Egy közvetett viszonteladó ügyfeleinek listájának lekért listája.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e05248b16b803529258de806c25b117f3104ad2a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446326"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="057e2-103">Közvetett viszonteladó ügyfeleinek lekérése</span><span class="sxs-lookup"><span data-stu-id="057e2-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="057e2-104">Egy közvetett viszonteladó ügyfeleinek listájának lekért listája.</span><span class="sxs-lookup"><span data-stu-id="057e2-104">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="057e2-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="057e2-105">Prerequisites</span></span>

- <span data-ttu-id="057e2-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="057e2-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="057e2-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="057e2-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="057e2-108">A közvetett viszonteladó bérlőazonosítója.</span><span class="sxs-lookup"><span data-stu-id="057e2-108">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="057e2-109">C\#</span><span class="sxs-lookup"><span data-stu-id="057e2-109">C\#</span></span>

<span data-ttu-id="057e2-110">Ha olyan ügyfelek gyűjteményét kell lekérte, akik kapcsolatban vannak a megadott közvetett viszonteladóval, először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot a szűrő létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="057e2-110">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="057e2-111">A [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumerálás tagját át kell adni egy sztringgé, és a szűrőművelet típusaként meg kell adni a [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) mezőt.</span><span class="sxs-lookup"><span data-stu-id="057e2-111">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="057e2-112">Meg kell adnia annak a közvetett viszonteladónak a bérlőazonosítóját is, amely alapján szűrni tud.</span><span class="sxs-lookup"><span data-stu-id="057e2-112">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="057e2-113">Ezután példányosított egy [**iQuery-objektumot,**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) amelyet átadhat a lekérdezésnek a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódus hívásával és a szűrő átadásával.</span><span class="sxs-lookup"><span data-stu-id="057e2-113">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="057e2-114">A BuildSimplyQuery csak egy a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztály által támogatott lekérdezéstípusok közül.</span><span class="sxs-lookup"><span data-stu-id="057e2-114">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="057e2-115">A szűrő végrehajtásához és az eredmény lekért végrehajtásához először az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) használatával szerezze be a partner ügyfélműveletei interfészét.</span><span class="sxs-lookup"><span data-stu-id="057e2-115">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="057e2-116">Ezután hívja meg a [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy [**a QueryAsync metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="057e2-116">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="057e2-117">Ha létre kell hoznia egy enumerátort a lapozó eredmények bejárása érdekében, szerezze be az ügyfélgyűjtemény enumerátor-előállító felületét az [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) tulajdonságból, majd hívja meg a [**Létrehozás**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)függvényt az alábbi kódban látható módon, az ügyfélgyűjteményt tartalmazó változó átadásával.</span><span class="sxs-lookup"><span data-stu-id="057e2-117">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

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

<span data-ttu-id="057e2-118">**Minta:** [Konzoltesztelő](console-test-app.md)**alkalmazás Project:** Partnerközpont SDK Samples **Osztály:** GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="057e2-118">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="057e2-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="057e2-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="057e2-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="057e2-120">Request syntax</span></span>

| <span data-ttu-id="057e2-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="057e2-121">Method</span></span>  | <span data-ttu-id="057e2-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="057e2-122">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="057e2-123">**Kap**</span><span class="sxs-lookup"><span data-stu-id="057e2-123">**GET**</span></span> | <span data-ttu-id="057e2-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="057e2-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="057e2-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="057e2-125">URI parameter</span></span>

<span data-ttu-id="057e2-126">A kérelem létrehozásához használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="057e2-126">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="057e2-127">Név</span><span class="sxs-lookup"><span data-stu-id="057e2-127">Name</span></span>   | <span data-ttu-id="057e2-128">Típus</span><span class="sxs-lookup"><span data-stu-id="057e2-128">Type</span></span>   | <span data-ttu-id="057e2-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="057e2-129">Required</span></span> | <span data-ttu-id="057e2-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="057e2-130">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="057e2-131">size</span><span class="sxs-lookup"><span data-stu-id="057e2-131">size</span></span>   | <span data-ttu-id="057e2-132">int</span><span class="sxs-lookup"><span data-stu-id="057e2-132">int</span></span>    | <span data-ttu-id="057e2-133">Nem</span><span class="sxs-lookup"><span data-stu-id="057e2-133">No</span></span>       | <span data-ttu-id="057e2-134">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="057e2-134">The number of results to be displayed at one time.</span></span> <span data-ttu-id="057e2-135">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="057e2-135">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="057e2-136">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="057e2-136">filter</span></span> | <span data-ttu-id="057e2-137">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="057e2-137">filter</span></span> | <span data-ttu-id="057e2-138">Igen</span><span class="sxs-lookup"><span data-stu-id="057e2-138">Yes</span></span>      | <span data-ttu-id="057e2-139">A keresést szűrő lekérdezés.</span><span class="sxs-lookup"><span data-stu-id="057e2-139">The query that filters the search.</span></span> <span data-ttu-id="057e2-140">Egy adott közvetett viszonteladó ügyfeleinek lekéréséhez be kell szúrni a közvetett viszonteladó azonosítóját, és bele kell foglalnia és kódolnia kell a következő sztringet: {"Field":"IndirectReseller","Value":"{közvetett viszonteladó-azonosító}","Operátor":"kezdete"}. \_</span><span class="sxs-lookup"><span data-stu-id="057e2-140">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="057e2-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="057e2-141">Request headers</span></span>

<span data-ttu-id="057e2-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="057e2-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="057e2-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="057e2-143">Request body</span></span>

<span data-ttu-id="057e2-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="057e2-144">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="057e2-145">Példakérés (kódolt)</span><span class="sxs-lookup"><span data-stu-id="057e2-145">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="057e2-146">Példa kérése (dekódolva)</span><span class="sxs-lookup"><span data-stu-id="057e2-146">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="057e2-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="057e2-147">REST response</span></span>

<span data-ttu-id="057e2-148">Ha a válasz törzse sikeres, a viszonteladó ügyfeleivel kapcsolatos információkat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="057e2-148">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="057e2-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="057e2-149">Response success and error codes</span></span>

<span data-ttu-id="057e2-150">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="057e2-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="057e2-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="057e2-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="057e2-152">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="057e2-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="057e2-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="057e2-153">Response example</span></span>

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
