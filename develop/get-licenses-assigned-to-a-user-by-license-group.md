---
title: Adott felhasználóhoz rendelt licencek lekérése licenccsoport szerint
description: A felhasználóhoz rendelt licencek listájának lekért listája a megadott licenccsoportokhoz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 54acf6f315e3062d03903a98d0c6c1946065f95e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446003"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="d2d0d-103">Adott felhasználóhoz rendelt licencek lekérése licenccsoport szerint</span><span class="sxs-lookup"><span data-stu-id="d2d0d-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="d2d0d-104">A felhasználóhoz rendelt licencek listájának lekért listája a megadott licenccsoportokhoz.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-104">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2d0d-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d2d0d-105">Prerequisites</span></span>

- <span data-ttu-id="d2d0d-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d2d0d-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d2d0d-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d2d0d-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d2d0d-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d2d0d-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d2d0d-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d2d0d-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d2d0d-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d2d0d-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d2d0d-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d2d0d-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d2d0d-114">Egy felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-114">A user identifier.</span></span>

- <span data-ttu-id="d2d0d-115">Egy vagy több licenccsoport-azonosítót felsoroló lista.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-115">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="d2d0d-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d2d0d-116">C\#</span></span>

<span data-ttu-id="d2d0d-117">Annak ellenőrzéséhez, hogy mely licencek vannak hozzárendelve egy felhasználóhoz a megadott licenccsoportokból, először példányosodja a [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)típusú [List/dotnet/api/system.collections.generic.list-1) típust, majd adja hozzá a licenccsoportokat a listához.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-117">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="d2d0d-118">Ezután használja az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-118">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="d2d0d-119">Ezután hívja meg a [**Users.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) a felhasználói azonosítóval a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-119">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="d2d0d-120">Ezután szerezze be az ügyfélfelhasználói licencműveletekkel kapcsolatos felületet a [**Licencek tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses)</span><span class="sxs-lookup"><span data-stu-id="d2d0d-120">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="d2d0d-121">Végül továbbküldi a licenccsoportok listáját a [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) metódusnak a felhasználóhoz rendelt licencek gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-121">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

// To get the group1 (Azure Active Directory (AAD)) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1 };
var customerUserAadAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get the group2 (Minecraft) assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group2 };
var customerUserSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);

