---
title: Egy ügyfél szabályzati listájának lekérése
description: A megadott ügyfél konfigurációs házirendjei gyűjteményének beolvasása.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 16886b1adca393ed2967f2a4fe74a379bef1c1c7
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768100"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="7669f-103">Egy ügyfél szabályzati listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="7669f-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="7669f-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="7669f-104">**Applies to:**</span></span>

- <span data-ttu-id="7669f-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="7669f-105">Partner Center</span></span>
- <span data-ttu-id="7669f-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="7669f-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7669f-107">Ez a cikk azt ismerteti, hogyan kérhető le a megadott ügyfél konfigurációs házirendjeinek gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="7669f-107">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7669f-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7669f-108">Prerequisites</span></span>

- <span data-ttu-id="7669f-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="7669f-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7669f-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="7669f-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7669f-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7669f-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7669f-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="7669f-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7669f-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="7669f-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7669f-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="7669f-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7669f-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="7669f-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7669f-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7669f-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7669f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7669f-117">C\#</span></span>

<span data-ttu-id="7669f-118">Az összes ügyfél szabályzatának beszerzése:</span><span class="sxs-lookup"><span data-stu-id="7669f-118">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="7669f-119">Hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="7669f-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="7669f-120">Kérje le a [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) tulajdonságot, és szerezzen be egy felületet a konfigurációs házirend-gyűjtési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="7669f-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="7669f-121">A [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) metódus meghívásával kérheti le a szabályzatok gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="7669f-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="7669f-122">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="7669f-122">For an example, see the following:</span></span>

- <span data-ttu-id="7669f-123">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7669f-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7669f-124">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="7669f-124">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="7669f-125">Osztály: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="7669f-125">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7669f-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="7669f-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7669f-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7669f-127">Request syntax</span></span>

| <span data-ttu-id="7669f-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="7669f-128">Method</span></span>  | <span data-ttu-id="7669f-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7669f-129">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="7669f-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="7669f-130">**GET**</span></span> | <span data-ttu-id="7669f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="7669f-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="7669f-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="7669f-132">URI parameter</span></span>

<span data-ttu-id="7669f-133">A kérelem létrehozásakor használja a következő Path paramétert:</span><span class="sxs-lookup"><span data-stu-id="7669f-133">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="7669f-134">Név</span><span class="sxs-lookup"><span data-stu-id="7669f-134">Name</span></span>        | <span data-ttu-id="7669f-135">Típus</span><span class="sxs-lookup"><span data-stu-id="7669f-135">Type</span></span>   | <span data-ttu-id="7669f-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7669f-136">Required</span></span> | <span data-ttu-id="7669f-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="7669f-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="7669f-138">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="7669f-138">customer-id</span></span> | <span data-ttu-id="7669f-139">sztring</span><span class="sxs-lookup"><span data-stu-id="7669f-139">string</span></span> | <span data-ttu-id="7669f-140">Igen</span><span class="sxs-lookup"><span data-stu-id="7669f-140">Yes</span></span>      | <span data-ttu-id="7669f-141">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="7669f-141">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7669f-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7669f-142">Request headers</span></span>

<span data-ttu-id="7669f-143">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7669f-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7669f-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7669f-144">Request body</span></span>

<span data-ttu-id="7669f-145">Nincs</span><span class="sxs-lookup"><span data-stu-id="7669f-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7669f-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7669f-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
Content-Length:0
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7669f-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7669f-147">REST response</span></span>

<span data-ttu-id="7669f-148">Ha ez sikeres, a válasz törzse tartalmazza a [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -erőforrások gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="7669f-148">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7669f-149">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7669f-149">Response success and error codes</span></span>

<span data-ttu-id="7669f-150">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="7669f-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7669f-151">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="7669f-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7669f-152">Teljes listát a következő témakörben talál: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="7669f-152">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7669f-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7669f-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1221
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d5ff2573-3ef8-4553-aac4-4b73d97dce1b
MS-RequestId: 6eb7383d-eeb5-44d7-8570-e0ed12c0547a
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:49 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "8c7d25aa-2dbb-409c-a1f0-f55bd9108fa9",
            "name": "Windows 10 Enterprise E3",
            "category": "o_o_b_e",
            "description": "P462017 description",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-04-27T11:30:34.1944704-07:00",
            "lastModifiedDate": "2017-04-27T11:30:34.1944704-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
            "name": "Test policy",
            "category": "o_o_b_e",
            "description": "Test policy creation from API 1",
            "devicesAssigned": 0,
            "policySettings": ["skip_express_settings"],
            "createdDate": "2017-07-25T11:03:03.8457088-07:00",
            "lastModifiedDate": "2017-07-25T11:04:00.8150016-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "a96b5fd9-0f3a-419a-b55c-a8aecd6b1f00",
            "name": "Windows 10 Enterprise E5",
            "category": "o_o_b_e",
            "description": "test policy creation from API",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-07-25T11:07:36.1501184-07:00",
            "lastModifiedDate": "2017-07-25T11:07:36.1501184-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
