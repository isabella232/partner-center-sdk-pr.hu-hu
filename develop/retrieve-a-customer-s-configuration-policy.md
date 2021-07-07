---
title: Egy ügyfél konfigurációs szabályzatának lekérése
description: A megadott ügyfélhez megadott konfigurációs szabályzat lekérése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f9a8cb435c63d8d02c3b4633abc8723353116f37
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547495"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="072a8-103">Egy ügyfél konfigurációs szabályzatának lekérése</span><span class="sxs-lookup"><span data-stu-id="072a8-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="072a8-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="072a8-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="072a8-105">A megadott ügyfélhez megadott konfigurációs szabályzat lekérése.</span><span class="sxs-lookup"><span data-stu-id="072a8-105">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="072a8-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="072a8-106">Prerequisites</span></span>

- <span data-ttu-id="072a8-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="072a8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="072a8-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="072a8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="072a8-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="072a8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="072a8-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="072a8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="072a8-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="072a8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="072a8-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="072a8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="072a8-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="072a8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="072a8-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="072a8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="072a8-115">A szabályzat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="072a8-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="072a8-116">C\#</span><span class="sxs-lookup"><span data-stu-id="072a8-116">C\#</span></span>

<span data-ttu-id="072a8-117">A megadott ügyfél konfigurációs szabályzatának lekérése érdekében először hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával, hogy lekérje a megadott ügyfél műveleteinek interfészét.</span><span class="sxs-lookup"><span data-stu-id="072a8-117">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="072a8-118">Ezután hívja meg a [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a szabályzat azonosítójával, hogy lekérje a megadott szabályzat konfigurációs házirend-műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="072a8-118">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="072a8-119">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) vagy [**GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) a konfigurációs szabályzat lekérése érdekében.</span><span class="sxs-lookup"><span data-stu-id="072a8-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="072a8-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="072a8-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="072a8-121">**Project**: Partnerközpont SDK **Osztály:** GetConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="072a8-121">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="072a8-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="072a8-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="072a8-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="072a8-123">Request syntax</span></span>

| <span data-ttu-id="072a8-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="072a8-124">Method</span></span>  | <span data-ttu-id="072a8-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="072a8-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="072a8-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="072a8-126">**GET**</span></span> | <span data-ttu-id="072a8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="072a8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="072a8-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="072a8-128">URI parameter</span></span>

<span data-ttu-id="072a8-129">A kérelem létrehozásakor használja a következő elérési utat és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="072a8-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="072a8-130">Név</span><span class="sxs-lookup"><span data-stu-id="072a8-130">Name</span></span>        | <span data-ttu-id="072a8-131">Típus</span><span class="sxs-lookup"><span data-stu-id="072a8-131">Type</span></span>   | <span data-ttu-id="072a8-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="072a8-132">Required</span></span> | <span data-ttu-id="072a8-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="072a8-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="072a8-134">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="072a8-134">customer-id</span></span> | <span data-ttu-id="072a8-135">sztring</span><span class="sxs-lookup"><span data-stu-id="072a8-135">string</span></span> | <span data-ttu-id="072a8-136">Igen</span><span class="sxs-lookup"><span data-stu-id="072a8-136">Yes</span></span>      | <span data-ttu-id="072a8-137">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="072a8-137">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="072a8-138">policy-id</span><span class="sxs-lookup"><span data-stu-id="072a8-138">policy-id</span></span>   | <span data-ttu-id="072a8-139">sztring</span><span class="sxs-lookup"><span data-stu-id="072a8-139">string</span></span> | <span data-ttu-id="072a8-140">Igen</span><span class="sxs-lookup"><span data-stu-id="072a8-140">Yes</span></span>      | <span data-ttu-id="072a8-141">Egy GUID-formátumú sztring, amely azonosítja a szabályzatot.</span><span class="sxs-lookup"><span data-stu-id="072a8-141">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="072a8-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="072a8-142">Request headers</span></span>

<span data-ttu-id="072a8-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="072a8-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="072a8-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="072a8-144">Request body</span></span>

<span data-ttu-id="072a8-145">None</span><span class="sxs-lookup"><span data-stu-id="072a8-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="072a8-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="072a8-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="072a8-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="072a8-147">REST response</span></span>

<span data-ttu-id="072a8-148">Ha a művelet sikeres, a válasz tartalmazza a kért [ConfigurationPolicy erőforrást.](device-deployment-resources.md#configurationpolicy)</span><span class="sxs-lookup"><span data-stu-id="072a8-148">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="072a8-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="072a8-149">Response success and error codes</span></span>

<span data-ttu-id="072a8-150">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="072a8-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="072a8-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="072a8-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="072a8-152">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="072a8-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="072a8-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="072a8-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
