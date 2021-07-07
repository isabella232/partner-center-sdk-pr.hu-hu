---
title: Új ügyfél-konfigurációs szabályzat létrehozása
description: Megtudhatja, hogyan hozhat létre Partnerközpont új konfigurációs szabályzatot egy adott ügyfél számára a Partnerközpont API-k használatával. A cikk előfeltételeket, lépéseket és példákat tartalmaz.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 530ff72862204bda093385252450f4eb81b63160
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973672"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="c9da4-104">Új konfigurációs szabályzat létrehozása a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="c9da4-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="c9da4-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="c9da4-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="c9da4-106">Új konfigurációs szabályzat létrehozása a megadott ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="c9da4-106">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9da4-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c9da4-107">Prerequisites</span></span>

- <span data-ttu-id="c9da4-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c9da4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c9da4-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="c9da4-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c9da4-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c9da4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c9da4-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="c9da4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c9da4-112">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="c9da4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c9da4-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="c9da4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c9da4-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="c9da4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c9da4-115">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c9da4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c9da4-116">C\#</span><span class="sxs-lookup"><span data-stu-id="c9da4-116">C\#</span></span>

<span data-ttu-id="c9da4-117">Új konfigurációs szabályzat létrehozása a megadott ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="c9da4-117">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="c9da4-118">Példányositsa az új [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) objektumot az alábbi kódrészletben látható módon.</span><span class="sxs-lookup"><span data-stu-id="c9da4-118">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="c9da4-119">Ezután hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával, hogy lekérje a műveletek interfészét a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="c9da4-119">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="c9da4-120">A [**ConfigurationPolicies tulajdonság lekérésével**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) lekéri a konfigurációs szabályzatgyűjtemény műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="c9da4-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="c9da4-121">A konfigurációs [**szabályzat létrehozásához**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) hívja meg a [**Create vagy a CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="c9da4-121">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="c9da4-122">C \# példa</span><span class="sxs-lookup"><span data-stu-id="c9da4-122">C\# example</span></span>

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

<span data-ttu-id="c9da4-123">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="c9da4-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c9da4-124">**Project**: Partnerközpont SDK **osztály:** CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="c9da4-124">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c9da4-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="c9da4-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c9da4-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c9da4-126">Request syntax</span></span>

| <span data-ttu-id="c9da4-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="c9da4-127">Method</span></span>   | <span data-ttu-id="c9da4-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c9da4-128">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="c9da4-129">**Post**</span><span class="sxs-lookup"><span data-stu-id="c9da4-129">**POST**</span></span> | <span data-ttu-id="c9da4-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c9da4-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="c9da4-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c9da4-131">URI parameter</span></span>

<span data-ttu-id="c9da4-132">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="c9da4-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="c9da4-133">Név</span><span class="sxs-lookup"><span data-stu-id="c9da4-133">Name</span></span>        | <span data-ttu-id="c9da4-134">Típus</span><span class="sxs-lookup"><span data-stu-id="c9da4-134">Type</span></span>   | <span data-ttu-id="c9da4-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c9da4-135">Required</span></span> | <span data-ttu-id="c9da4-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="c9da4-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="c9da4-137">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="c9da4-137">customer-id</span></span> | <span data-ttu-id="c9da4-138">sztring</span><span class="sxs-lookup"><span data-stu-id="c9da4-138">string</span></span> | <span data-ttu-id="c9da4-139">Igen</span><span class="sxs-lookup"><span data-stu-id="c9da4-139">Yes</span></span>      | <span data-ttu-id="c9da4-140">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="c9da4-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c9da4-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c9da4-141">Request headers</span></span>

<span data-ttu-id="c9da4-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c9da4-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c9da4-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c9da4-143">Request body</span></span>

<span data-ttu-id="c9da4-144">A kérelem törzsének tartalmaznia kell egy objektumot, amely tartalmazza a konfigurációs szabályzat adatait az alábbi táblázatban leírtak szerint:</span><span class="sxs-lookup"><span data-stu-id="c9da4-144">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="c9da4-145">Név</span><span class="sxs-lookup"><span data-stu-id="c9da4-145">Name</span></span>           | <span data-ttu-id="c9da4-146">Típus</span><span class="sxs-lookup"><span data-stu-id="c9da4-146">Type</span></span>             | <span data-ttu-id="c9da4-147">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c9da4-147">Required</span></span> | <span data-ttu-id="c9da4-148">Leírás</span><span class="sxs-lookup"><span data-stu-id="c9da4-148">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="c9da4-149">name</span><span class="sxs-lookup"><span data-stu-id="c9da4-149">name</span></span>           | <span data-ttu-id="c9da4-150">sztring</span><span class="sxs-lookup"><span data-stu-id="c9da4-150">string</span></span>           | <span data-ttu-id="c9da4-151">Igen</span><span class="sxs-lookup"><span data-stu-id="c9da4-151">Yes</span></span>      | <span data-ttu-id="c9da4-152">A szabályzat rövid neve.</span><span class="sxs-lookup"><span data-stu-id="c9da4-152">The friendly name of the policy.</span></span> |
| <span data-ttu-id="c9da4-153">category</span><span class="sxs-lookup"><span data-stu-id="c9da4-153">category</span></span>       | <span data-ttu-id="c9da4-154">sztring</span><span class="sxs-lookup"><span data-stu-id="c9da4-154">string</span></span>           | <span data-ttu-id="c9da4-155">Igen</span><span class="sxs-lookup"><span data-stu-id="c9da4-155">Yes</span></span>      | <span data-ttu-id="c9da4-156">A szabályzat kategóriája.</span><span class="sxs-lookup"><span data-stu-id="c9da4-156">The policy category.</span></span>             |
| <span data-ttu-id="c9da4-157">leírás</span><span class="sxs-lookup"><span data-stu-id="c9da4-157">description</span></span>    | <span data-ttu-id="c9da4-158">sztring</span><span class="sxs-lookup"><span data-stu-id="c9da4-158">string</span></span>           | <span data-ttu-id="c9da4-159">No</span><span class="sxs-lookup"><span data-stu-id="c9da4-159">No</span></span>       | <span data-ttu-id="c9da4-160">A szabályzat leírása.</span><span class="sxs-lookup"><span data-stu-id="c9da4-160">The policy description.</span></span>          |
| <span data-ttu-id="c9da4-161">policySettings</span><span class="sxs-lookup"><span data-stu-id="c9da4-161">policySettings</span></span> | <span data-ttu-id="c9da4-162">sztringek tömbje</span><span class="sxs-lookup"><span data-stu-id="c9da4-162">array of strings</span></span> | <span data-ttu-id="c9da4-163">Igen</span><span class="sxs-lookup"><span data-stu-id="c9da4-163">Yes</span></span>      | <span data-ttu-id="c9da4-164">A szabályzat beállításai.</span><span class="sxs-lookup"><span data-stu-id="c9da4-164">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="c9da4-165">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c9da4-165">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c9da4-166">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c9da4-166">REST response</span></span>

<span data-ttu-id="c9da4-167">Ha ez sikeres, a válasz törzse tartalmazza az új szabályzat [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="c9da4-167">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c9da4-168">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c9da4-168">Response success and error codes</span></span>

<span data-ttu-id="c9da4-169">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="c9da4-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c9da4-170">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="c9da4-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c9da4-171">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c9da4-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c9da4-172">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c9da4-172">Response example</span></span>

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
