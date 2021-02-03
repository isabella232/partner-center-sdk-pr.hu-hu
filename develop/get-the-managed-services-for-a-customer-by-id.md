---
title: Egy ügyfél felügyelt szolgáltatásainak lekérése azonosító alapján
description: Lekéri az ügyfél felügyelt szolgáltatásait. Más szóval az összes ügyfél-előfizetésre mutató hivatkozásokat kap, amelyekhez delegált rendszergazdai jogosultságokkal rendelkezik. Ezekkel a hivatkozásokkal támogatást és Fájlszolgáltatások-kéréseket biztosíthat a Microsofttal.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4764fce6a80035ea4b9dcc6677a3da28fc863eb7
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768408"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="40dfb-105">Egy ügyfél felügyelt szolgáltatásainak lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="40dfb-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="40dfb-106">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="40dfb-106">**Applies To**</span></span>

- <span data-ttu-id="40dfb-107">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="40dfb-107">Partner Center</span></span>
- <span data-ttu-id="40dfb-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="40dfb-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="40dfb-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="40dfb-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="40dfb-110">Lekéri az ügyfél felügyelt szolgáltatásait.</span><span class="sxs-lookup"><span data-stu-id="40dfb-110">Gets the managed services for a customer.</span></span> <span data-ttu-id="40dfb-111">Más szóval az összes ügyfél-előfizetésre mutató hivatkozásokat kap, amelyekhez delegált rendszergazdai jogosultságokkal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="40dfb-111">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="40dfb-112">Ezekkel a hivatkozásokkal támogatást és Fájlszolgáltatások-kéréseket biztosíthat a Microsofttal.</span><span class="sxs-lookup"><span data-stu-id="40dfb-112">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40dfb-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="40dfb-113">Prerequisites</span></span>

- <span data-ttu-id="40dfb-114">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="40dfb-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="40dfb-115">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="40dfb-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="40dfb-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40dfb-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="40dfb-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="40dfb-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="40dfb-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="40dfb-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="40dfb-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="40dfb-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="40dfb-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="40dfb-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="40dfb-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40dfb-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="40dfb-122">C\#</span><span class="sxs-lookup"><span data-stu-id="40dfb-122">C\#</span></span>

<span data-ttu-id="40dfb-123">Az ügyfélhez tartozó összes felügyelt szolgáltatás listájának megjelenítéséhez használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="40dfb-123">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="40dfb-124">Ezután hívja meg a [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) tulajdonságot, majd a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="40dfb-124">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="40dfb-125">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="40dfb-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="40dfb-126">**Projekt**: PartnerCenterSDK. FeaturesSamples **osztály**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="40dfb-126">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="40dfb-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="40dfb-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="40dfb-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="40dfb-128">Request syntax</span></span>

| <span data-ttu-id="40dfb-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="40dfb-129">Method</span></span>  | <span data-ttu-id="40dfb-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="40dfb-130">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40dfb-131">**GET**</span><span class="sxs-lookup"><span data-stu-id="40dfb-131">**GET**</span></span> | <span data-ttu-id="40dfb-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/managedservices http/1.1</span><span class="sxs-lookup"><span data-stu-id="40dfb-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="40dfb-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="40dfb-133">URI parameter</span></span>

<span data-ttu-id="40dfb-134">Az ügyfél felügyelt szolgáltatásainak beszerzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="40dfb-134">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="40dfb-135">Név</span><span class="sxs-lookup"><span data-stu-id="40dfb-135">Name</span></span>                   | <span data-ttu-id="40dfb-136">Típus</span><span class="sxs-lookup"><span data-stu-id="40dfb-136">Type</span></span>     | <span data-ttu-id="40dfb-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="40dfb-137">Required</span></span> | <span data-ttu-id="40dfb-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="40dfb-138">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="40dfb-139">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="40dfb-139">**customer-tenant-id**</span></span> | <span data-ttu-id="40dfb-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="40dfb-140">**guid**</span></span> | <span data-ttu-id="40dfb-141">Y</span><span class="sxs-lookup"><span data-stu-id="40dfb-141">Y</span></span>        | <span data-ttu-id="40dfb-142">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="40dfb-142">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="40dfb-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="40dfb-143">Request headers</span></span>

<span data-ttu-id="40dfb-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="40dfb-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="40dfb-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="40dfb-145">Request body</span></span>

<span data-ttu-id="40dfb-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="40dfb-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="40dfb-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="40dfb-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="40dfb-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="40dfb-148">REST response</span></span>

<span data-ttu-id="40dfb-149">Ha a művelet sikeres, ez a módszer **felügyelt szolgáltatási** objektumok gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="40dfb-149">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="40dfb-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="40dfb-150">Response success and error codes</span></span>

<span data-ttu-id="40dfb-151">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="40dfb-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="40dfb-152">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="40dfb-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="40dfb-153">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="40dfb-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="40dfb-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="40dfb-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
