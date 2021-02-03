---
title: Új ügyfél-konfigurációs házirend létrehozása
description: Ismerje meg, hogyan hozhat létre új konfigurációs házirendet a partner Center API-kkal egy adott ügyfélhez. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 21a0bfde7f931371ff09d6c27de0281a4ed3b3cb
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768639"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="f9833-104">Új konfigurációs szabályzat létrehozása a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="f9833-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="f9833-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="f9833-105">**Applies to:**</span></span>

- <span data-ttu-id="f9833-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f9833-106">Partner Center</span></span>
- <span data-ttu-id="f9833-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f9833-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="f9833-108">Új konfigurációs házirend létrehozása a megadott ügyfélhez.</span><span class="sxs-lookup"><span data-stu-id="f9833-108">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9833-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f9833-109">Prerequisites</span></span>

- <span data-ttu-id="f9833-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f9833-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f9833-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="f9833-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f9833-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9833-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f9833-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f9833-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f9833-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="f9833-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f9833-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f9833-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f9833-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="f9833-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f9833-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9833-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f9833-118">C\#</span><span class="sxs-lookup"><span data-stu-id="f9833-118">C\#</span></span>

<span data-ttu-id="f9833-119">Új konfigurációs házirend létrehozása a megadott ügyfélhez:</span><span class="sxs-lookup"><span data-stu-id="f9833-119">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="f9833-120">A következő kódrészletben látható módon hozza létre az új [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) objektumot.</span><span class="sxs-lookup"><span data-stu-id="f9833-120">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="f9833-121">Ezután hívja meg a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="f9833-121">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="f9833-122">Kérje le a [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) tulajdonságot, és szerezzen be egy felületet a konfigurációs házirend-gyűjtési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="f9833-122">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="f9833-123">A konfigurációs szabályzat létrehozásához hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="f9833-123">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="f9833-124">C \# példa</span><span class="sxs-lookup"><span data-stu-id="f9833-124">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

<span data-ttu-id="f9833-125">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9833-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f9833-126">**Projekt**: partner Center SDK Samples **osztály**: CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="f9833-126">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f9833-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f9833-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f9833-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f9833-128">Request syntax</span></span>

| <span data-ttu-id="f9833-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="f9833-129">Method</span></span>   | <span data-ttu-id="f9833-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f9833-130">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="f9833-131">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="f9833-131">**POST**</span></span> | <span data-ttu-id="f9833-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="f9833-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="f9833-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f9833-133">URI parameter</span></span>

<span data-ttu-id="f9833-134">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="f9833-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="f9833-135">Név</span><span class="sxs-lookup"><span data-stu-id="f9833-135">Name</span></span>        | <span data-ttu-id="f9833-136">Típus</span><span class="sxs-lookup"><span data-stu-id="f9833-136">Type</span></span>   | <span data-ttu-id="f9833-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f9833-137">Required</span></span> | <span data-ttu-id="f9833-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="f9833-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="f9833-139">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="f9833-139">customer-id</span></span> | <span data-ttu-id="f9833-140">sztring</span><span class="sxs-lookup"><span data-stu-id="f9833-140">string</span></span> | <span data-ttu-id="f9833-141">Igen</span><span class="sxs-lookup"><span data-stu-id="f9833-141">Yes</span></span>      | <span data-ttu-id="f9833-142">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="f9833-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f9833-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f9833-143">Request headers</span></span>

<span data-ttu-id="f9833-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f9833-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f9833-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f9833-145">Request body</span></span>

<span data-ttu-id="f9833-146">A kérelem törzsének tartalmaznia kell egy olyan objektumot, amely tartalmazza a konfigurációs házirend adatait az alábbi táblázatban leírtak szerint:</span><span class="sxs-lookup"><span data-stu-id="f9833-146">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="f9833-147">Név</span><span class="sxs-lookup"><span data-stu-id="f9833-147">Name</span></span>           | <span data-ttu-id="f9833-148">Típus</span><span class="sxs-lookup"><span data-stu-id="f9833-148">Type</span></span>             | <span data-ttu-id="f9833-149">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f9833-149">Required</span></span> | <span data-ttu-id="f9833-150">Leírás</span><span class="sxs-lookup"><span data-stu-id="f9833-150">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="f9833-151">name</span><span class="sxs-lookup"><span data-stu-id="f9833-151">name</span></span>           | <span data-ttu-id="f9833-152">sztring</span><span class="sxs-lookup"><span data-stu-id="f9833-152">string</span></span>           | <span data-ttu-id="f9833-153">Igen</span><span class="sxs-lookup"><span data-stu-id="f9833-153">Yes</span></span>      | <span data-ttu-id="f9833-154">A szabályzat rövid neve.</span><span class="sxs-lookup"><span data-stu-id="f9833-154">The friendly name of the policy.</span></span> |
| <span data-ttu-id="f9833-155">category</span><span class="sxs-lookup"><span data-stu-id="f9833-155">category</span></span>       | <span data-ttu-id="f9833-156">sztring</span><span class="sxs-lookup"><span data-stu-id="f9833-156">string</span></span>           | <span data-ttu-id="f9833-157">Igen</span><span class="sxs-lookup"><span data-stu-id="f9833-157">Yes</span></span>      | <span data-ttu-id="f9833-158">A szabályzat kategóriája.</span><span class="sxs-lookup"><span data-stu-id="f9833-158">The policy category.</span></span>             |
| <span data-ttu-id="f9833-159">leírás</span><span class="sxs-lookup"><span data-stu-id="f9833-159">description</span></span>    | <span data-ttu-id="f9833-160">sztring</span><span class="sxs-lookup"><span data-stu-id="f9833-160">string</span></span>           | <span data-ttu-id="f9833-161">No</span><span class="sxs-lookup"><span data-stu-id="f9833-161">No</span></span>       | <span data-ttu-id="f9833-162">A szabályzat leírása.</span><span class="sxs-lookup"><span data-stu-id="f9833-162">The policy description.</span></span>          |
| <span data-ttu-id="f9833-163">policySettings</span><span class="sxs-lookup"><span data-stu-id="f9833-163">policySettings</span></span> | <span data-ttu-id="f9833-164">sztringek tömbje</span><span class="sxs-lookup"><span data-stu-id="f9833-164">array of strings</span></span> | <span data-ttu-id="f9833-165">Igen</span><span class="sxs-lookup"><span data-stu-id="f9833-165">Yes</span></span>      | <span data-ttu-id="f9833-166">A házirend-beállítások.</span><span class="sxs-lookup"><span data-stu-id="f9833-166">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="f9833-167">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f9833-167">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="f9833-168">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f9833-168">REST response</span></span>

<span data-ttu-id="f9833-169">Ha a művelet sikeres, a válasz törzse tartalmazza az új szabályzathoz tartozó [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="f9833-169">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f9833-170">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f9833-170">Response success and error codes</span></span>

<span data-ttu-id="f9833-171">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f9833-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f9833-172">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f9833-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f9833-173">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="f9833-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f9833-174">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f9833-174">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
