---
title: Felhasználói szerepkörök beállítása egy ügyfélnél
description: Egy ügyfél-fiókban több címtár-szerepkör található. A szerepkörökhöz felhasználói fiókokat is hozzárendelhet.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768268"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="f71f0-104">Felhasználói szerepkörök beállítása egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="f71f0-104">Set user roles for a customer</span></span>

<span data-ttu-id="f71f0-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="f71f0-105">**Applies To**</span></span>

- <span data-ttu-id="f71f0-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f71f0-106">Partner Center</span></span>

<span data-ttu-id="f71f0-107">Egy ügyfél-fiókban több címtár-szerepkör található.</span><span class="sxs-lookup"><span data-stu-id="f71f0-107">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="f71f0-108">A szerepkörökhöz felhasználói fiókokat is hozzárendelhet.</span><span class="sxs-lookup"><span data-stu-id="f71f0-108">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f71f0-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f71f0-109">Prerequisites</span></span>

- <span data-ttu-id="f71f0-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f71f0-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f71f0-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="f71f0-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f71f0-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f71f0-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f71f0-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="f71f0-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f71f0-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="f71f0-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f71f0-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="f71f0-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f71f0-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="f71f0-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f71f0-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f71f0-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f71f0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="f71f0-118">C\#</span></span>

