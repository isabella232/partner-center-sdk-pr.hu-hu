---
title: Az ügyfelek listájának lekérése keresési mező alapján szűrve
description: Egy szűrőnek megfelelő ügyfél-erőforrások gyűjteményét kéri le. Igény szerint beállíthatja az oldalméret méretét. A szűrést vállalat neve, tartomány, közvetett viszonteladó vagy közvetett felhőalapú megoldás-szolgáltató (CSP) alapján végezheti el.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: aad9524dbe2c9edbbd7c1d50da7a448f6872fcb9
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768124"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="571a0-105">Az ügyfelek listájának lekérése keresési mező alapján szűrve</span><span class="sxs-lookup"><span data-stu-id="571a0-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="571a0-106">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="571a0-106">**Applies To**</span></span>

- <span data-ttu-id="571a0-107">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="571a0-107">Partner Center</span></span>
- <span data-ttu-id="571a0-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="571a0-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="571a0-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="571a0-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="571a0-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="571a0-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="571a0-111">Egy szűrőnek megfelelő [ügyfél](customer-resources.md#customer) -erőforrások gyűjteményét kéri le.</span><span class="sxs-lookup"><span data-stu-id="571a0-111">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="571a0-112">Igény szerint beállíthatja az oldalméret méretét.</span><span class="sxs-lookup"><span data-stu-id="571a0-112">You can optionally set a page size.</span></span> <span data-ttu-id="571a0-113">A szűrést vállalat neve, tartomány, közvetett viszonteladó vagy közvetett felhőalapú megoldás-szolgáltató (CSP) alapján végezheti el.</span><span class="sxs-lookup"><span data-stu-id="571a0-113">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="571a0-114">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="571a0-114">Prerequisites</span></span>

- <span data-ttu-id="571a0-115">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="571a0-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="571a0-116">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="571a0-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="571a0-117">Felhasználó által létrehozott szűrő.</span><span class="sxs-lookup"><span data-stu-id="571a0-117">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="571a0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="571a0-118">C\#</span></span>

<span data-ttu-id="571a0-119">Egy szűrőnek megfelelő ügyfelek gyűjteményének lekéréséhez először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot a szűrő létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="571a0-119">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="571a0-120">Meg kell adnia egy karakterláncot, amely tartalmazza a [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), és a szűrési művelet típusát adja meg [**FieldFilterOperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)néven.</span><span class="sxs-lookup"><span data-stu-id="571a0-120">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="571a0-121">Ez az egyetlen, az ügyfelek végpontja által támogatott szűrési művelet.</span><span class="sxs-lookup"><span data-stu-id="571a0-121">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="571a0-122">Emellett meg kell adnia a szűréshez használandó karakterláncot is.</span><span class="sxs-lookup"><span data-stu-id="571a0-122">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="571a0-123">Ezután hozza létre a [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) objektumot a lekérdezésnek való átadáshoz. ehhez hívja meg a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódust, és adja át a szűrőt.</span><span class="sxs-lookup"><span data-stu-id="571a0-123">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="571a0-124">A BuildSimplyQuery csak az [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztály által támogatott lekérdezések egyike.</span><span class="sxs-lookup"><span data-stu-id="571a0-124">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="571a0-125">Végül, a szűrő végrehajtásához és az eredmény beszerzéséhez először használja a [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) felületet a partner ügyfél-műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="571a0-125">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="571a0-126">Ezután hívja meg a [**lekérdezés**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy a [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="571a0-126">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

<span data-ttu-id="571a0-127">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="571a0-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="571a0-128">**Projekt**: partner Center SDK Samples **osztály**: FilterCustomers.cs</span><span class="sxs-lookup"><span data-stu-id="571a0-128">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="571a0-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="571a0-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="571a0-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="571a0-130">Request syntax</span></span>

| <span data-ttu-id="571a0-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="571a0-131">Method</span></span>  | <span data-ttu-id="571a0-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="571a0-132">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="571a0-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="571a0-133">**GET**</span></span> | <span data-ttu-id="571a0-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? méret = {size} &szűrő = {Filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="571a0-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="571a0-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="571a0-135">URI parameters</span></span>

<span data-ttu-id="571a0-136">Használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="571a0-136">Use the following query parameters.</span></span>

| <span data-ttu-id="571a0-137">Név</span><span class="sxs-lookup"><span data-stu-id="571a0-137">Name</span></span>   | <span data-ttu-id="571a0-138">Típus</span><span class="sxs-lookup"><span data-stu-id="571a0-138">Type</span></span>   | <span data-ttu-id="571a0-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="571a0-139">Required</span></span> | <span data-ttu-id="571a0-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="571a0-140">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="571a0-141">size</span><span class="sxs-lookup"><span data-stu-id="571a0-141">size</span></span>   | <span data-ttu-id="571a0-142">int</span><span class="sxs-lookup"><span data-stu-id="571a0-142">int</span></span>    | <span data-ttu-id="571a0-143">Nem</span><span class="sxs-lookup"><span data-stu-id="571a0-143">No</span></span>       | <span data-ttu-id="571a0-144">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="571a0-144">The number of results to be displayed at one time.</span></span> <span data-ttu-id="571a0-145">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="571a0-145">This parameter is optional.</span></span> |
| <span data-ttu-id="571a0-146">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="571a0-146">filter</span></span> | <span data-ttu-id="571a0-147">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="571a0-147">filter</span></span> | <span data-ttu-id="571a0-148">Igen</span><span class="sxs-lookup"><span data-stu-id="571a0-148">Yes</span></span>      | <span data-ttu-id="571a0-149">Az ügyfelekre alkalmazandó szűrő.</span><span class="sxs-lookup"><span data-stu-id="571a0-149">The filter to apply to customers.</span></span> <span data-ttu-id="571a0-150">Ennek kódolású sztringnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="571a0-150">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="571a0-151">Szűrési szintaxis</span><span class="sxs-lookup"><span data-stu-id="571a0-151">Filter Syntax</span></span>

<span data-ttu-id="571a0-152">A Filter paramétert vesszővel elválasztott, kulcs-érték párokból álló sorozatként kell összeállítani.</span><span class="sxs-lookup"><span data-stu-id="571a0-152">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="571a0-153">Minden kulcsot és értéket külön kell megadni, és kettősponttal kell elválasztani őket.</span><span class="sxs-lookup"><span data-stu-id="571a0-153">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="571a0-154">A teljes szűrőt kódolni kell.</span><span class="sxs-lookup"><span data-stu-id="571a0-154">The entire filter must be encoded.</span></span>

<span data-ttu-id="571a0-155">A kódolás nélküli példa a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="571a0-155">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="571a0-156">A következő táblázat a szükséges kulcs-érték párokat ismerteti:</span><span class="sxs-lookup"><span data-stu-id="571a0-156">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="571a0-157">Kulcs</span><span class="sxs-lookup"><span data-stu-id="571a0-157">Key</span></span>      | <span data-ttu-id="571a0-158">Érték</span><span class="sxs-lookup"><span data-stu-id="571a0-158">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="571a0-159">Mező</span><span class="sxs-lookup"><span data-stu-id="571a0-159">Field</span></span>    | <span data-ttu-id="571a0-160">A szűrni kívánt mező.</span><span class="sxs-lookup"><span data-stu-id="571a0-160">The field to filter.</span></span> <span data-ttu-id="571a0-161">Az érvényes értékek a [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)-ben találhatók.</span><span class="sxs-lookup"><span data-stu-id="571a0-161">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="571a0-162">Érték</span><span class="sxs-lookup"><span data-stu-id="571a0-162">Value</span></span>    | <span data-ttu-id="571a0-163">A szűréshez használandó érték.</span><span class="sxs-lookup"><span data-stu-id="571a0-163">The value to filter by.</span></span> <span data-ttu-id="571a0-164">A rendszer figyelmen kívül hagyja az érték esetét.</span><span class="sxs-lookup"><span data-stu-id="571a0-164">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="571a0-165">Operátor</span><span class="sxs-lookup"><span data-stu-id="571a0-165">Operator</span></span> | <span data-ttu-id="571a0-166">Az alkalmazni kívánt operátor.</span><span class="sxs-lookup"><span data-stu-id="571a0-166">The operator to apply.</span></span> <span data-ttu-id="571a0-167">Ez az ügyfél-forgatókönyv egyetlen támogatott értéke a "kezdete \_ ".</span><span class="sxs-lookup"><span data-stu-id="571a0-167">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="571a0-168">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="571a0-168">Request headers</span></span>

<span data-ttu-id="571a0-169">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="571a0-169">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="571a0-170">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="571a0-170">Request body</span></span>

<span data-ttu-id="571a0-171">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="571a0-171">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="571a0-172">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="571a0-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="571a0-173">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="571a0-173">REST response</span></span>

<span data-ttu-id="571a0-174">Ha a művelet sikeres, ez a metódus a válasz törzsében lévő [ügyfél](customer-resources.md#customer) -erőforrások egyező gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="571a0-174">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="571a0-175">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="571a0-175">Response success and error codes</span></span>

<span data-ttu-id="571a0-176">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="571a0-176">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="571a0-177">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="571a0-177">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="571a0-178">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="571a0-178">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="571a0-179">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="571a0-179">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