// To get both AAD and Minecraft assigned licenses.
List<LicenseGroupId> licenseGroupIds = new List<LicenseGroupId>(){ LicenseGroupId.Group1, LicenseGroupId.Group2 };
var customerUserBothAadAndSfbAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get(licenseGroupIds);
```

## <a name="rest-request"></a><span data-ttu-id="d2d0d-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d2d0d-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d2d0d-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d2d0d-123">Request syntax</span></span>

| <span data-ttu-id="d2d0d-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="d2d0d-124">Method</span></span>  | <span data-ttu-id="d2d0d-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d2d0d-125">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2d0d-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-126">**GET**</span></span> | <span data-ttu-id="d2d0d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users/{felhasználói azonosító}/licenses?licenseGroupIds=Group1 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d2d0d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="d2d0d-128">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-128">**GET**</span></span> | <span data-ttu-id="d2d0d-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users/{felhasználói azonosító}/licenses?licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d2d0d-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="d2d0d-130">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d2d0d-130">**GET**</span></span> | <span data-ttu-id="d2d0d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users/{felhasználói azonosító}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d2d0d-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d2d0d-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d2d0d-132">URI parameter</span></span>

<span data-ttu-id="d2d0d-133">Az alábbi elérési út és lekérdezési paraméterek segítségével azonosíthatja az ügyfél-, felhasználó- és licenccsoportokat.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-133">Use the following path and query parameters to identify the customer, user, and license groups.</span></span>

| <span data-ttu-id="d2d0d-134">Név</span><span class="sxs-lookup"><span data-stu-id="d2d0d-134">Name</span></span>            | <span data-ttu-id="d2d0d-135">Típus</span><span class="sxs-lookup"><span data-stu-id="d2d0d-135">Type</span></span>   | <span data-ttu-id="d2d0d-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d2d0d-136">Required</span></span> | <span data-ttu-id="d2d0d-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="d2d0d-137">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2d0d-138">ügyfélazonosító</span><span class="sxs-lookup"><span data-stu-id="d2d0d-138">customer-id</span></span>     | <span data-ttu-id="d2d0d-139">sztring</span><span class="sxs-lookup"><span data-stu-id="d2d0d-139">string</span></span> | <span data-ttu-id="d2d0d-140">Igen</span><span class="sxs-lookup"><span data-stu-id="d2d0d-140">Yes</span></span>      | <span data-ttu-id="d2d0d-141">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-141">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="d2d0d-142">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="d2d0d-142">user-id</span></span>         | <span data-ttu-id="d2d0d-143">sztring</span><span class="sxs-lookup"><span data-stu-id="d2d0d-143">string</span></span> | <span data-ttu-id="d2d0d-144">Igen</span><span class="sxs-lookup"><span data-stu-id="d2d0d-144">Yes</span></span>      | <span data-ttu-id="d2d0d-145">A felhasználót azonosító GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-145">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="d2d0d-146">licenseGroupIds (licenccsoport-azonosítók)</span><span class="sxs-lookup"><span data-stu-id="d2d0d-146">licenseGroupIds</span></span> | <span data-ttu-id="d2d0d-147">sztring</span><span class="sxs-lookup"><span data-stu-id="d2d0d-147">string</span></span> | <span data-ttu-id="d2d0d-148">No</span><span class="sxs-lookup"><span data-stu-id="d2d0d-148">No</span></span>       | <span data-ttu-id="d2d0d-149">A hozzárendelt licencek licenccsoportját jelző felsorolásérték.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-149">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="d2d0d-150">Érvényes értékek: Group1, Group2 Group1 – Ez a csoport az összes olyan terméket tartalmaz, amelynek licence a Azure Active Directory (AAD) alatt kezelhető.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-150">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="d2d0d-151">2. csoport – Ez a csoport csak Minecraft terméklicenceket.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-151">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d2d0d-152">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d2d0d-152">Request headers</span></span>

<span data-ttu-id="d2d0d-153">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d2d0d-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d2d0d-154">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d2d0d-154">Request body</span></span>

<span data-ttu-id="d2d0d-155">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-155">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d2d0d-156">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d2d0d-156">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d2d0d-157">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d2d0d-157">REST response</span></span>

<span data-ttu-id="d2d0d-158">Ha a művelet sikeres, a válasz törzse tartalmazza a [licencerőforrások](license-resources.md#license) gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-158">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d2d0d-159">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d2d0d-159">Response success and error codes</span></span>

<span data-ttu-id="d2d0d-160">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d2d0d-161">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d2d0d-162">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d2d0d-162">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d2d0d-163">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d2d0d-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
    "totalCount": 2,
    "items": [{
            "servicePlans": [

            ],
            "productSku": {
                "id": "984df360-9a74-4647-8cf8-696749f6247a",
                "name": "Minecraft Education Edition Faculty",
                "skuPartNumber": "CFQ7TTC0K5DR/0002",
                "licenseGroupId": "group2"
            },
            "attributes": {
                "objectType": "License"
            }
        }, {
            "servicePlans": [{
                    "displayName": "Windows Defender Advanced Threat Protection",
                    "serviceName": "WINDEFATP",
                    "id": "871d91ec-ec1a-452b-a83f-bd76c7d770ef",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Windows 10 Enterprise E3",
                    "serviceName": "WIN10_PRO_ENT_SUB",
                    "id": "21b439ba-a0ca-424f-a6cc-52f954a5b111",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "1e7e1070-8ccb-4aca-b470-d7cb538cb07e",
                "name": "Windows 10 Enterprise E5",
                "skuPartNumber": "WIN_ENT_E5",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="d2d0d-164">Válasz példa (nem található egyező licenc)</span><span class="sxs-lookup"><span data-stu-id="d2d0d-164">Response example (no matching licenses found)</span></span>

<span data-ttu-id="d2d0d-165">Ha a megadott licenccsoportokhoz nem találhatók megfelelő licencek, a válasz egy üres gyűjteményt tartalmaz, amelynek totalCount eleme 0.</span><span class="sxs-lookup"><span data-stu-id="d2d0d-165">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