<span data-ttu-id="f71f0-119">Ha egy címtárbeli szerepkört szeretne hozzárendelni egy ügyfél-felhasználóhoz, hozzon létre egy új [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) a megfelelő felhasználói adatokkal.</span><span class="sxs-lookup"><span data-stu-id="f71f0-119">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="f71f0-120">Ezután hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="f71f0-120">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="f71f0-121">Innen válassza a [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metódust a címtár SZEREPKÖR-azonosítóval a szerepkör megadásához.</span><span class="sxs-lookup"><span data-stu-id="f71f0-121">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="f71f0-122">Ezután nyissa meg a **UserMembers** gyűjteményt, és a [**create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) metódussal adja hozzá az új felhasználói tagot az adott szerepkörhöz rendelt felhasználói tagok gyűjteményéhez.</span><span class="sxs-lookup"><span data-stu-id="f71f0-122">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

<span data-ttu-id="f71f0-123">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f71f0-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f71f0-124">**Projekt**: partner Center SDK Samples **osztály**: AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="f71f0-124">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f71f0-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f71f0-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f71f0-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f71f0-126">Request syntax</span></span>

| <span data-ttu-id="f71f0-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="f71f0-127">Method</span></span>   | <span data-ttu-id="f71f0-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f71f0-128">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f71f0-129">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="f71f0-129">**POST**</span></span> | <span data-ttu-id="f71f0-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers http/1.1</span><span class="sxs-lookup"><span data-stu-id="f71f0-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f71f0-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f71f0-131">URI parameter</span></span>

<span data-ttu-id="f71f0-132">A megfelelő ügyfél és szerepkör azonosításához használja a következő URI-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="f71f0-132">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="f71f0-133">Annak a felhasználónak a azonosításához, akihez a szerepkört hozzá szeretné rendelni, adja meg az azonosítási adatokat a kérelem törzsében.</span><span class="sxs-lookup"><span data-stu-id="f71f0-133">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="f71f0-134">Név</span><span class="sxs-lookup"><span data-stu-id="f71f0-134">Name</span></span>                   | <span data-ttu-id="f71f0-135">Típus</span><span class="sxs-lookup"><span data-stu-id="f71f0-135">Type</span></span>     | <span data-ttu-id="f71f0-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f71f0-136">Required</span></span> | <span data-ttu-id="f71f0-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="f71f0-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f71f0-138">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="f71f0-138">**customer-tenant-id**</span></span> | <span data-ttu-id="f71f0-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="f71f0-139">**guid**</span></span> | <span data-ttu-id="f71f0-140">Y</span><span class="sxs-lookup"><span data-stu-id="f71f0-140">Y</span></span>        | <span data-ttu-id="f71f0-141">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="f71f0-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="f71f0-142">**szerepkör-azonosító**</span><span class="sxs-lookup"><span data-stu-id="f71f0-142">**role-id**</span></span>            | <span data-ttu-id="f71f0-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="f71f0-143">**guid**</span></span> | <span data-ttu-id="f71f0-144">Y</span><span class="sxs-lookup"><span data-stu-id="f71f0-144">Y</span></span>        | <span data-ttu-id="f71f0-145">Az érték egy GUID formátumú **szerepkör-azonosító** , amely azonosítja a felhasználóhoz hozzárendelni kívánt szerepkört.</span><span class="sxs-lookup"><span data-stu-id="f71f0-145">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="f71f0-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f71f0-146">Request headers</span></span>

<span data-ttu-id="f71f0-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f71f0-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f71f0-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f71f0-148">Request body</span></span>

<span data-ttu-id="f71f0-149">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="f71f0-149">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="f71f0-150">Név</span><span class="sxs-lookup"><span data-stu-id="f71f0-150">Name</span></span>                  | <span data-ttu-id="f71f0-151">Típus</span><span class="sxs-lookup"><span data-stu-id="f71f0-151">Type</span></span>       | <span data-ttu-id="f71f0-152">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f71f0-152">Required</span></span> | <span data-ttu-id="f71f0-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="f71f0-153">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="f71f0-154">**ID**</span><span class="sxs-lookup"><span data-stu-id="f71f0-154">**Id**</span></span>                | <span data-ttu-id="f71f0-155">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="f71f0-155">**string**</span></span> | <span data-ttu-id="f71f0-156">Y</span><span class="sxs-lookup"><span data-stu-id="f71f0-156">Y</span></span>        | <span data-ttu-id="f71f0-157">A szerepkörhöz hozzáadandó felhasználó azonosítója.</span><span class="sxs-lookup"><span data-stu-id="f71f0-157">The Id of the user to add to the role.</span></span> |
| <span data-ttu-id="f71f0-158">**Megjelenítendő név**</span><span class="sxs-lookup"><span data-stu-id="f71f0-158">**DisplayName**</span></span>       | <span data-ttu-id="f71f0-159">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="f71f0-159">**string**</span></span> | <span data-ttu-id="f71f0-160">Y</span><span class="sxs-lookup"><span data-stu-id="f71f0-160">Y</span></span>        | <span data-ttu-id="f71f0-161">A felhasználó felhasználóbarát megjelenítendő neve.</span><span class="sxs-lookup"><span data-stu-id="f71f0-161">The friendly display name of the user.</span></span> |
| <span data-ttu-id="f71f0-162">**UserPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="f71f0-162">**UserPrincipalName**</span></span> | <span data-ttu-id="f71f0-163">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="f71f0-163">**string**</span></span> | <span data-ttu-id="f71f0-164">Y</span><span class="sxs-lookup"><span data-stu-id="f71f0-164">Y</span></span>        | <span data-ttu-id="f71f0-165">A felhasználói tag neve.</span><span class="sxs-lookup"><span data-stu-id="f71f0-165">The name of the user principal.</span></span>        |
| <span data-ttu-id="f71f0-166">**Attribútumok**</span><span class="sxs-lookup"><span data-stu-id="f71f0-166">**Attributes**</span></span>        | <span data-ttu-id="f71f0-167">**objektum**</span><span class="sxs-lookup"><span data-stu-id="f71f0-167">**object**</span></span> | <span data-ttu-id="f71f0-168">Y</span><span class="sxs-lookup"><span data-stu-id="f71f0-168">Y</span></span>        | <span data-ttu-id="f71f0-169">A "objektumtípus": "UserMember" kifejezést tartalmazza</span><span class="sxs-lookup"><span data-stu-id="f71f0-169">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="f71f0-170">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f71f0-170">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="f71f0-171">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f71f0-171">REST response</span></span>

<span data-ttu-id="f71f0-172">Ez a metódus visszaadja azt a felhasználói fiókot, amelyhez a szerepkör-azonosító csatolva lett, ha a felhasználó sikeresen hozzárendelte a szerepkört.</span><span class="sxs-lookup"><span data-stu-id="f71f0-172">This method returns the user account with the role id attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f71f0-173">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f71f0-173">Response success and error codes</span></span>

<span data-ttu-id="f71f0-174">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f71f0-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f71f0-175">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f71f0-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f71f0-176">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="f71f0-176">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f71f0-177">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f71f0-177">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
