---
title: Konfigurációs szabályzat frissítése a megadott ügyfélnél
description: A megadott ügyfélhez megadott konfigurációs szabályzat frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5e008f41a44f2b7cf3ddfd705505175c69bbad38
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530233"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="4b3c9-103">Konfigurációs szabályzat frissítése a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="4b3c9-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="4b3c9-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="4b3c9-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="4b3c9-105">A megadott ügyfélhez megadott konfigurációs szabályzat frissítése.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-105">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b3c9-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4b3c9-106">Prerequisites</span></span>

- <span data-ttu-id="4b3c9-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4b3c9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4b3c9-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4b3c9-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4b3c9-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4b3c9-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4b3c9-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4b3c9-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4b3c9-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4b3c9-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4b3c9-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4b3c9-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="4b3c9-113">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4b3c9-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4b3c9-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4b3c9-115">A szabályzat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="4b3c9-116">C\#</span><span class="sxs-lookup"><span data-stu-id="4b3c9-116">C\#</span></span>

<span data-ttu-id="4b3c9-117">A megadott ügyfél meglévő konfigurációs szabályzatának frissítéséhez az alábbi kódrészletben látható módon példányositsa az új [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) objektumot.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-117">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="4b3c9-118">Az új objektumban lévő értékek lecserélik a meglévő objektum megfelelő értékeit.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-118">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="4b3c9-119">Ezután hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával, hogy lekérje a megadott ügyfél műveleteinek interfészét.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-119">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="4b3c9-120">Ezután hívja meg a [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a szabályzat azonosítójával, hogy lekérje a megadott házirend konfigurációs házirendműveletei felületét.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="4b3c9-121">Végül hívja meg a [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) vagy [**a PatchAsync metódust**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) a konfigurációs szabályzat frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-121">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

<span data-ttu-id="4b3c9-122">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4b3c9-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4b3c9-123">**Project:** Partnerközpont SDK **Osztály:** UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="4b3c9-123">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4b3c9-124">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4b3c9-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4b3c9-125">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4b3c9-125">Request syntax</span></span>

