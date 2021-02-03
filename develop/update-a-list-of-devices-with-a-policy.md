---
title: Eszközök listájának frissítése szabályzattal
description: Az eszközök listájának frissítése a megadott ügyfél konfigurációs házirendjével.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04c2ef33116335db40bd2934dc7e33d57f015097
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768376"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="69ad5-103">Eszközök listájának frissítése szabályzattal</span><span class="sxs-lookup"><span data-stu-id="69ad5-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="69ad5-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="69ad5-104">**Applies To**</span></span>

- <span data-ttu-id="69ad5-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="69ad5-105">Partner Center</span></span>
- <span data-ttu-id="69ad5-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="69ad5-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="69ad5-107">Az eszközök listájának frissítése a megadott ügyfél konfigurációs házirendjével.</span><span class="sxs-lookup"><span data-stu-id="69ad5-107">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69ad5-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="69ad5-108">Prerequisites</span></span>

- <span data-ttu-id="69ad5-109">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="69ad5-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="69ad5-110">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="69ad5-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="69ad5-111">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="69ad5-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="69ad5-112">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="69ad5-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="69ad5-113">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="69ad5-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="69ad5-114">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="69ad5-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="69ad5-115">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="69ad5-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="69ad5-116">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="69ad5-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="69ad5-117">A házirend-azonosító.</span><span class="sxs-lookup"><span data-stu-id="69ad5-117">The policy identifier.</span></span>

- <span data-ttu-id="69ad5-118">A frissítendő eszközök azonosítói.</span><span class="sxs-lookup"><span data-stu-id="69ad5-118">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="69ad5-119">C\#</span><span class="sxs-lookup"><span data-stu-id="69ad5-119">C\#</span></span>

<span data-ttu-id="69ad5-120">A megadott konfigurációs házirenddel rendelkező eszközök listájának frissítéséhez először a [KeyValuePair/DotNet/API/System. Collections. Generic. KeyValuePair [**-2) típusú**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)[List/DotNet/API/System. Collections. Generic. list -1 "példányt hozza létre, és adja hozzá az alkalmazandó szabályzatot az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="69ad5-120">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="69ad5-121">Szüksége lesz a házirend házirend-azonosítójára.</span><span class="sxs-lookup"><span data-stu-id="69ad5-121">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="69ad5-122">Ezután hozza létre a szabályzattal frissítendő [**eszközbeállítások**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) listáját, megadhatja az eszköz azonosítóját és az alkalmazandó házirendet tartalmazó listát.</span><span class="sxs-lookup"><span data-stu-id="69ad5-122">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="69ad5-123">Ezután hozzon létre egy [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) objektumot, és állítsa be az [**eszközök**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) tulajdonságot az eszköz objektumainak listájára.</span><span class="sxs-lookup"><span data-stu-id="69ad5-123">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="69ad5-124">Az eszköz házirend-frissítési kérelmének feldolgozásához hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval, és kérje le a felületet a megadott ügyfél műveleteire.</span><span class="sxs-lookup"><span data-stu-id="69ad5-124">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="69ad5-125">Ezután kérje le a [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) tulajdonságot az ügyfél-eszköz gyűjtési műveleteihez szükséges illesztőfelület beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="69ad5-125">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="69ad5-126">Végül hívja meg a [**frissítési**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) metódust a DevicePolicyUpdateRequest objektummal, hogy frissítse az eszközöket a szabályzattal.</span><span class="sxs-lookup"><span data-stu-id="69ad5-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

<span data-ttu-id="69ad5-127">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="69ad5-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="69ad5-128">**Projekt**: partner Center SDK Samples **osztály**: UpdateDevicesPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="69ad5-128">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="69ad5-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="69ad5-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="69ad5-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="69ad5-130">Request syntax</span></span>

| <span data-ttu-id="69ad5-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="69ad5-131">Method</span></span>    | <span data-ttu-id="69ad5-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="69ad5-132">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="69ad5-133">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="69ad5-133">**PATCH**</span></span> | <span data-ttu-id="69ad5-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/DevicePolicyUpdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="69ad5-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="69ad5-135">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="69ad5-135">URI parameter</span></span>

<span data-ttu-id="69ad5-136">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="69ad5-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="69ad5-137">Név</span><span class="sxs-lookup"><span data-stu-id="69ad5-137">Name</span></span>        | <span data-ttu-id="69ad5-138">Típus</span><span class="sxs-lookup"><span data-stu-id="69ad5-138">Type</span></span>   | <span data-ttu-id="69ad5-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="69ad5-139">Required</span></span> | <span data-ttu-id="69ad5-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="69ad5-140">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="69ad5-141">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="69ad5-141">customer-id</span></span> | <span data-ttu-id="69ad5-142">sztring</span><span class="sxs-lookup"><span data-stu-id="69ad5-142">string</span></span> | <span data-ttu-id="69ad5-143">Igen</span><span class="sxs-lookup"><span data-stu-id="69ad5-143">Yes</span></span>      | <span data-ttu-id="69ad5-144">Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="69ad5-144">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="69ad5-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="69ad5-145">Request headers</span></span>

<span data-ttu-id="69ad5-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="69ad5-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="69ad5-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="69ad5-147">Request body</span></span>

<span data-ttu-id="69ad5-148">A kérelem törzsének tartalmaznia kell egy [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="69ad5-148">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="69ad5-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="69ad5-149">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="69ad5-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="69ad5-150">REST response</span></span>

<span data-ttu-id="69ad5-151">Ha a művelet sikeres, a válasz egy olyan **Location** fejlécet tartalmaz, amely rendelkezik egy URI-val, amely a Batch-folyamat állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="69ad5-151">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="69ad5-152">Mentse ezt az URI-t más kapcsolódó REST API-kkal való használatra.</span><span class="sxs-lookup"><span data-stu-id="69ad5-152">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="69ad5-153">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="69ad5-153">Response success and error codes</span></span>

<span data-ttu-id="69ad5-154">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="69ad5-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="69ad5-155">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="69ad5-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="69ad5-156">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="69ad5-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="69ad5-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="69ad5-157">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
