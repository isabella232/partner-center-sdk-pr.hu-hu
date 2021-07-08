---
title: Egy ügyfél szabályzati listájának lekérése
description: A megadott ügyfél konfigurációs házirendek gyűjteményének lekérése.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bf6ace0d2425e28d80c4f2310878c2d2a9e2a876
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874584"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="6b1dd-103">Egy ügyfél szabályzati listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="6b1dd-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="6b1dd-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="6b1dd-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="6b1dd-105">Ez a cikk azt ismerteti, hogyan lehet lekérni a megadott ügyfél konfigurációs szabályzatának gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-105">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b1dd-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6b1dd-106">Prerequisites</span></span>

- <span data-ttu-id="6b1dd-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6b1dd-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6b1dd-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6b1dd-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6b1dd-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6b1dd-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6b1dd-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6b1dd-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6b1dd-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6b1dd-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6b1dd-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6b1dd-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="6b1dd-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6b1dd-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6b1dd-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6b1dd-115">C\#</span><span class="sxs-lookup"><span data-stu-id="6b1dd-115">C\#</span></span>

<span data-ttu-id="6b1dd-116">Az ügyfél összes szabályzatának listáját a következővel lehet lekérte:</span><span class="sxs-lookup"><span data-stu-id="6b1dd-116">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="6b1dd-117">Hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="6b1dd-118">A [**ConfigurationPolicies tulajdonság lekérésével**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) lekéri a konfigurációs szabályzatgyűjtemény műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-118">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="6b1dd-119">A [**szabályzatgyűjtemény lekéréséhez**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) hívja meg a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="6b1dd-120">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="6b1dd-120">For an example, see the following:</span></span>

- <span data-ttu-id="6b1dd-121">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6b1dd-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="6b1dd-122">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="6b1dd-122">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="6b1dd-123">Osztály: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="6b1dd-123">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="6b1dd-124">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="6b1dd-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6b1dd-125">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6b1dd-125">Request syntax</span></span>

| <span data-ttu-id="6b1dd-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="6b1dd-126">Method</span></span>  | <span data-ttu-id="6b1dd-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6b1dd-127">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="6b1dd-128">**Kap**</span><span class="sxs-lookup"><span data-stu-id="6b1dd-128">**GET**</span></span> | <span data-ttu-id="6b1dd-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6b1dd-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="6b1dd-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="6b1dd-130">URI parameter</span></span>

<span data-ttu-id="6b1dd-131">A kérelem létrehozásakor használja a következő elérésiút-paramétert:</span><span class="sxs-lookup"><span data-stu-id="6b1dd-131">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="6b1dd-132">Név</span><span class="sxs-lookup"><span data-stu-id="6b1dd-132">Name</span></span>        | <span data-ttu-id="6b1dd-133">Típus</span><span class="sxs-lookup"><span data-stu-id="6b1dd-133">Type</span></span>   | <span data-ttu-id="6b1dd-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6b1dd-134">Required</span></span> | <span data-ttu-id="6b1dd-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="6b1dd-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="6b1dd-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="6b1dd-136">customer-id</span></span> | <span data-ttu-id="6b1dd-137">sztring</span><span class="sxs-lookup"><span data-stu-id="6b1dd-137">string</span></span> | <span data-ttu-id="6b1dd-138">Igen</span><span class="sxs-lookup"><span data-stu-id="6b1dd-138">Yes</span></span>      | <span data-ttu-id="6b1dd-139">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6b1dd-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6b1dd-140">Request headers</span></span>

<span data-ttu-id="6b1dd-141">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6b1dd-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6b1dd-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6b1dd-142">Request body</span></span>

<span data-ttu-id="6b1dd-143">None</span><span class="sxs-lookup"><span data-stu-id="6b1dd-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="6b1dd-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6b1dd-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6b1dd-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6b1dd-145">REST response</span></span>

<span data-ttu-id="6b1dd-146">Ha a művelet sikeres, a válasz törzse [tartalmazza a ConfigurationPolicy erőforrások gyűjteményét.](device-deployment-resources.md#configurationpolicy)</span><span class="sxs-lookup"><span data-stu-id="6b1dd-146">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6b1dd-147">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6b1dd-147">Response success and error codes</span></span>

<span data-ttu-id="6b1dd-148">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6b1dd-149">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="6b1dd-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6b1dd-150">A teljes listát a REST Partnerközpont [hibakódokat.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6b1dd-150">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6b1dd-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6b1dd-151">Response example</span></span>

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