| <span data-ttu-id="4b3c9-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="4b3c9-126">Method</span></span>  | <span data-ttu-id="4b3c9-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4b3c9-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4b3c9-128">**PUT**</span><span class="sxs-lookup"><span data-stu-id="4b3c9-128">**PUT**</span></span> | <span data-ttu-id="4b3c9-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/policies/{szabályzatazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4b3c9-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4b3c9-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4b3c9-130">URI parameter</span></span>

<span data-ttu-id="4b3c9-131">A kérelem létrehozásakor használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="4b3c9-132">Név</span><span class="sxs-lookup"><span data-stu-id="4b3c9-132">Name</span></span>        | <span data-ttu-id="4b3c9-133">Típus</span><span class="sxs-lookup"><span data-stu-id="4b3c9-133">Type</span></span>   | <span data-ttu-id="4b3c9-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4b3c9-134">Required</span></span> | <span data-ttu-id="4b3c9-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="4b3c9-135">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="4b3c9-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="4b3c9-136">customer-id</span></span> | <span data-ttu-id="4b3c9-137">sztring</span><span class="sxs-lookup"><span data-stu-id="4b3c9-137">string</span></span> | <span data-ttu-id="4b3c9-138">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-138">Yes</span></span>      | <span data-ttu-id="4b3c9-139">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-139">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="4b3c9-140">policy-id</span><span class="sxs-lookup"><span data-stu-id="4b3c9-140">policy-id</span></span>   | <span data-ttu-id="4b3c9-141">sztring</span><span class="sxs-lookup"><span data-stu-id="4b3c9-141">string</span></span> | <span data-ttu-id="4b3c9-142">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-142">Yes</span></span>      | <span data-ttu-id="4b3c9-143">Egy GUID-formátumú sztring, amely azonosítja a frissíteni kívánt szabályzatot.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-143">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4b3c9-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4b3c9-144">Request headers</span></span>

<span data-ttu-id="4b3c9-145">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4b3c9-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4b3c9-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4b3c9-146">Request body</span></span>

<span data-ttu-id="4b3c9-147">A kérelem törzsének tartalmaznia kell egy objektumot, amely a szabályzat adatait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-147">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="4b3c9-148">Név</span><span class="sxs-lookup"><span data-stu-id="4b3c9-148">Name</span></span>            | <span data-ttu-id="4b3c9-149">Típus</span><span class="sxs-lookup"><span data-stu-id="4b3c9-149">Type</span></span>             | <span data-ttu-id="4b3c9-150">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4b3c9-150">Required</span></span> | <span data-ttu-id="4b3c9-151">Frissíthető</span><span class="sxs-lookup"><span data-stu-id="4b3c9-151">Updatable</span></span> | <span data-ttu-id="4b3c9-152">Leírás</span><span class="sxs-lookup"><span data-stu-id="4b3c9-152">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4b3c9-153">id</span><span class="sxs-lookup"><span data-stu-id="4b3c9-153">id</span></span>              | <span data-ttu-id="4b3c9-154">sztring</span><span class="sxs-lookup"><span data-stu-id="4b3c9-154">string</span></span>           | <span data-ttu-id="4b3c9-155">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-155">Yes</span></span>      | <span data-ttu-id="4b3c9-156">Nem</span><span class="sxs-lookup"><span data-stu-id="4b3c9-156">No</span></span>        | <span data-ttu-id="4b3c9-157">A szabályzatot azonosító GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-157">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="4b3c9-158">name</span><span class="sxs-lookup"><span data-stu-id="4b3c9-158">name</span></span>            | <span data-ttu-id="4b3c9-159">sztring</span><span class="sxs-lookup"><span data-stu-id="4b3c9-159">string</span></span>           | <span data-ttu-id="4b3c9-160">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-160">Yes</span></span>      | <span data-ttu-id="4b3c9-161">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-161">Yes</span></span>       | <span data-ttu-id="4b3c9-162">A szabályzat rövid neve.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-162">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="4b3c9-163">category</span><span class="sxs-lookup"><span data-stu-id="4b3c9-163">category</span></span>        | <span data-ttu-id="4b3c9-164">sztring</span><span class="sxs-lookup"><span data-stu-id="4b3c9-164">string</span></span>           | <span data-ttu-id="4b3c9-165">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-165">Yes</span></span>      | <span data-ttu-id="4b3c9-166">Nem</span><span class="sxs-lookup"><span data-stu-id="4b3c9-166">No</span></span>        | <span data-ttu-id="4b3c9-167">A szabályzat kategóriája.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-167">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="4b3c9-168">leírás</span><span class="sxs-lookup"><span data-stu-id="4b3c9-168">description</span></span>     | <span data-ttu-id="4b3c9-169">sztring</span><span class="sxs-lookup"><span data-stu-id="4b3c9-169">string</span></span>           | <span data-ttu-id="4b3c9-170">Nem</span><span class="sxs-lookup"><span data-stu-id="4b3c9-170">No</span></span>       | <span data-ttu-id="4b3c9-171">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-171">Yes</span></span>       | <span data-ttu-id="4b3c9-172">A szabályzat leírása.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-172">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="4b3c9-173">devicesAssigned (hozzárendelt eszközök)</span><span class="sxs-lookup"><span data-stu-id="4b3c9-173">devicesAssigned</span></span> | <span data-ttu-id="4b3c9-174">szám</span><span class="sxs-lookup"><span data-stu-id="4b3c9-174">number</span></span>           | <span data-ttu-id="4b3c9-175">Nem</span><span class="sxs-lookup"><span data-stu-id="4b3c9-175">No</span></span>       | <span data-ttu-id="4b3c9-176">Nem</span><span class="sxs-lookup"><span data-stu-id="4b3c9-176">No</span></span>        | <span data-ttu-id="4b3c9-177">Az eszközök száma.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-177">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="4b3c9-178">policySettings</span><span class="sxs-lookup"><span data-stu-id="4b3c9-178">policySettings</span></span>  | <span data-ttu-id="4b3c9-179">sztringek tömbje</span><span class="sxs-lookup"><span data-stu-id="4b3c9-179">array of strings</span></span> | <span data-ttu-id="4b3c9-180">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-180">Yes</span></span>      | <span data-ttu-id="4b3c9-181">Igen</span><span class="sxs-lookup"><span data-stu-id="4b3c9-181">Yes</span></span>       | <span data-ttu-id="4b3c9-182">A szabályzat beállításai: "none","remove \_ oem \_ preinstalls","oobe \_ user not local \_ \_ \_ admin","skip \_ express \_ settings","skip \_ oem \_ registration,"skip \_ eula".</span><span class="sxs-lookup"><span data-stu-id="4b3c9-182">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="4b3c9-183">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4b3c9-183">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="4b3c9-184">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4b3c9-184">REST response</span></span>

<span data-ttu-id="4b3c9-185">Ha ez sikeres, a válasz törzse tartalmazza az új szabályzat [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-185">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4b3c9-186">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4b3c9-186">Response success and error codes</span></span>

<span data-ttu-id="4b3c9-187">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4b3c9-188">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4b3c9-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4b3c9-189">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4b3c9-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4b3c9-190">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4b3c9-190">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
