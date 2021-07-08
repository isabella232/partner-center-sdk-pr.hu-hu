---
title: A rendelkezésre álló licencek listájának lekérése licenccsoport alapján
description: A megadott ügyfél felhasználói számára elérhető licenccsoportok licenclistának lekért listája.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: de59dfccf723c8f2411d9dadc51beb88688d5b02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874516"
---
# <a name="get-a-list-of-available-licenses-by-license-group"></a><span data-ttu-id="46276-103">A rendelkezésre álló licencek listájának lekérése licenccsoport alapján</span><span class="sxs-lookup"><span data-stu-id="46276-103">Get a list of available licenses by license group</span></span>

<span data-ttu-id="46276-104">A megadott ügyfél felhasználói számára elérhető licenccsoportok licenclistának lekért listája.</span><span class="sxs-lookup"><span data-stu-id="46276-104">How to get a list of licenses for the specified license groups available to users of the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46276-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="46276-105">Prerequisites</span></span>

- <span data-ttu-id="46276-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="46276-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="46276-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="46276-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="46276-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="46276-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="46276-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="46276-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="46276-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="46276-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="46276-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="46276-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="46276-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="46276-112">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="46276-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="46276-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="46276-114">Egy vagy több licenccsoport-azonosítót felsoroló lista.</span><span class="sxs-lookup"><span data-stu-id="46276-114">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="46276-115">C\#</span><span class="sxs-lookup"><span data-stu-id="46276-115">C\#</span></span>

<span data-ttu-id="46276-116">A megadott licenccsoportokhoz elérhető licencek listájának lekért listájának lekért első része egy [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)típusú lista példányosítása, majd [a](/dotnet/api/system.collections.generic.list-1) licenccsoportok hozzáadása a listához.</span><span class="sxs-lookup"><span data-stu-id="46276-116">To get a list of available licenses for the specified license groups, start by instantiating a [List](/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="46276-117">Ezután használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="46276-117">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="46276-118">Ezután lekéri a [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) tulajdonság értékét az ügyfél által előfizetett termékváltozat-gyűjtési műveletek felületének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="46276-118">Then, get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span> <span data-ttu-id="46276-119">Végül továbbküldi a licenccsoportok listáját a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) metódusnak az előfizetett termékcsoportok listájának lekérése érdekében az elérhető licencegységek részleteivel.</span><span class="sxs-lookup"><span data-stu-id="46276-119">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of subscribed SKUs with details on available license units.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get subscribed SKUs available for group1, the license group for Azure Active Directory (AAD).
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1};
var customerUserAadSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get subscribed SKUs available for group2, the license group for Minecraft product licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group2};
var customerUserSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);

// To get both AAD and Minecraft subscribed SKUs.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>() { LicenseGroupId.Group1, LicenseGroupId.Group2};
var customerUserBothAadAndSfbSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="46276-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="46276-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="46276-121">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="46276-121">Request syntax</span></span>

| <span data-ttu-id="46276-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="46276-122">Method</span></span>  | <span data-ttu-id="46276-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="46276-123">Request URI</span></span>                                                                                                                                  |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="46276-124">**Kap**</span><span class="sxs-lookup"><span data-stu-id="46276-124">**GET**</span></span> | <span data-ttu-id="46276-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="46276-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="46276-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="46276-126">**GET**</span></span> | <span data-ttu-id="46276-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="46276-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="46276-128">**Kap**</span><span class="sxs-lookup"><span data-stu-id="46276-128">**GET**</span></span> | <span data-ttu-id="46276-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="46276-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="46276-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="46276-130">URI parameter</span></span>

<span data-ttu-id="46276-131">Az ügyfél és a licenccsoportok azonosításához használja az alábbi elérési utat és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="46276-131">Use the following path and query parameters to identify the customer and the license groups.</span></span>

