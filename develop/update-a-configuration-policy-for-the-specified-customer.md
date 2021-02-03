---
title: Konfigurációs szabályzat frissítése a megadott ügyfélnél
description: A megadott ügyfél konfigurációs házirendjének frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bf3b6f4db7516779c157b647725368ff0e4a570
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768403"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="51acc-103">Konfigurációs szabályzat frissítése a megadott ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="51acc-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="51acc-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="51acc-104">**Applies To**</span></span>

- <span data-ttu-id="51acc-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="51acc-105">Partner Center</span></span>
- <span data-ttu-id="51acc-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="51acc-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="51acc-107">A megadott ügyfél konfigurációs házirendjének frissítése.</span><span class="sxs-lookup"><span data-stu-id="51acc-107">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51acc-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="51acc-108">Prerequisites</span></span>

- <span data-ttu-id="51acc-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="51acc-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="51acc-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="51acc-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="51acc-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="51acc-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="51acc-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="51acc-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="51acc-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="51acc-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="51acc-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="51acc-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="51acc-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="51acc-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="51acc-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="51acc-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="51acc-117">A házirend-azonosító.</span><span class="sxs-lookup"><span data-stu-id="51acc-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="51acc-118">C\#</span><span class="sxs-lookup"><span data-stu-id="51acc-118">C\#</span></span>

<span data-ttu-id="51acc-119">Ha frissíteni szeretne egy meglévő konfigurációs házirendet a megadott ügyfél számára, egy új [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) objektumot hoz létre, ahogy az a következő kódrészletben látható.</span><span class="sxs-lookup"><span data-stu-id="51acc-119">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="51acc-120">Az új objektum értékei a meglévő objektum megfelelő értékeit cserélik le.</span><span class="sxs-lookup"><span data-stu-id="51acc-120">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="51acc-121">Ezután hívja meg a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a műveletekre a megadott ügyfélen.</span><span class="sxs-lookup"><span data-stu-id="51acc-121">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="51acc-122">Ezután hívja meg a [**ConfigurationPolicies. ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) metódust a házirend-azonosítóval, hogy lekérje az adott szabályzathoz tartozó konfigurációs házirend műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="51acc-122">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="51acc-123">Végül hívja meg a [**patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) vagy a [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) metódust a konfigurációs szabályzat frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="51acc-123">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

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

<span data-ttu-id="51acc-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="51acc-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="51acc-125">**Projekt**: partner Center SDK Samples **osztály**: UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="51acc-125">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="51acc-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="51acc-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="51acc-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="51acc-127">Request syntax</span></span>

| <span data-ttu-id="51acc-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="51acc-128">Method</span></span>  | <span data-ttu-id="51acc-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="51acc-129">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="51acc-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="51acc-130">**PUT**</span></span> | <span data-ttu-id="51acc-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="51acc-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="51acc-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="51acc-132">URI parameter</span></span>

<span data-ttu-id="51acc-133">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="51acc-133">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="51acc-134">Név</span><span class="sxs-lookup"><span data-stu-id="51acc-134">Name</span></span>        | <span data-ttu-id="51acc-135">Típus</span><span class="sxs-lookup"><span data-stu-id="51acc-135">Type</span></span>   | <span data-ttu-id="51acc-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="51acc-136">Required</span></span> | <span data-ttu-id="51acc-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="51acc-137">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="51acc-138">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="51acc-138">customer-id</span></span> | <span data-ttu-id="51acc-139">sztring</span><span class="sxs-lookup"><span data-stu-id="51acc-139">string</span></span> | <span data-ttu-id="51acc-140">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-140">Yes</span></span>      | <span data-ttu-id="51acc-141">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="51acc-141">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="51acc-142">házirend-azonosító</span><span class="sxs-lookup"><span data-stu-id="51acc-142">policy-id</span></span>   | <span data-ttu-id="51acc-143">sztring</span><span class="sxs-lookup"><span data-stu-id="51acc-143">string</span></span> | <span data-ttu-id="51acc-144">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-144">Yes</span></span>      | <span data-ttu-id="51acc-145">Egy GUID-formázott karakterlánc, amely a frissítendő szabályzatot azonosítja.</span><span class="sxs-lookup"><span data-stu-id="51acc-145">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="51acc-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="51acc-146">Request headers</span></span>

<span data-ttu-id="51acc-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="51acc-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="51acc-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="51acc-148">Request body</span></span>

