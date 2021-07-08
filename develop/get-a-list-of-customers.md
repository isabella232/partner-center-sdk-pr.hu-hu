---
title: Az ügyfelek listájának lekérése
description: A partner összes ügyfelet képviselő erőforrások gyűjteményének lekért gyűjtése.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 840c9d1a61451763d37a19639f99b12f1deb7521
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874346"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="a88aa-103">Az ügyfelek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="a88aa-103">Get a list of customers</span></span>

<span data-ttu-id="a88aa-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a88aa-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a88aa-105">Ez a cikk bemutatja, hogyan gyűjti össze a partner összes ügyfelet képviselő erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="a88aa-105">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="a88aa-106">Ezt a műveletet az irányítópulton Partnerközpont is végrehajthatja.</span><span class="sxs-lookup"><span data-stu-id="a88aa-106">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="a88aa-107">A főoldal **Ügyfélkezelés területén** válassza az **Ügyfelek megtekintése lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a88aa-107">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="a88aa-108">Vagy az oldalsávon válassza az Ügyfelek **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a88aa-108">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a88aa-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a88aa-109">Prerequisites</span></span>

- <span data-ttu-id="a88aa-110">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a88aa-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a88aa-111">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="a88aa-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a88aa-112">C\#</span><span class="sxs-lookup"><span data-stu-id="a88aa-112">C\#</span></span>

<span data-ttu-id="a88aa-113">Az összes ügyfél listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="a88aa-113">To get a list of all customers:</span></span>

1. <span data-ttu-id="a88aa-114">Az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjtemény használatával hozzon létre **egy IPartner** objektumot.</span><span class="sxs-lookup"><span data-stu-id="a88aa-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="a88aa-115">Az ügyféllista lekérdezése a [**Query() vagy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) [**a QueryAsync() metódusokkal.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync)</span><span class="sxs-lookup"><span data-stu-id="a88aa-115">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="a88aa-116">(A lekérdezések létrehozásával vonatkozó utasításokért lásd a [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) osztályt.)</span><span class="sxs-lookup"><span data-stu-id="a88aa-116">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="a88aa-117">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="a88aa-117">For an example, see the following:</span></span>

- <span data-ttu-id="a88aa-118">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a88aa-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a88aa-119">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="a88aa-119">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="a88aa-120">Osztály: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="a88aa-120">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="a88aa-121">Java</span><span class="sxs-lookup"><span data-stu-id="a88aa-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a88aa-122">Az összes ügyfél listájának lekért listája:</span><span class="sxs-lookup"><span data-stu-id="a88aa-122">To get a list of all customers:</span></span>

1. <span data-ttu-id="a88aa-123">Az [**IAggregatePartner.getCustomers**] függvény használatával lekért hivatkozás az ügyfélműveletekkel kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="a88aa-123">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="a88aa-124">Az ügyféllista lekérése a **query() függvény** használatával.</span><span class="sxs-lookup"><span data-stu-id="a88aa-124">Retrieve the customer list using the **query()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="a88aa-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a88aa-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a88aa-126">Hajtsa végre [**a Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) parancsot paraméterek nélkül az ügyfelek teljes listájának leállításához.</span><span class="sxs-lookup"><span data-stu-id="a88aa-126">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="a88aa-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="a88aa-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a88aa-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a88aa-128">Request syntax</span></span>

| <span data-ttu-id="a88aa-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="a88aa-129">Method</span></span>  | <span data-ttu-id="a88aa-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a88aa-130">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="a88aa-131">**Kap**</span><span class="sxs-lookup"><span data-stu-id="a88aa-131">**GET**</span></span> | <span data-ttu-id="a88aa-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a88aa-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="a88aa-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a88aa-133">URI parameter</span></span>

<span data-ttu-id="a88aa-134">Az alábbi lekérdezési paraméterrel lekérdezheti az ügyfelek listáját.</span><span class="sxs-lookup"><span data-stu-id="a88aa-134">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="a88aa-135">Név</span><span class="sxs-lookup"><span data-stu-id="a88aa-135">Name</span></span>     | <span data-ttu-id="a88aa-136">Típus</span><span class="sxs-lookup"><span data-stu-id="a88aa-136">Type</span></span>    | <span data-ttu-id="a88aa-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a88aa-137">Required</span></span> | <span data-ttu-id="a88aa-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="a88aa-138">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="a88aa-139">**Méret**</span><span class="sxs-lookup"><span data-stu-id="a88aa-139">**size**</span></span> | <span data-ttu-id="a88aa-140">**int**</span><span class="sxs-lookup"><span data-stu-id="a88aa-140">**int**</span></span> | <span data-ttu-id="a88aa-141">Y</span><span class="sxs-lookup"><span data-stu-id="a88aa-141">Y</span></span>        | <span data-ttu-id="a88aa-142">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="a88aa-142">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a88aa-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a88aa-143">Request headers</span></span>

<span data-ttu-id="a88aa-144">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a88aa-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a88aa-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a88aa-145">Request body</span></span>

<span data-ttu-id="a88aa-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="a88aa-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a88aa-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a88aa-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="a88aa-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a88aa-148">REST response</span></span>

<span data-ttu-id="a88aa-149">Ha a művelet sikeres, ez a metódus ügyfélerőforrások [gyűjteményét](customer-resources.md#customer) adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="a88aa-149">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a88aa-150">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a88aa-150">Response success and error codes</span></span>

<span data-ttu-id="a88aa-151">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="a88aa-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a88aa-152">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="a88aa-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a88aa-153">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a88aa-153">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a88aa-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a88aa-154">Response example</span></span>

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
