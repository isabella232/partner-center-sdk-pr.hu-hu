---
title: Az ügyfelek listájának lekérése
description: Az összes partner ügyfeleit képviselő erőforrások gyűjteményének beszerzése.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 2dd8469458809ab38b6d6081adc91d6d1184d2d0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768295"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="4bda0-103">Az ügyfelek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="4bda0-103">Get a list of customers</span></span>

<span data-ttu-id="4bda0-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="4bda0-104">**Applies to:**</span></span>

- <span data-ttu-id="4bda0-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="4bda0-105">Partner Center</span></span>
- <span data-ttu-id="4bda0-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="4bda0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4bda0-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4bda0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4bda0-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4bda0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4bda0-109">Ez a cikk azt ismerteti, hogyan szerezhet be egy olyan erőforrás-gyűjteményt, amely az összes partner ügyfelet képviseli.</span><span class="sxs-lookup"><span data-stu-id="4bda0-109">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="4bda0-110">Ezt a műveletet a partner Center irányítópultján is végrehajthatja.</span><span class="sxs-lookup"><span data-stu-id="4bda0-110">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="4bda0-111">A főoldalon az **ügyfél-kezelés** területen válassza az **ügyfelek megtekintése** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="4bda0-111">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="4bda0-112">Vagy az oldalsávon válassza az **ügyfelek** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="4bda0-112">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bda0-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4bda0-113">Prerequisites</span></span>

- <span data-ttu-id="4bda0-114">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="4bda0-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4bda0-115">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="4bda0-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="4bda0-116">C\#</span><span class="sxs-lookup"><span data-stu-id="4bda0-116">C\#</span></span>

<span data-ttu-id="4bda0-117">Az összes ügyfél listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="4bda0-117">To get a list of all customers:</span></span>

1. <span data-ttu-id="4bda0-118">A [**IAggregatePartner. Customs**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjtemény használatával hozzon létre egy **IPartner** objektumot.</span><span class="sxs-lookup"><span data-stu-id="4bda0-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="4bda0-119">Kérje le az ügyfelek listáját a [**query ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) vagy a [**QueryAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="4bda0-119">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="4bda0-120">(A lekérdezések létrehozásával kapcsolatos utasításokért tekintse meg a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztályt.)</span><span class="sxs-lookup"><span data-stu-id="4bda0-120">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="4bda0-121">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="4bda0-121">For an example, see the following:</span></span>

- <span data-ttu-id="4bda0-122">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4bda0-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4bda0-123">Projekt: **PartnerSDK. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="4bda0-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="4bda0-124">Osztály: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="4bda0-124">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="4bda0-125">Java</span><span class="sxs-lookup"><span data-stu-id="4bda0-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="4bda0-126">Az összes ügyfél listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="4bda0-126">To get a list of all customers:</span></span>

1. <span data-ttu-id="4bda0-127">Használja az [**IAggregatePartner. getCustomers**] függvényt az ügyfél műveleteire mutató hivatkozás beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="4bda0-127">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="4bda0-128">Kérje le az ügyfél listáját a **query ()** függvény használatával.</span><span class="sxs-lookup"><span data-stu-id="4bda0-128">Retrieve the customer list using the **query()** function.</span></span>

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="4bda0-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bda0-129">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="4bda0-130">Futtassa a [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) parancsot paraméterek nélkül, hogy teljes listát kapjon az ügyfelekről.</span><span class="sxs-lookup"><span data-stu-id="4bda0-130">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="4bda0-131">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="4bda0-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4bda0-132">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4bda0-132">Request syntax</span></span>

| <span data-ttu-id="4bda0-133">Metódus</span><span class="sxs-lookup"><span data-stu-id="4bda0-133">Method</span></span>  | <span data-ttu-id="4bda0-134">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4bda0-134">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="4bda0-135">**GET**</span><span class="sxs-lookup"><span data-stu-id="4bda0-135">**GET**</span></span> | <span data-ttu-id="4bda0-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers? méret = {size} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4bda0-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="4bda0-137">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4bda0-137">URI parameter</span></span>

<span data-ttu-id="4bda0-138">Használja az alábbi lekérdezési paramétert az ügyfelek listájának lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="4bda0-138">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="4bda0-139">Név</span><span class="sxs-lookup"><span data-stu-id="4bda0-139">Name</span></span>     | <span data-ttu-id="4bda0-140">Típus</span><span class="sxs-lookup"><span data-stu-id="4bda0-140">Type</span></span>    | <span data-ttu-id="4bda0-141">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4bda0-141">Required</span></span> | <span data-ttu-id="4bda0-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="4bda0-142">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="4bda0-143">**méret**</span><span class="sxs-lookup"><span data-stu-id="4bda0-143">**size**</span></span> | <span data-ttu-id="4bda0-144">**int**</span><span class="sxs-lookup"><span data-stu-id="4bda0-144">**int**</span></span> | <span data-ttu-id="4bda0-145">Y</span><span class="sxs-lookup"><span data-stu-id="4bda0-145">Y</span></span>        | <span data-ttu-id="4bda0-146">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="4bda0-146">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4bda0-147">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4bda0-147">Request headers</span></span>

<span data-ttu-id="4bda0-148">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4bda0-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4bda0-149">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4bda0-149">Request body</span></span>

<span data-ttu-id="4bda0-150">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="4bda0-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4bda0-151">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4bda0-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="4bda0-152">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4bda0-152">REST response</span></span>

<span data-ttu-id="4bda0-153">Ha ez sikeres, ez a metódus a válasz törzsében lévő [ügyfél](customer-resources.md#customer) -erőforrások gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="4bda0-153">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4bda0-154">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4bda0-154">Response success and error codes</span></span>

<span data-ttu-id="4bda0-155">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="4bda0-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4bda0-156">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="4bda0-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4bda0-157">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4bda0-157">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4bda0-158">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4bda0-158">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