<span data-ttu-id="51acc-149">A kérés törzsének tartalmaznia kell egy objektumot, amely megadja a szabályzat adatait.</span><span class="sxs-lookup"><span data-stu-id="51acc-149">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="51acc-150">Név</span><span class="sxs-lookup"><span data-stu-id="51acc-150">Name</span></span>            | <span data-ttu-id="51acc-151">Típus</span><span class="sxs-lookup"><span data-stu-id="51acc-151">Type</span></span>             | <span data-ttu-id="51acc-152">Kötelező</span><span class="sxs-lookup"><span data-stu-id="51acc-152">Required</span></span> | <span data-ttu-id="51acc-153">Frissíthető</span><span class="sxs-lookup"><span data-stu-id="51acc-153">Updatable</span></span> | <span data-ttu-id="51acc-154">Leírás</span><span class="sxs-lookup"><span data-stu-id="51acc-154">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="51acc-155">id</span><span class="sxs-lookup"><span data-stu-id="51acc-155">id</span></span>              | <span data-ttu-id="51acc-156">sztring</span><span class="sxs-lookup"><span data-stu-id="51acc-156">string</span></span>           | <span data-ttu-id="51acc-157">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-157">Yes</span></span>      | <span data-ttu-id="51acc-158">Nem</span><span class="sxs-lookup"><span data-stu-id="51acc-158">No</span></span>        | <span data-ttu-id="51acc-159">A házirendet azonosító GUID formátumú karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="51acc-159">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="51acc-160">name</span><span class="sxs-lookup"><span data-stu-id="51acc-160">name</span></span>            | <span data-ttu-id="51acc-161">sztring</span><span class="sxs-lookup"><span data-stu-id="51acc-161">string</span></span>           | <span data-ttu-id="51acc-162">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-162">Yes</span></span>      | <span data-ttu-id="51acc-163">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-163">Yes</span></span>       | <span data-ttu-id="51acc-164">A szabályzat rövid neve.</span><span class="sxs-lookup"><span data-stu-id="51acc-164">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="51acc-165">category</span><span class="sxs-lookup"><span data-stu-id="51acc-165">category</span></span>        | <span data-ttu-id="51acc-166">sztring</span><span class="sxs-lookup"><span data-stu-id="51acc-166">string</span></span>           | <span data-ttu-id="51acc-167">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-167">Yes</span></span>      | <span data-ttu-id="51acc-168">Nem</span><span class="sxs-lookup"><span data-stu-id="51acc-168">No</span></span>        | <span data-ttu-id="51acc-169">A szabályzat kategóriája.</span><span class="sxs-lookup"><span data-stu-id="51acc-169">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="51acc-170">leírás</span><span class="sxs-lookup"><span data-stu-id="51acc-170">description</span></span>     | <span data-ttu-id="51acc-171">sztring</span><span class="sxs-lookup"><span data-stu-id="51acc-171">string</span></span>           | <span data-ttu-id="51acc-172">Nem</span><span class="sxs-lookup"><span data-stu-id="51acc-172">No</span></span>       | <span data-ttu-id="51acc-173">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-173">Yes</span></span>       | <span data-ttu-id="51acc-174">A szabályzat leírása.</span><span class="sxs-lookup"><span data-stu-id="51acc-174">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="51acc-175">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="51acc-175">devicesAssigned</span></span> | <span data-ttu-id="51acc-176">szám</span><span class="sxs-lookup"><span data-stu-id="51acc-176">number</span></span>           | <span data-ttu-id="51acc-177">Nem</span><span class="sxs-lookup"><span data-stu-id="51acc-177">No</span></span>       | <span data-ttu-id="51acc-178">Nem</span><span class="sxs-lookup"><span data-stu-id="51acc-178">No</span></span>        | <span data-ttu-id="51acc-179">Az eszközök száma.</span><span class="sxs-lookup"><span data-stu-id="51acc-179">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="51acc-180">policySettings</span><span class="sxs-lookup"><span data-stu-id="51acc-180">policySettings</span></span>  | <span data-ttu-id="51acc-181">sztringek tömbje</span><span class="sxs-lookup"><span data-stu-id="51acc-181">array of strings</span></span> | <span data-ttu-id="51acc-182">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-182">Yes</span></span>      | <span data-ttu-id="51acc-183">Igen</span><span class="sxs-lookup"><span data-stu-id="51acc-183">Yes</span></span>       | <span data-ttu-id="51acc-184">A házirend-beállítások: "None", " \_ OEM- \_ előtelepítések eltávolítása", "Oobe \_ felhasználó \_ nem \_ helyi \_ rendszergazda", "expressz beállítások kihagyása \_ \_ ", "az \_ OEM- \_ regisztráció \_ kihagyása", "kihagyott EULA".</span><span class="sxs-lookup"><span data-stu-id="51acc-184">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="51acc-185">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="51acc-185">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="51acc-186">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="51acc-186">REST response</span></span>

<span data-ttu-id="51acc-187">Ha a művelet sikeres, a válasz törzse tartalmazza az új szabályzathoz tartozó [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="51acc-187">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="51acc-188">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="51acc-188">Response success and error codes</span></span>

<span data-ttu-id="51acc-189">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="51acc-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="51acc-190">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="51acc-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="51acc-191">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="51acc-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="51acc-192">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="51acc-192">Response example</span></span>

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
