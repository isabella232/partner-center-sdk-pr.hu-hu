---
title: Az ügyfelek listájának lekérése keresési mező alapján szűrve
description: Lekért egy szűrőnek megfelelő ügyfélerőforrás-gyűjteményt. Igény szerint meg is állíthatja az oldalméretet. Szűrhet vállalatnév, tartomány, közvetett viszonteladó vagy közvetett felhőszolgáltató (CSP) alapján.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 663b8509d8704f9c443796d9fbcf72fb9c5b7fb2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874958"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="7b893-105">Az ügyfelek listájának lekérése keresési mező alapján szűrve</span><span class="sxs-lookup"><span data-stu-id="7b893-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="7b893-106">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7b893-106">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7b893-107">Lekért egy [szűrőnek](customer-resources.md#customer) megfelelő ügyfélerőforrás-gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="7b893-107">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="7b893-108">Igény szerint meg is állíthatja az oldalméretet.</span><span class="sxs-lookup"><span data-stu-id="7b893-108">You can optionally set a page size.</span></span> <span data-ttu-id="7b893-109">Szűrhet vállalatnév, tartomány, közvetett viszonteladó vagy közvetett felhőszolgáltató (CSP) alapján.</span><span class="sxs-lookup"><span data-stu-id="7b893-109">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b893-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7b893-110">Prerequisites</span></span>

- <span data-ttu-id="7b893-111">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7b893-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7b893-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="7b893-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7b893-113">Felhasználó által felépített szűrő.</span><span class="sxs-lookup"><span data-stu-id="7b893-113">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="7b893-114">C\#</span><span class="sxs-lookup"><span data-stu-id="7b893-114">C\#</span></span>

<span data-ttu-id="7b893-115">A szűrőnek megfelelő ügyfelek gyűjteményének lekért létrehozásához először hozzon létre egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumot.</span><span class="sxs-lookup"><span data-stu-id="7b893-115">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="7b893-116">A [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)mezőt tartalmazó sztringet kell átadnia, és a szűrőművelet típusát [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)értékkel kell jeleznie.</span><span class="sxs-lookup"><span data-stu-id="7b893-116">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="7b893-117">Ez az egyetlen mezőszűrő művelet, amelyet az ügyfelek végpontja támogat.</span><span class="sxs-lookup"><span data-stu-id="7b893-117">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="7b893-118">A szűréshez meg kell adnia a sztringet is.</span><span class="sxs-lookup"><span data-stu-id="7b893-118">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="7b893-119">Ezután példányosított egy [**iQuery-objektumot**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) a lekérdezésnek való átadáshoz a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódus hívásával és a szűrő átadásával.</span><span class="sxs-lookup"><span data-stu-id="7b893-119">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="7b893-120">A BuildSimplyQuery csak egy a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztály által támogatott lekérdezéstípusok közül.</span><span class="sxs-lookup"><span data-stu-id="7b893-120">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="7b893-121">Végül a szűrő végrehajtásához és az eredmény lekért eredményéhez először használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) metódust, hogy lekért egy felületet a partner ügyfélműveleteihez.</span><span class="sxs-lookup"><span data-stu-id="7b893-121">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="7b893-122">Ezután hívja meg a [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy [**a QueryAsync metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="7b893-122">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

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

<span data-ttu-id="7b893-123">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7b893-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7b893-124">**Project**: Partnerközpont SDK **Osztály:** FilterCustomers.cs</span><span class="sxs-lookup"><span data-stu-id="7b893-124">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7b893-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="7b893-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7b893-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7b893-126">Request syntax</span></span>

| <span data-ttu-id="7b893-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="7b893-127">Method</span></span>  | <span data-ttu-id="7b893-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7b893-128">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b893-129">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7b893-129">**GET**</span></span> | <span data-ttu-id="7b893-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7b893-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="7b893-131">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7b893-131">URI parameters</span></span>

<span data-ttu-id="7b893-132">Használja az alábbi lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="7b893-132">Use the following query parameters.</span></span>

| <span data-ttu-id="7b893-133">Név</span><span class="sxs-lookup"><span data-stu-id="7b893-133">Name</span></span>   | <span data-ttu-id="7b893-134">Típus</span><span class="sxs-lookup"><span data-stu-id="7b893-134">Type</span></span>   | <span data-ttu-id="7b893-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7b893-135">Required</span></span> | <span data-ttu-id="7b893-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="7b893-136">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="7b893-137">size</span><span class="sxs-lookup"><span data-stu-id="7b893-137">size</span></span>   | <span data-ttu-id="7b893-138">int</span><span class="sxs-lookup"><span data-stu-id="7b893-138">int</span></span>    | <span data-ttu-id="7b893-139">Nem</span><span class="sxs-lookup"><span data-stu-id="7b893-139">No</span></span>       | <span data-ttu-id="7b893-140">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="7b893-140">The number of results to be displayed at one time.</span></span> <span data-ttu-id="7b893-141">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="7b893-141">This parameter is optional.</span></span> |
| <span data-ttu-id="7b893-142">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="7b893-142">filter</span></span> | <span data-ttu-id="7b893-143">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="7b893-143">filter</span></span> | <span data-ttu-id="7b893-144">Igen</span><span class="sxs-lookup"><span data-stu-id="7b893-144">Yes</span></span>      | <span data-ttu-id="7b893-145">Az ügyfelekre alkalmazandó szűrő.</span><span class="sxs-lookup"><span data-stu-id="7b893-145">The filter to apply to customers.</span></span> <span data-ttu-id="7b893-146">Ennek kódolt sztringnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="7b893-146">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="7b893-147">Szűrőszintaxis</span><span class="sxs-lookup"><span data-stu-id="7b893-147">Filter Syntax</span></span>

<span data-ttu-id="7b893-148">A szűrőparamétert vesszővel tagolt kulcs-érték párok sorozataként kell összerakni.</span><span class="sxs-lookup"><span data-stu-id="7b893-148">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="7b893-149">Minden kulcsot és értéket külön kell idézni, és kettősponttal kell elválasztani egymástól.</span><span class="sxs-lookup"><span data-stu-id="7b893-149">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="7b893-150">A teljes szűrőt kódolni kell.</span><span class="sxs-lookup"><span data-stu-id="7b893-150">The entire filter must be encoded.</span></span>

<span data-ttu-id="7b893-151">Egy nem kódolatlan példa a következő:</span><span class="sxs-lookup"><span data-stu-id="7b893-151">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="7b893-152">Az alábbi táblázat a szükséges kulcs-érték párokat ismerteti:</span><span class="sxs-lookup"><span data-stu-id="7b893-152">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="7b893-153">Kulcs</span><span class="sxs-lookup"><span data-stu-id="7b893-153">Key</span></span>      | <span data-ttu-id="7b893-154">Érték</span><span class="sxs-lookup"><span data-stu-id="7b893-154">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b893-155">Mező</span><span class="sxs-lookup"><span data-stu-id="7b893-155">Field</span></span>    | <span data-ttu-id="7b893-156">A szűrni való mező.</span><span class="sxs-lookup"><span data-stu-id="7b893-156">The field to filter.</span></span> <span data-ttu-id="7b893-157">Az érvényes értékek a [**CustomerSearchField mezőben találhatók.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)</span><span class="sxs-lookup"><span data-stu-id="7b893-157">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="7b893-158">Érték</span><span class="sxs-lookup"><span data-stu-id="7b893-158">Value</span></span>    | <span data-ttu-id="7b893-159">A szűrési érték.</span><span class="sxs-lookup"><span data-stu-id="7b893-159">The value to filter by.</span></span> <span data-ttu-id="7b893-160">A rendszer figyelmen kívül hagyja az érték kis- és nagyját.</span><span class="sxs-lookup"><span data-stu-id="7b893-160">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="7b893-161">Operátor</span><span class="sxs-lookup"><span data-stu-id="7b893-161">Operator</span></span> | <span data-ttu-id="7b893-162">Az alkalmazandó operátor.</span><span class="sxs-lookup"><span data-stu-id="7b893-162">The operator to apply.</span></span> <span data-ttu-id="7b893-163">Ebben az ügyfélforgatókönyvben az egyetlen támogatott érték a \_ "kezdete".</span><span class="sxs-lookup"><span data-stu-id="7b893-163">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="7b893-164">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7b893-164">Request headers</span></span>

<span data-ttu-id="7b893-165">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7b893-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7b893-166">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7b893-166">Request body</span></span>

<span data-ttu-id="7b893-167">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7b893-167">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7b893-168">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7b893-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="7b893-169">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7b893-169">REST response</span></span>

<span data-ttu-id="7b893-170">Ha ez a módszer sikeres, a válasz törzsében egyező [Ügyfél-erőforrások](customer-resources.md#customer) gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="7b893-170">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7b893-171">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7b893-171">Response success and error codes</span></span>

<span data-ttu-id="7b893-172">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="7b893-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7b893-173">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="7b893-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7b893-174">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7b893-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7b893-175">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7b893-175">Response example</span></span>

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
