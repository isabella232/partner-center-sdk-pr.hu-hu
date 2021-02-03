---
title: Adott felhasználóhoz rendelt licencek lekérése licenccsoport szerint
description: A megadott licencfeltételek felhasználó által hozzárendelt licencek listájának beolvasása.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 28c10e3e2acb30e4110213344959a87d4ddfcffb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768320"
---
# <a name="get-licenses-assigned-to-a-user-by-license-group"></a><span data-ttu-id="d62a0-103">Adott felhasználóhoz rendelt licencek lekérése licenccsoport szerint</span><span class="sxs-lookup"><span data-stu-id="d62a0-103">Get licenses assigned to a user by license group</span></span>

<span data-ttu-id="d62a0-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="d62a0-104">**Applies To**</span></span>

- <span data-ttu-id="d62a0-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d62a0-105">Partner Center</span></span>

<span data-ttu-id="d62a0-106">A megadott licencfeltételek felhasználó által hozzárendelt licencek listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="d62a0-106">How to get a list of user assigned licenses for the specified license groups.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d62a0-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d62a0-107">Prerequisites</span></span>

- <span data-ttu-id="d62a0-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="d62a0-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d62a0-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="d62a0-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d62a0-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d62a0-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d62a0-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d62a0-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d62a0-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="d62a0-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d62a0-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="d62a0-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d62a0-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="d62a0-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d62a0-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d62a0-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d62a0-116">Egy felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="d62a0-116">A user identifier.</span></span>

- <span data-ttu-id="d62a0-117">Egy vagy több engedélyszám-azonosító listája.</span><span class="sxs-lookup"><span data-stu-id="d62a0-117">A list of one or more license group identifiers.</span></span>

## <a name="c"></a><span data-ttu-id="d62a0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="d62a0-118">C\#</span></span>

