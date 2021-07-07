---
title: Egy ügyfél felhasználói szerepköreinek lekérése
description: Lekért lista a felhasználói fiókhoz csatolt összes szerepkörről/engedélyről. A változatok közé tartozik az ügyfél összes felhasználói fiókra vonatkozó összes engedélyének lekért listája, valamint az adott szerepkörhöz rendelkező felhasználók listája.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f58e8b7eae5bb47265bb1ac83fcdcd160f735d2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445918"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="329a0-104">Egy ügyfél felhasználói szerepköreinek lekérése</span><span class="sxs-lookup"><span data-stu-id="329a0-104">Get user roles for a customer</span></span>

<span data-ttu-id="329a0-105">Lekért lista a felhasználói fiókhoz csatolt összes szerepkörről/engedélyről.</span><span class="sxs-lookup"><span data-stu-id="329a0-105">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="329a0-106">A változatok közé tartozik az ügyfél összes felhasználói fiókra vonatkozó összes engedélyének lekért listája, valamint az adott szerepkörhöz rendelkező felhasználók listája.</span><span class="sxs-lookup"><span data-stu-id="329a0-106">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="329a0-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="329a0-107">Prerequisites</span></span>

- <span data-ttu-id="329a0-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="329a0-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="329a0-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="329a0-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="329a0-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="329a0-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="329a0-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="329a0-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="329a0-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="329a0-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="329a0-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="329a0-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="329a0-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="329a0-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="329a0-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="329a0-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="329a0-116">C\#</span><span class="sxs-lookup"><span data-stu-id="329a0-116">C\#</span></span>

<span data-ttu-id="329a0-117">Egy adott ügyfél összes címtárszerepkörének lekérését először a megadott ügyfél-azonosítóval kell lekérni.</span><span class="sxs-lookup"><span data-stu-id="329a0-117">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="329a0-118">Ezután használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="329a0-118">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="329a0-119">Ezután hívja meg **a DirectoryRoles** tulajdonságot, majd a **Get() vagy** **a GetAsync() metódust.**</span><span class="sxs-lookup"><span data-stu-id="329a0-119">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="329a0-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="329a0-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="329a0-121">**Project:** Partnerközpont SDK Samples **Osztály:** GetCustomerDirectoryRoles.cs</span><span class="sxs-lookup"><span data-stu-id="329a0-121">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="329a0-122">Az adott szerepkört használó ügyfélfelhasználók listájának lekérése először a megadott ügyfél-azonosítót és a címtárszerepkör-azonosítót kell lekérni.</span><span class="sxs-lookup"><span data-stu-id="329a0-122">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="329a0-123">Ezután használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="329a0-123">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="329a0-124">Ezután hívja meg a **DirectoryRoles** tulajdonságot, majd a **ById()** metódust, majd a **UserMembers** tulajdonságot, majd a **Get() vagy** **a GetAsync() metódust.**</span><span class="sxs-lookup"><span data-stu-id="329a0-124">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="329a0-125">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="329a0-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="329a0-126">**Project:** PartnerSDK.FeatureSamples **osztály:** GetCustomerDirectoryRoleUserMembers.cs</span><span class="sxs-lookup"><span data-stu-id="329a0-126">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="329a0-127">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="329a0-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="329a0-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="329a0-128">Request syntax</span></span>

| <span data-ttu-id="329a0-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="329a0-129">Method</span></span>  | <span data-ttu-id="329a0-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="329a0-130">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="329a0-131">**Kap**</span><span class="sxs-lookup"><span data-stu-id="329a0-131">**GET**</span></span> | <span data-ttu-id="329a0-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{felhasználói azonosító}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="329a0-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="329a0-133">**Kap**</span><span class="sxs-lookup"><span data-stu-id="329a0-133">**GET**</span></span> | <span data-ttu-id="329a0-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="329a0-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="329a0-135">**Kap**</span><span class="sxs-lookup"><span data-stu-id="329a0-135">**GET**</span></span> | <span data-ttu-id="329a0-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{szerepkör-azonosító}/usermembers</span><span class="sxs-lookup"><span data-stu-id="329a0-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="329a0-137">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="329a0-137">URI parameter</span></span>

<span data-ttu-id="329a0-138">Az alábbi lekérdezési paraméterrel azonosíthatja a megfelelő ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="329a0-138">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="329a0-139">Név</span><span class="sxs-lookup"><span data-stu-id="329a0-139">Name</span></span>                   | <span data-ttu-id="329a0-140">Típus</span><span class="sxs-lookup"><span data-stu-id="329a0-140">Type</span></span>     | <span data-ttu-id="329a0-141">Kötelező</span><span class="sxs-lookup"><span data-stu-id="329a0-141">Required</span></span> | <span data-ttu-id="329a0-142">Leírás</span><span class="sxs-lookup"><span data-stu-id="329a0-142">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="329a0-143">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="329a0-143">**customer-tenant-id**</span></span> | <span data-ttu-id="329a0-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="329a0-144">**guid**</span></span> | <span data-ttu-id="329a0-145">Y</span><span class="sxs-lookup"><span data-stu-id="329a0-145">Y</span></span>        | <span data-ttu-id="329a0-146">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="329a0-146">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="329a0-147">**felhasználóazonosító**</span><span class="sxs-lookup"><span data-stu-id="329a0-147">**user-id**</span></span>            | <span data-ttu-id="329a0-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="329a0-148">**guid**</span></span> | <span data-ttu-id="329a0-149">N</span><span class="sxs-lookup"><span data-stu-id="329a0-149">N</span></span>        | <span data-ttu-id="329a0-150">Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="329a0-150">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="329a0-151">**szerepkör-azonosító**</span><span class="sxs-lookup"><span data-stu-id="329a0-151">**role-id**</span></span>            | <span data-ttu-id="329a0-152">**guid**</span><span class="sxs-lookup"><span data-stu-id="329a0-152">**guid**</span></span> | <span data-ttu-id="329a0-153">N</span><span class="sxs-lookup"><span data-stu-id="329a0-153">N</span></span>        | <span data-ttu-id="329a0-154">Az érték egy GUID formátumú **szerepkör-azonosító,** amely egy szerepkörtípushoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="329a0-154">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="329a0-155">Ezeket az azonosítókat úgy kaphatja meg, ha lekérdezi egy ügyfél összes címtár-szerepkörét az összes felhasználói fiókra.</span><span class="sxs-lookup"><span data-stu-id="329a0-155">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="329a0-156">(A második forgatókönyv, fent).</span><span class="sxs-lookup"><span data-stu-id="329a0-156">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="329a0-157">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="329a0-157">Request headers</span></span>

<span data-ttu-id="329a0-158">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="329a0-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="329a0-159">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="329a0-159">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="329a0-160">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="329a0-160">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="329a0-161">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="329a0-161">REST response</span></span>

<span data-ttu-id="329a0-162">Sikeres művelet esetén ez a metódus az adott felhasználói fiókhoz társított szerepkörök listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="329a0-162">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="329a0-163">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="329a0-163">Response success and error codes</span></span>

<span data-ttu-id="329a0-164">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="329a0-164">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="329a0-165">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="329a0-165">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="329a0-166">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="329a0-166">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="329a0-167">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="329a0-167">Response example</span></span>

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
