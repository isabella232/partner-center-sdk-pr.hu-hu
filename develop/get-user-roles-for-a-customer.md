---
title: Egy ügyfél felhasználói szerepköreinek lekérése
description: A felhasználói fiókhoz csatolt összes szerepkör/engedély listájának beolvasása. A variációk közé tartozik az ügyfél összes felhasználói fiókja összes engedélyének lekérése, valamint az adott szerepkörrel rendelkező felhasználók listájának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767812"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="9082d-104">Egy ügyfél felhasználói szerepköreinek lekérése</span><span class="sxs-lookup"><span data-stu-id="9082d-104">Get user roles for a customer</span></span>

<span data-ttu-id="9082d-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="9082d-105">**Applies To**</span></span>

- <span data-ttu-id="9082d-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="9082d-106">Partner Center</span></span>

<span data-ttu-id="9082d-107">A felhasználói fiókhoz csatolt összes szerepkör/engedély listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="9082d-107">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="9082d-108">A variációk közé tartozik az ügyfél összes felhasználói fiókja összes engedélyének lekérése, valamint az adott szerepkörrel rendelkező felhasználók listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="9082d-108">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9082d-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9082d-109">Prerequisites</span></span>

- <span data-ttu-id="9082d-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="9082d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9082d-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="9082d-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9082d-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9082d-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9082d-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9082d-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9082d-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="9082d-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9082d-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9082d-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9082d-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="9082d-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9082d-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9082d-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9082d-118">C\#</span><span class="sxs-lookup"><span data-stu-id="9082d-118">C\#</span></span>

<span data-ttu-id="9082d-119">Egy adott ügyfél összes címtár-szerepkörének lekéréséhez először kérje le a megadott ügyfél-azonosítót.</span><span class="sxs-lookup"><span data-stu-id="9082d-119">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="9082d-120">Ezután használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="9082d-120">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="9082d-121">Ezután hívja meg a **DirectoryRoles** tulajdonságot, majd a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="9082d-121">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="9082d-122">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9082d-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9082d-123">**Projekt**: partner Center SDK Samples **osztály**: GetCustomerDirectoryRoles.cs</span><span class="sxs-lookup"><span data-stu-id="9082d-123">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="9082d-124">Az adott szerepkörrel rendelkező ügyfél-felhasználók listájának lekéréséhez először kérje le a megadott ügyfél-azonosítót és a címtár szerepkör-AZONOSÍTÓját.</span><span class="sxs-lookup"><span data-stu-id="9082d-124">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="9082d-125">Ezután használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="9082d-125">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="9082d-126">Ezután hívja meg a **DirectoryRoles** tulajdonságot, majd a **ById ()** metódust, majd a **UserMembers** tulajdonságot, amelyet a **Get ()** vagy a **GetAsync ()** metódus követ.</span><span class="sxs-lookup"><span data-stu-id="9082d-126">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="9082d-127">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9082d-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9082d-128">**Projekt**: PartnerSDK. FeatureSamples **osztály**: GetCustomerDirectoryRoleUserMembers.cs</span><span class="sxs-lookup"><span data-stu-id="9082d-128">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9082d-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="9082d-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9082d-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="9082d-130">Request syntax</span></span>

| <span data-ttu-id="9082d-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="9082d-131">Method</span></span>  | <span data-ttu-id="9082d-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9082d-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9082d-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="9082d-133">**GET**</span></span> | <span data-ttu-id="9082d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="9082d-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="9082d-135">**GET**</span><span class="sxs-lookup"><span data-stu-id="9082d-135">**GET**</span></span> | <span data-ttu-id="9082d-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="9082d-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="9082d-137">**GET**</span><span class="sxs-lookup"><span data-stu-id="9082d-137">**GET**</span></span> | <span data-ttu-id="9082d-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="9082d-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="9082d-139">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="9082d-139">URI parameter</span></span>

<span data-ttu-id="9082d-140">A megfelelő ügyfél azonosításához használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="9082d-140">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="9082d-141">Név</span><span class="sxs-lookup"><span data-stu-id="9082d-141">Name</span></span>                   | <span data-ttu-id="9082d-142">Típus</span><span class="sxs-lookup"><span data-stu-id="9082d-142">Type</span></span>     | <span data-ttu-id="9082d-143">Kötelező</span><span class="sxs-lookup"><span data-stu-id="9082d-143">Required</span></span> | <span data-ttu-id="9082d-144">Leírás</span><span class="sxs-lookup"><span data-stu-id="9082d-144">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9082d-145">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="9082d-145">**customer-tenant-id**</span></span> | <span data-ttu-id="9082d-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="9082d-146">**guid**</span></span> | <span data-ttu-id="9082d-147">Y</span><span class="sxs-lookup"><span data-stu-id="9082d-147">Y</span></span>        | <span data-ttu-id="9082d-148">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="9082d-148">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="9082d-149">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="9082d-149">**user-id**</span></span>            | <span data-ttu-id="9082d-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="9082d-150">**guid**</span></span> | <span data-ttu-id="9082d-151">N</span><span class="sxs-lookup"><span data-stu-id="9082d-151">N</span></span>        | <span data-ttu-id="9082d-152">Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="9082d-152">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="9082d-153">**szerepkör-azonosító**</span><span class="sxs-lookup"><span data-stu-id="9082d-153">**role-id**</span></span>            | <span data-ttu-id="9082d-154">**guid**</span><span class="sxs-lookup"><span data-stu-id="9082d-154">**guid**</span></span> | <span data-ttu-id="9082d-155">N</span><span class="sxs-lookup"><span data-stu-id="9082d-155">N</span></span>        | <span data-ttu-id="9082d-156">Az érték egy szerepkör-típushoz tartozó GUID formátumú **szerepkör-azonosító** .</span><span class="sxs-lookup"><span data-stu-id="9082d-156">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="9082d-157">Ezeket az azonosítókat úgy érheti el, ha lekérdezi az összes címtárbeli szerepkört az összes felhasználói fiókban.</span><span class="sxs-lookup"><span data-stu-id="9082d-157">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="9082d-158">(A fenti második forgatókönyv).</span><span class="sxs-lookup"><span data-stu-id="9082d-158">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9082d-159">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9082d-159">Request headers</span></span>

<span data-ttu-id="9082d-160">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9082d-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9082d-161">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9082d-161">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="9082d-162">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9082d-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="9082d-163">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9082d-163">REST response</span></span>

<span data-ttu-id="9082d-164">Ha a művelet sikeres, ez a metódus az adott felhasználói fiókhoz társított szerepkörök listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="9082d-164">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9082d-165">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9082d-165">Response success and error codes</span></span>

<span data-ttu-id="9082d-166">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="9082d-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9082d-167">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="9082d-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9082d-168">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9082d-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9082d-169">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9082d-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