| <span data-ttu-id="46276-132">Név</span><span class="sxs-lookup"><span data-stu-id="46276-132">Name</span></span>            | <span data-ttu-id="46276-133">Típus</span><span class="sxs-lookup"><span data-stu-id="46276-133">Type</span></span>   | <span data-ttu-id="46276-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="46276-134">Required</span></span> | <span data-ttu-id="46276-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="46276-135">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="46276-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="46276-136">customer-id</span></span>     | <span data-ttu-id="46276-137">sztring</span><span class="sxs-lookup"><span data-stu-id="46276-137">string</span></span> | <span data-ttu-id="46276-138">Igen</span><span class="sxs-lookup"><span data-stu-id="46276-138">Yes</span></span>      | <span data-ttu-id="46276-139">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="46276-139">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="46276-140">licenseGroupIds (licenccsoport-azonosítók)</span><span class="sxs-lookup"><span data-stu-id="46276-140">licenseGroupIds</span></span> | <span data-ttu-id="46276-141">sztring</span><span class="sxs-lookup"><span data-stu-id="46276-141">string</span></span> | <span data-ttu-id="46276-142">No</span><span class="sxs-lookup"><span data-stu-id="46276-142">No</span></span>       | <span data-ttu-id="46276-143">A hozzárendelt licencek licenccsoportját jelző felsorolásérték.</span><span class="sxs-lookup"><span data-stu-id="46276-143">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="46276-144">Érvényes értékek: Group1, Group2 Group1 – Ez a csoport az összes olyan terméket tartalmaz, amelynek licence a Azure Active Directory (AAD) kezelhető.</span><span class="sxs-lookup"><span data-stu-id="46276-144">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="46276-145">Group2 (2. csoport) – Ez a csoport csak Minecraft terméklicenceket.</span><span class="sxs-lookup"><span data-stu-id="46276-145">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="46276-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="46276-146">Request headers</span></span>

<span data-ttu-id="46276-147">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="46276-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="46276-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="46276-148">Request body</span></span>

<span data-ttu-id="46276-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="46276-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="46276-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="46276-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="46276-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="46276-151">REST response</span></span>

<span data-ttu-id="46276-152">Ha a művelet sikeres, a válasz törzse a [SubscribedSku](license-resources.md#subscribedsku) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="46276-152">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="46276-153">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="46276-153">Response success and error codes</span></span>

<span data-ttu-id="46276-154">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="46276-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="46276-155">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="46276-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="46276-156">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="46276-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="46276-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="46276-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: S6Pd5XQAx0Ss/zQi.0
MS-ServerId: 030011719
Date: Sat, 10 Jun 2017 00:19:44 GMT

{
    "totalCount": 04,
    "items": [{
            "availableUnits": 15,
            "activeUnits": 15,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 15,
            "warningUnits": 0,
            "productSku": {
                "id": "078d2b04-f1bd-4111-bbd4-b4b1b354cef4",
                "name": "Azure Active Directory Premium P1",
                "skuPartNumber": "AAD_PREMIUM",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 1,
            "activeUnits": 1,
            "consumedUnits": 0,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "54b84594-9c77-4499-8d65-5e0d5f410e78",
                "name": "Dynamics AX Task",
                "skuPartNumber": "AX_TASK_USER",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 23,
            "activeUnits": 72,
            "consumedUnits": 49,
            "suspendedUnits": 0,
            "totalUnits": 72,
            "warningUnits": 0,
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "targetType": "User",
                "licenseGroupId": "group2"
            },
            "servicePlans": [

            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }, {
            "availableUnits": 71,
            "activeUnits": 112,
            "consumedUnits": 41,
            "suspendedUnits": 0,
            "totalUnits": 112,
            "warningUnits": 0,
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-skus-found"></a><span data-ttu-id="46276-158">Válasz példa (nem található egyező SKUs)</span><span class="sxs-lookup"><span data-stu-id="46276-158">Response example (no matching SKUs found)</span></span>

<span data-ttu-id="46276-159">Ha a megadott licenccsoportokhoz nem találhatók megfelelő előfizetett termékcsoportok, a válasz egy üres gyűjteményt tartalmaz egy totalCount elemmel, amelynek értéke 0.</span><span class="sxs-lookup"><span data-stu-id="46276-159">If no matching subscribed SKUs can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 71
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CV: q05xrhUeDUKvhrFt.0
MS-ServerId: 030020525
Date: Fri, 09 Jun 2017 22:50:11 GMT

{
    "totalCount": 0,
    "items": [],
    "attributes": {
        "objectType": "Collection"
    }
}
```
