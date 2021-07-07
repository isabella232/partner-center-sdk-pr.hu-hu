---
title: Eszközök listájának frissítése szabályzattal
description: Eszközlista frissítése a megadott ügyfél konfigurációs szabályzatával.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b35873eb253b0929bfc01662b0beb9b31d0c6b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530072"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="d9d94-103">Eszközök listájának frissítése szabályzattal</span><span class="sxs-lookup"><span data-stu-id="d9d94-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="d9d94-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Németországhoz</span><span class="sxs-lookup"><span data-stu-id="d9d94-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="d9d94-105">Eszközlista frissítése a megadott ügyfél konfigurációs szabályzatával.</span><span class="sxs-lookup"><span data-stu-id="d9d94-105">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9d94-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d9d94-106">Prerequisites</span></span>

- <span data-ttu-id="d9d94-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d9d94-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d9d94-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="d9d94-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d9d94-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d9d94-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d9d94-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d9d94-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d9d94-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d9d94-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d9d94-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d9d94-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d9d94-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d9d94-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d9d94-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d9d94-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d9d94-115">A szabályzat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="d9d94-115">The policy identifier.</span></span>

- <span data-ttu-id="d9d94-116">A frissítenie kell az eszközök eszközazonosítóit.</span><span class="sxs-lookup"><span data-stu-id="d9d94-116">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="d9d94-117">C\#</span><span class="sxs-lookup"><span data-stu-id="d9d94-117">C\#</span></span>

<span data-ttu-id="d9d94-118">A megadott konfigurációs házirendet használó eszközök listájának frissítéséhez először példányosítson egy [List/dotnet/api/system.collections.generic.list-1) típusú [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) típusú szabályzatot, az alábbi példakódban látható módon.</span><span class="sxs-lookup"><span data-stu-id="d9d94-118">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="d9d94-119">Szüksége lesz a szabályzat szabályzatazonosítóra.</span><span class="sxs-lookup"><span data-stu-id="d9d94-119">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="d9d94-120">Ezután hozzon létre [](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) egy listát a szabályzatban frissíthető eszközobjektumokról, és adja meg az egyes eszközökre vonatkozó eszközazonosítót és az alkalmazandó szabályzatot tartalmazó listát.</span><span class="sxs-lookup"><span data-stu-id="d9d94-120">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="d9d94-121">Ezután példányositsa a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) objektumot, és állítsa az [**Eszközök**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) tulajdonságot az eszközobjektumok listájára.</span><span class="sxs-lookup"><span data-stu-id="d9d94-121">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="d9d94-122">Az eszköz szabályzatfrissítési kérésének feldolgozásához hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval a megadott ügyfél műveleteinek interfészének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d9d94-122">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="d9d94-123">Ezután olvassa be a [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) tulajdonságot az ügyfél eszközgyűjteményi műveleteinek felületének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d9d94-123">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="d9d94-124">Végül hívja meg az [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) metódust a DevicePolicyUpdateRequest objektummal az eszközök a szabályzat használatával való frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="d9d94-124">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

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

<span data-ttu-id="d9d94-125">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d9d94-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d9d94-126">**Project**: Partnerközpont SDK **osztály:** UpdateDevicesPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="d9d94-126">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d9d94-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d9d94-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d9d94-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d9d94-128">Request syntax</span></span>

| <span data-ttu-id="d9d94-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="d9d94-129">Method</span></span>    | <span data-ttu-id="d9d94-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d9d94-130">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d9d94-131">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="d9d94-131">**PATCH**</span></span> | <span data-ttu-id="d9d94-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/DevicePolicyUpdates HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d9d94-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d9d94-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d9d94-133">URI parameter</span></span>

<span data-ttu-id="d9d94-134">A kérelem létrehozásakor használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="d9d94-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="d9d94-135">Név</span><span class="sxs-lookup"><span data-stu-id="d9d94-135">Name</span></span>        | <span data-ttu-id="d9d94-136">Típus</span><span class="sxs-lookup"><span data-stu-id="d9d94-136">Type</span></span>   | <span data-ttu-id="d9d94-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d9d94-137">Required</span></span> | <span data-ttu-id="d9d94-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="d9d94-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="d9d94-139">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="d9d94-139">customer-id</span></span> | <span data-ttu-id="d9d94-140">sztring</span><span class="sxs-lookup"><span data-stu-id="d9d94-140">string</span></span> | <span data-ttu-id="d9d94-141">Igen</span><span class="sxs-lookup"><span data-stu-id="d9d94-141">Yes</span></span>      | <span data-ttu-id="d9d94-142">Egy GUID-formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d9d94-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d9d94-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d9d94-143">Request headers</span></span>

<span data-ttu-id="d9d94-144">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d9d94-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d9d94-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d9d94-145">Request body</span></span>

<span data-ttu-id="d9d94-146">A kérelem törzsének tartalmaznia kell egy [DevicePolicyUpdateRequest erőforrást.](device-deployment-resources.md#devicepolicyupdaterequest)</span><span class="sxs-lookup"><span data-stu-id="d9d94-146">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="d9d94-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d9d94-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d9d94-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d9d94-148">REST response</span></span>

<span data-ttu-id="d9d94-149">Ha a válasz sikeres, a válasz tartalmaz egy **Location** fejlécet, amely rendelkezik egy URI-azonosítóval, amely a kötegelt folyamat állapotának lekérésére használható.</span><span class="sxs-lookup"><span data-stu-id="d9d94-149">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="d9d94-150">Mentse ezt az URI-t a többi kapcsolódó REST API-val való használathoz.</span><span class="sxs-lookup"><span data-stu-id="d9d94-150">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d9d94-151">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d9d94-151">Response success and error codes</span></span>

<span data-ttu-id="d9d94-152">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d9d94-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d9d94-153">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d9d94-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d9d94-154">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d9d94-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d9d94-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d9d94-155">Response example</span></span>

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
