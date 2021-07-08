---
title: Egy ügyfél felügyelt szolgáltatásainak lekérése azonosító alapján
description: Lekérte egy ügyfél felügyelt szolgáltatásait. Más szóval szerezze be az összes olyan ügyfél-előfizetés hivatkozásait, amelyekhez delegálta a rendszergazdai jogosultságokat. Ezekkel a hivatkozásokkal támogatási és fájlszolgáltatás-kérelmeket nyújthat a Microsoftnak.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cf7e7b62113bd96b00fdc2301e4e7ac4f5d4243
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548447"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="b5d88-105">Egy ügyfél felügyelt szolgáltatásainak lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="b5d88-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="b5d88-106">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b5d88-106">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b5d88-107">Lekérte egy ügyfél felügyelt szolgáltatásait.</span><span class="sxs-lookup"><span data-stu-id="b5d88-107">Gets the managed services for a customer.</span></span> <span data-ttu-id="b5d88-108">Más szóval szerezze be az összes olyan ügyfél-előfizetés hivatkozásait, amelyekhez delegálta a rendszergazdai jogosultságokat.</span><span class="sxs-lookup"><span data-stu-id="b5d88-108">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="b5d88-109">Ezekkel a hivatkozásokkal támogatási és fájlszolgáltatás-kérelmeket nyújthat a Microsoftnak.</span><span class="sxs-lookup"><span data-stu-id="b5d88-109">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5d88-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b5d88-110">Prerequisites</span></span>

- <span data-ttu-id="b5d88-111">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b5d88-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b5d88-112">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b5d88-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b5d88-113">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5d88-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b5d88-114">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b5d88-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b5d88-115">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b5d88-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b5d88-116">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b5d88-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b5d88-117">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="b5d88-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b5d88-118">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5d88-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b5d88-119">C\#</span><span class="sxs-lookup"><span data-stu-id="b5d88-119">C\#</span></span>

<span data-ttu-id="b5d88-120">Az ügyfél összes felügyelt szolgáltatásának megjelenítéséhez használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="b5d88-120">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="b5d88-121">Ezután hívja meg [**a ManagedServices tulajdonságot,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) majd a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) a [**GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="b5d88-121">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="b5d88-122">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b5d88-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b5d88-123">**Project:** PartnerCenterSDK.FeaturesSamples **osztály:** CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="b5d88-123">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b5d88-124">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="b5d88-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b5d88-125">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b5d88-125">Request syntax</span></span>

| <span data-ttu-id="b5d88-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="b5d88-126">Method</span></span>  | <span data-ttu-id="b5d88-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b5d88-127">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b5d88-128">**Kap**</span><span class="sxs-lookup"><span data-stu-id="b5d88-128">**GET**</span></span> | <span data-ttu-id="b5d88-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b5d88-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b5d88-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b5d88-130">URI parameter</span></span>

<span data-ttu-id="b5d88-131">A következő lekérdezési paraméterrel lekérdezheti az ügyfél felügyelt szolgáltatásait.</span><span class="sxs-lookup"><span data-stu-id="b5d88-131">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="b5d88-132">Név</span><span class="sxs-lookup"><span data-stu-id="b5d88-132">Name</span></span>                   | <span data-ttu-id="b5d88-133">Típus</span><span class="sxs-lookup"><span data-stu-id="b5d88-133">Type</span></span>     | <span data-ttu-id="b5d88-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b5d88-134">Required</span></span> | <span data-ttu-id="b5d88-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="b5d88-135">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="b5d88-136">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="b5d88-136">**customer-tenant-id**</span></span> | <span data-ttu-id="b5d88-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="b5d88-137">**guid**</span></span> | <span data-ttu-id="b5d88-138">Y</span><span class="sxs-lookup"><span data-stu-id="b5d88-138">Y</span></span>        | <span data-ttu-id="b5d88-139">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="b5d88-139">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b5d88-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b5d88-140">Request headers</span></span>

<span data-ttu-id="b5d88-141">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b5d88-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b5d88-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b5d88-142">Request body</span></span>

<span data-ttu-id="b5d88-143">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b5d88-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b5d88-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b5d88-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="b5d88-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b5d88-145">REST response</span></span>

<span data-ttu-id="b5d88-146">Ha a művelet sikeres, ez a metódus felügyeltszolgáltatás-objektumok gyűjteményét adja **vissza** a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="b5d88-146">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b5d88-147">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b5d88-147">Response success and error codes</span></span>

<span data-ttu-id="b5d88-148">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="b5d88-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b5d88-149">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="b5d88-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b5d88-150">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b5d88-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b5d88-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b5d88-151">Response example</span></span>

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
