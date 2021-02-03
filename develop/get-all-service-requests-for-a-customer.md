---
title: Egy ügyfél összes szolgáltatáskérésének lekérése
description: Minden ügyfél szolgáltatási kérelmének beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f473c7a7d43b1a3929d983fb23dae92fdafbc0f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768472"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="02813-103">Egy ügyfél összes szolgáltatáskérésének lekérése</span><span class="sxs-lookup"><span data-stu-id="02813-103">Get all service requests for a customer</span></span>

<span data-ttu-id="02813-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="02813-104">**Applies To**</span></span>

- <span data-ttu-id="02813-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="02813-105">Partner Center</span></span>
- <span data-ttu-id="02813-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="02813-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="02813-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="02813-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="02813-108">Minden ügyfél szolgáltatási kérelmének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="02813-108">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="02813-109">A partner Center irányítópultján ezt a műveletet a [felhasználó kiválasztásával](get-a-customer-by-name.md)végezheti el.</span><span class="sxs-lookup"><span data-stu-id="02813-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="02813-110">Ezután válassza a **Service Management** elemet a bal oldali oldalsávon.</span><span class="sxs-lookup"><span data-stu-id="02813-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="02813-111">Az ügyfél szolgáltatási kérelmei a **támogatási jegyek** területen jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="02813-111">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02813-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="02813-112">Prerequisites</span></span>

- <span data-ttu-id="02813-113">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="02813-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="02813-114">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="02813-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="02813-115">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="02813-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="02813-116">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="02813-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="02813-117">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="02813-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="02813-118">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="02813-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="02813-119">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="02813-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="02813-120">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="02813-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="02813-121">C\#</span><span class="sxs-lookup"><span data-stu-id="02813-121">C\#</span></span>

<span data-ttu-id="02813-122">Az ügyfél összes szolgáltatási kérelmének megjelenítéséhez használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="02813-122">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="02813-123">Ezután hívja meg a [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) tulajdonságot, majd a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="02813-123">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="02813-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="02813-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="02813-125">**Projekt**: PartnerCenterSDK. FeaturesSamples **osztály**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="02813-125">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="02813-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="02813-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="02813-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="02813-127">Request syntax</span></span>

| <span data-ttu-id="02813-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="02813-128">Method</span></span>  | <span data-ttu-id="02813-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="02813-129">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="02813-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="02813-130">**GET**</span></span> | <span data-ttu-id="02813-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/servicerequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="02813-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="02813-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="02813-132">URI parameter</span></span>

<span data-ttu-id="02813-133">Használja az alábbi lekérdezési paramétert az ügyfélhez tartozó összes szolgáltatás kérésének beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="02813-133">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="02813-134">Név</span><span class="sxs-lookup"><span data-stu-id="02813-134">Name</span></span>                   | <span data-ttu-id="02813-135">Típus</span><span class="sxs-lookup"><span data-stu-id="02813-135">Type</span></span>     | <span data-ttu-id="02813-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="02813-136">Required</span></span> | <span data-ttu-id="02813-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="02813-137">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="02813-138">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="02813-138">**customer-tenant-id**</span></span> | <span data-ttu-id="02813-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="02813-139">**guid**</span></span> | <span data-ttu-id="02813-140">Y</span><span class="sxs-lookup"><span data-stu-id="02813-140">Y</span></span>        | <span data-ttu-id="02813-141">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="02813-141">A GUID corresponding to the customer..</span></span> |

### <a name="request-headers"></a><span data-ttu-id="02813-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="02813-142">Request headers</span></span>

<span data-ttu-id="02813-143">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="02813-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="02813-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="02813-144">Request body</span></span>

<span data-ttu-id="02813-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="02813-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="02813-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="02813-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="02813-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="02813-147">REST response</span></span>

<span data-ttu-id="02813-148">Ha a művelet sikeres, ez a metódus egy **szolgáltatási kérelem** erőforrásainak gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="02813-148">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="02813-149">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="02813-149">Response success and error codes</span></span>

<span data-ttu-id="02813-150">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="02813-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="02813-151">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="02813-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="02813-152">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="02813-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="02813-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="02813-153">Response example</span></span>

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
