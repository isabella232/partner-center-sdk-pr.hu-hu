---
title: Egy ügyfél összes szolgáltatáskérésének lekérése
description: Lekérése az ügyfél összes szolgáltatáskérését.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ffcbbb9cf14b1b2a5b3becab541d3042c3cad508
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760674"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="5b9b8-103">Egy ügyfél összes szolgáltatáskérésének lekérése</span><span class="sxs-lookup"><span data-stu-id="5b9b8-103">Get all service requests for a customer</span></span>

<span data-ttu-id="5b9b8-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="5b9b8-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5b9b8-105">Lekérése az ügyfél összes szolgáltatáskérését.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-105">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="5b9b8-106">Az Partnerközpont irányítópulton ez a művelet úgy hajtható végre, hogy először [kiválaszt egy ügyfelet.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="5b9b8-107">Ezután válassza a **Szolgáltatáskezelés lehetőséget** a bal oldali oldalsávon.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="5b9b8-108">Az ügyfél szolgáltatáskérései a Támogatási jegyek alatt **jelennek meg.**</span><span class="sxs-lookup"><span data-stu-id="5b9b8-108">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b9b8-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5b9b8-109">Prerequisites</span></span>

- <span data-ttu-id="5b9b8-110">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5b9b8-111">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5b9b8-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b9b8-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5b9b8-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5b9b8-114">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5b9b8-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5b9b8-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5b9b8-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5b9b8-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="5b9b8-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5b9b8-117">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b9b8-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5b9b8-118">C\#</span><span class="sxs-lookup"><span data-stu-id="5b9b8-118">C\#</span></span>

<span data-ttu-id="5b9b8-119">Az ügyfél összes szolgáltatáskérésének megjelenítéséhez használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-119">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="5b9b8-120">Ezután hívja meg [**a ServiceRequests tulajdonságot,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) majd a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) a [**GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-120">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="5b9b8-121">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5b9b8-122">**Project:** PartnerCenterSDK.FeaturesSamples **osztály:** CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="5b9b8-122">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5b9b8-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="5b9b8-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5b9b8-124">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5b9b8-124">Request syntax</span></span>

| <span data-ttu-id="5b9b8-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="5b9b8-125">Method</span></span>  | <span data-ttu-id="5b9b8-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5b9b8-126">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5b9b8-127">**Kap**</span><span class="sxs-lookup"><span data-stu-id="5b9b8-127">**GET**</span></span> | <span data-ttu-id="5b9b8-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5b9b8-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5b9b8-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="5b9b8-129">URI parameter</span></span>

<span data-ttu-id="5b9b8-130">Az alábbi lekérdezési paraméterrel lekérdezheti az ügyfél összes szolgáltatáskérését.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-130">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="5b9b8-131">Név</span><span class="sxs-lookup"><span data-stu-id="5b9b8-131">Name</span></span>                   | <span data-ttu-id="5b9b8-132">Típus</span><span class="sxs-lookup"><span data-stu-id="5b9b8-132">Type</span></span>     | <span data-ttu-id="5b9b8-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5b9b8-133">Required</span></span> | <span data-ttu-id="5b9b8-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="5b9b8-134">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="5b9b8-135">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="5b9b8-135">**customer-tenant-id**</span></span> | <span data-ttu-id="5b9b8-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="5b9b8-136">**guid**</span></span> | <span data-ttu-id="5b9b8-137">Y</span><span class="sxs-lookup"><span data-stu-id="5b9b8-137">Y</span></span>        | <span data-ttu-id="5b9b8-138">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5b9b8-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5b9b8-139">Request headers</span></span>

<span data-ttu-id="5b9b8-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5b9b8-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5b9b8-141">Request body</span></span>

<span data-ttu-id="5b9b8-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5b9b8-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5b9b8-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="5b9b8-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5b9b8-144">REST response</span></span>

<span data-ttu-id="5b9b8-145">Ha a művelet sikeres, ez a metódus **szolgáltatáskérési** erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-145">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5b9b8-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5b9b8-146">Response success and error codes</span></span>

<span data-ttu-id="5b9b8-147">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5b9b8-148">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="5b9b8-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5b9b8-149">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5b9b8-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5b9b8-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5b9b8-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 742
Content-Type: application/json
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
Date: Tue, 24 Nov 2015 07:19:21 GMT

{
    "totalCount": 1,
    "items": [{
        "title": "Test",
        "severity": 0,
        "id": "615112491169010",
        "status": 1,
        "primaryContact": {
            "lastName": "LastName",
            "firstName": "FirstName"
        },
        "createdDate": "2015-11-24T01:07:00.863",
        "lastModifiedDate": "2015-11-24T01:17:10.61",
        "lastClosedDate": "0001-01-01T00:00:00",
        "attributes": {
            "objectType": "ServiceRequest"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
