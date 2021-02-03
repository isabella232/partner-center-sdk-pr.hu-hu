---
title: Egy ügyfél konfigurációs szabályzatának lekérése
description: A megadott ügyfél konfigurációs szabályzatának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d5d4ee83d1a66f33872d8b1f1327f47eeb4465e
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768400"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="80158-103">Egy ügyfél konfigurációs szabályzatának lekérése</span><span class="sxs-lookup"><span data-stu-id="80158-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="80158-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="80158-104">**Applies To**</span></span>

- <span data-ttu-id="80158-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="80158-105">Partner Center</span></span>
- <span data-ttu-id="80158-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="80158-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="80158-107">A megadott ügyfél konfigurációs szabályzatának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="80158-107">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80158-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="80158-108">Prerequisites</span></span>

- <span data-ttu-id="80158-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="80158-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80158-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="80158-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="80158-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80158-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80158-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="80158-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80158-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="80158-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80158-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="80158-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80158-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="80158-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80158-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80158-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="80158-117">A házirend-azonosító.</span><span class="sxs-lookup"><span data-stu-id="80158-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="80158-118">C\#</span><span class="sxs-lookup"><span data-stu-id="80158-118">C\#</span></span>

<span data-ttu-id="80158-119">A megadott ügyfélhez tartozó konfigurációs szabályzat lekéréséhez először hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="80158-119">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="80158-120">Ezután hívja meg a [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a házirend-azonosítóval, hogy lekérje az adott szabályzathoz tartozó konfigurációs házirend műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="80158-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="80158-121">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) metódust a konfigurációs szabályzat lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="80158-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="80158-122">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80158-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80158-123">**Projekt**: partner Center SDK Samples **osztály**: GetConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="80158-123">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="80158-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="80158-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80158-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="80158-125">Request syntax</span></span>

| <span data-ttu-id="80158-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="80158-126">Method</span></span>  | <span data-ttu-id="80158-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="80158-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80158-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="80158-128">**GET**</span></span> | <span data-ttu-id="80158-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="80158-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="80158-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="80158-130">URI parameter</span></span>

<span data-ttu-id="80158-131">A kérelem létrehozásakor használja az alábbi elérési utat és a lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="80158-131">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="80158-132">Név</span><span class="sxs-lookup"><span data-stu-id="80158-132">Name</span></span>        | <span data-ttu-id="80158-133">Típus</span><span class="sxs-lookup"><span data-stu-id="80158-133">Type</span></span>   | <span data-ttu-id="80158-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="80158-134">Required</span></span> | <span data-ttu-id="80158-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="80158-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="80158-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="80158-136">customer-id</span></span> | <span data-ttu-id="80158-137">sztring</span><span class="sxs-lookup"><span data-stu-id="80158-137">string</span></span> | <span data-ttu-id="80158-138">Igen</span><span class="sxs-lookup"><span data-stu-id="80158-138">Yes</span></span>      | <span data-ttu-id="80158-139">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="80158-139">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="80158-140">házirend-azonosító</span><span class="sxs-lookup"><span data-stu-id="80158-140">policy-id</span></span>   | <span data-ttu-id="80158-141">sztring</span><span class="sxs-lookup"><span data-stu-id="80158-141">string</span></span> | <span data-ttu-id="80158-142">Igen</span><span class="sxs-lookup"><span data-stu-id="80158-142">Yes</span></span>      | <span data-ttu-id="80158-143">Egy GUID-formázott karakterlánc, amely azonosítja a szabályzatot.</span><span class="sxs-lookup"><span data-stu-id="80158-143">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="80158-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="80158-144">Request headers</span></span>

<span data-ttu-id="80158-145">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="80158-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80158-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="80158-146">Request body</span></span>

<span data-ttu-id="80158-147">Nincs</span><span class="sxs-lookup"><span data-stu-id="80158-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="80158-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="80158-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="80158-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="80158-149">REST response</span></span>

<span data-ttu-id="80158-150">Ha a művelet sikeres, a válasz tartalmazza a kért [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="80158-150">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80158-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="80158-151">Response success and error codes</span></span>

<span data-ttu-id="80158-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="80158-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80158-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="80158-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80158-154">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="80158-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80158-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="80158-155">Response example</span></span>

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