<span data-ttu-id="d62a0-119">Annak ellenőrzéséhez, hogy mely licencek vannak hozzárendelve egy felhasználóhoz a megadott licencfeltételek alapján, kezdje a következőt: [List/DotNet/API/System. Collections. Generic. list -1), amely [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid)típusú, majd adja hozzá a licenc-csoportokat a listához.</span><span class="sxs-lookup"><span data-stu-id="d62a0-119">To check which licenses are assigned to a user from specified license groups, start by instantiating a [List/dotnet/api/system.collections.generic.list-1) of type [**LicenseGroupId**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid), and then add the license groups to the list.</span></span> <span data-ttu-id="d62a0-120">Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="d62a0-120">Then, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="d62a0-121">Ezután hívja meg a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a felhasználói azonosítóval a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="d62a0-121">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="d62a0-122">Ezután szerezzen be egy felületet az ügyfél felhasználói licencelési műveleteihez a [**licencek**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="d62a0-122">Then, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="d62a0-123">Végül adja át a licenc-csoportok listáját a [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) metódusnak a felhasználóhoz rendelt licencek gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d62a0-123">Finally, pass the list of license groups to the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="d62a0-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="d62a0-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d62a0-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d62a0-125">Request syntax</span></span>

| <span data-ttu-id="d62a0-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="d62a0-126">Method</span></span>  | <span data-ttu-id="d62a0-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d62a0-127">Request URI</span></span>                                                                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d62a0-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="d62a0-128">**GET**</span></span> | <span data-ttu-id="d62a0-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Group1 http/1.1</span><span class="sxs-lookup"><span data-stu-id="d62a0-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1 HTTP/1.1</span></span>                        |
| <span data-ttu-id="d62a0-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="d62a0-130">**GET**</span></span> | <span data-ttu-id="d62a0-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Group2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="d62a0-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group2 HTTP/1.1</span></span>                        |
| <span data-ttu-id="d62a0-132">**GET**</span><span class="sxs-lookup"><span data-stu-id="d62a0-132">**GET**</span></span> | <span data-ttu-id="d62a0-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses? LicenseGroupIds = Group1&LicenseGroupIds = Group2 http/1.1</span><span class="sxs-lookup"><span data-stu-id="d62a0-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d62a0-134">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d62a0-134">URI parameter</span></span>

<span data-ttu-id="d62a0-135">Használja az alábbi elérési utat és a lekérdezési paramétereket az ügyfél, a felhasználó és a licencek csoportjának azonosításához.</span><span class="sxs-lookup"><span data-stu-id="d62a0-135">Use the following path and query parameters to identify the customer, user and license groups.</span></span>

| <span data-ttu-id="d62a0-136">Név</span><span class="sxs-lookup"><span data-stu-id="d62a0-136">Name</span></span>            | <span data-ttu-id="d62a0-137">Típus</span><span class="sxs-lookup"><span data-stu-id="d62a0-137">Type</span></span>   | <span data-ttu-id="d62a0-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d62a0-138">Required</span></span> | <span data-ttu-id="d62a0-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="d62a0-139">Description</span></span>                                                                                                                                                                                                                                                           |
|-----------------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d62a0-140">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="d62a0-140">customer-id</span></span>     | <span data-ttu-id="d62a0-141">sztring</span><span class="sxs-lookup"><span data-stu-id="d62a0-141">string</span></span> | <span data-ttu-id="d62a0-142">Igen</span><span class="sxs-lookup"><span data-stu-id="d62a0-142">Yes</span></span>      | <span data-ttu-id="d62a0-143">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d62a0-143">A GUID formatted string that identifies the customer.</span></span>                                                                                                                                                                                                                 |
| <span data-ttu-id="d62a0-144">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="d62a0-144">user-id</span></span>         | <span data-ttu-id="d62a0-145">sztring</span><span class="sxs-lookup"><span data-stu-id="d62a0-145">string</span></span> | <span data-ttu-id="d62a0-146">Igen</span><span class="sxs-lookup"><span data-stu-id="d62a0-146">Yes</span></span>      | <span data-ttu-id="d62a0-147">Egy GUID formátumú karakterlánc, amely azonosítja a felhasználót.</span><span class="sxs-lookup"><span data-stu-id="d62a0-147">A GUID formatted string that identifies the user.</span></span>                                                                                                                                                                                                                     |
| <span data-ttu-id="d62a0-148">licenseGroupIds</span><span class="sxs-lookup"><span data-stu-id="d62a0-148">licenseGroupIds</span></span> | <span data-ttu-id="d62a0-149">sztring</span><span class="sxs-lookup"><span data-stu-id="d62a0-149">string</span></span> | <span data-ttu-id="d62a0-150">No</span><span class="sxs-lookup"><span data-stu-id="d62a0-150">No</span></span>       | <span data-ttu-id="d62a0-151">Egy enumerálási érték, amely a hozzárendelt licencek licencszerződését jelzi.</span><span class="sxs-lookup"><span data-stu-id="d62a0-151">An enum value that indicates the license group of the assigned licenses.</span></span> <span data-ttu-id="d62a0-152">Érvényes értékek: Group1, Group2 Group1 – ez a csoport minden olyan terméket tartalmaz, amelynek a licence felügyelhető a Azure Active Directoryban (HRE).</span><span class="sxs-lookup"><span data-stu-id="d62a0-152">Valid values: Group1, Group2 Group1 - This group has all products whose license can be managed in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="d62a0-153">Group2 – ez a csoport csak a Minecraft termék licenceit tartalmazta.</span><span class="sxs-lookup"><span data-stu-id="d62a0-153">Group2 - This group has only Minecraft product licenses.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d62a0-154">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d62a0-154">Request headers</span></span>

<span data-ttu-id="d62a0-155">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d62a0-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d62a0-156">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d62a0-156">Request body</span></span>

<span data-ttu-id="d62a0-157">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d62a0-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d62a0-158">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d62a0-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses?licenseGroupIds=Group1&licenseGroupIds=Group2 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a1d077e4-28b1-4578-b873-6d1a82fa1644
MS-CorrelationId: c8cb5a60-ae08-4afc-92f0-efc42adfa186
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d62a0-159">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d62a0-159">REST response</span></span>

<span data-ttu-id="d62a0-160">Ha ez sikeres, a válasz törzse tartalmazza a [licenc](license-resources.md#license) -erőforrások gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="d62a0-160">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d62a0-161">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d62a0-161">Response success and error codes</span></span>

<span data-ttu-id="d62a0-162">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="d62a0-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d62a0-163">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="d62a0-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d62a0-164">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d62a0-164">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d62a0-165">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d62a0-165">Response example</span></span>

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

### <a name="response-example-no-matching-licenses-found"></a><span data-ttu-id="d62a0-166">Példa válaszra (nem találhatók egyező licencek)</span><span class="sxs-lookup"><span data-stu-id="d62a0-166">Response example (no matching licenses found)</span></span>

<span data-ttu-id="d62a0-167">Ha a megadott licencfeltételeket nem találhatók egyező licencek, a válasz egy üres gyűjteményt tartalmaz egy olyan totalCount elemmel, amelynek értéke 0.</span><span class="sxs-lookup"><span data-stu-id="d62a0-167">If no matching licenses can be found for the specified license groups, the response contains an empty collection with a totalCount element whose value is 0.</span></span>

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
