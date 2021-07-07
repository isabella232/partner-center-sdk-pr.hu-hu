---
title: Felhasználói szerepkörök beállítása egy ügyfélnél
description: Az ügyfélfiókon belül címtárszerepkomó-készlet található. Ezekhez a szerepkörökhöz felhasználói fiókokat rendelhet.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a035d711ffa91200fa7b479ed5ec53929aa4feaf
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446700"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="2a53a-104">Felhasználói szerepkörök beállítása egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="2a53a-104">Set user roles for a customer</span></span>

<span data-ttu-id="2a53a-105">Az ügyfélfiókon belül címtárszerepkomó-készlet található.</span><span class="sxs-lookup"><span data-stu-id="2a53a-105">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="2a53a-106">Ezekhez a szerepkörökhöz felhasználói fiókokat rendelhet.</span><span class="sxs-lookup"><span data-stu-id="2a53a-106">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a53a-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2a53a-107">Prerequisites</span></span>

- <span data-ttu-id="2a53a-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2a53a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2a53a-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="2a53a-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="2a53a-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2a53a-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2a53a-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2a53a-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2a53a-112">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="2a53a-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2a53a-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="2a53a-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2a53a-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="2a53a-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2a53a-115">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2a53a-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2a53a-116">C\#</span><span class="sxs-lookup"><span data-stu-id="2a53a-116">C\#</span></span>

<span data-ttu-id="2a53a-117">Ha címtárszerepkört szeretne hozzárendelni egy ügyfélfelhasználóhoz, hozzon létre egy új [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) adatokat a megfelelő felhasználói adatokkal.</span><span class="sxs-lookup"><span data-stu-id="2a53a-117">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="2a53a-118">Ezután hívja meg az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) a megadott ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="2a53a-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="2a53a-119">A szerepkör megadásához használja a [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metódust a címtár-szerepkör azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="2a53a-119">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="2a53a-120">Ezután hozzáféréssel a **UserMembers** gyűjteményhez, és a [**Létrehozás**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) metódussal adja hozzá az új felhasználói tagot az adott szerepkörhöz rendelt felhasználói tagok gyűjteményéhez.</span><span class="sxs-lookup"><span data-stu-id="2a53a-120">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

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

<span data-ttu-id="2a53a-121">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2a53a-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2a53a-122">**Project**: Partnerközpont SDK **Osztály:** AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="2a53a-122">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2a53a-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="2a53a-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2a53a-124">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="2a53a-124">Request syntax</span></span>

| <span data-ttu-id="2a53a-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="2a53a-125">Method</span></span>   | <span data-ttu-id="2a53a-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2a53a-126">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2a53a-127">**Post**</span><span class="sxs-lookup"><span data-stu-id="2a53a-127">**POST**</span></span> | <span data-ttu-id="2a53a-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{szerepkör-azonosító}/usermembers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2a53a-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2a53a-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="2a53a-129">URI parameter</span></span>

<span data-ttu-id="2a53a-130">Az alábbi URI-paraméterekkel azonosíthatja a megfelelő ügyfelet és szerepkört.</span><span class="sxs-lookup"><span data-stu-id="2a53a-130">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="2a53a-131">Annak a felhasználónak az azonosításához, akihez hozzá kell rendelni a szerepkört, a kérelem törzsében meg kell határoznia az azonosító adatokat.</span><span class="sxs-lookup"><span data-stu-id="2a53a-131">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="2a53a-132">Név</span><span class="sxs-lookup"><span data-stu-id="2a53a-132">Name</span></span>                   | <span data-ttu-id="2a53a-133">Típus</span><span class="sxs-lookup"><span data-stu-id="2a53a-133">Type</span></span>     | <span data-ttu-id="2a53a-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2a53a-134">Required</span></span> | <span data-ttu-id="2a53a-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="2a53a-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2a53a-136">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="2a53a-136">**customer-tenant-id**</span></span> | <span data-ttu-id="2a53a-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="2a53a-137">**guid**</span></span> | <span data-ttu-id="2a53a-138">Y</span><span class="sxs-lookup"><span data-stu-id="2a53a-138">Y</span></span>        | <span data-ttu-id="2a53a-139">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="2a53a-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="2a53a-140">**szerepkör-azonosító**</span><span class="sxs-lookup"><span data-stu-id="2a53a-140">**role-id**</span></span>            | <span data-ttu-id="2a53a-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="2a53a-141">**guid**</span></span> | <span data-ttu-id="2a53a-142">Y</span><span class="sxs-lookup"><span data-stu-id="2a53a-142">Y</span></span>        | <span data-ttu-id="2a53a-143">Az érték egy GUID formátumú **szerepkör-azonosító,** amely azonosítja a felhasználóhoz hozzárendelni kívánt szerepkört.</span><span class="sxs-lookup"><span data-stu-id="2a53a-143">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="2a53a-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2a53a-144">Request headers</span></span>

<span data-ttu-id="2a53a-145">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2a53a-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2a53a-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2a53a-146">Request body</span></span>

<span data-ttu-id="2a53a-147">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="2a53a-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="2a53a-148">Név</span><span class="sxs-lookup"><span data-stu-id="2a53a-148">Name</span></span>                  | <span data-ttu-id="2a53a-149">Típus</span><span class="sxs-lookup"><span data-stu-id="2a53a-149">Type</span></span>       | <span data-ttu-id="2a53a-150">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2a53a-150">Required</span></span> | <span data-ttu-id="2a53a-151">Leírás</span><span class="sxs-lookup"><span data-stu-id="2a53a-151">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="2a53a-152">**Id**</span><span class="sxs-lookup"><span data-stu-id="2a53a-152">**Id**</span></span>                | <span data-ttu-id="2a53a-153">**sztring**</span><span class="sxs-lookup"><span data-stu-id="2a53a-153">**string**</span></span> | <span data-ttu-id="2a53a-154">Y</span><span class="sxs-lookup"><span data-stu-id="2a53a-154">Y</span></span>        | <span data-ttu-id="2a53a-155">A szerepkörhöz hozzáadnia kell a felhasználó azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="2a53a-155">The ID of the user to add to the role.</span></span> |
| <span data-ttu-id="2a53a-156">**Megjelenítendő név**</span><span class="sxs-lookup"><span data-stu-id="2a53a-156">**DisplayName**</span></span>       | <span data-ttu-id="2a53a-157">**sztring**</span><span class="sxs-lookup"><span data-stu-id="2a53a-157">**string**</span></span> | <span data-ttu-id="2a53a-158">Y</span><span class="sxs-lookup"><span data-stu-id="2a53a-158">Y</span></span>        | <span data-ttu-id="2a53a-159">A felhasználó rövid megjelenített neve.</span><span class="sxs-lookup"><span data-stu-id="2a53a-159">The friendly display name of the user.</span></span> |
| <span data-ttu-id="2a53a-160">**UserPrincipalName (Felhasználónév)**</span><span class="sxs-lookup"><span data-stu-id="2a53a-160">**UserPrincipalName**</span></span> | <span data-ttu-id="2a53a-161">**sztring**</span><span class="sxs-lookup"><span data-stu-id="2a53a-161">**string**</span></span> | <span data-ttu-id="2a53a-162">Y</span><span class="sxs-lookup"><span data-stu-id="2a53a-162">Y</span></span>        | <span data-ttu-id="2a53a-163">Az egyszerű felhasználó neve.</span><span class="sxs-lookup"><span data-stu-id="2a53a-163">The name of the user principal.</span></span>        |
| <span data-ttu-id="2a53a-164">**Attribútumok**</span><span class="sxs-lookup"><span data-stu-id="2a53a-164">**Attributes**</span></span>        | <span data-ttu-id="2a53a-165">**Objektum**</span><span class="sxs-lookup"><span data-stu-id="2a53a-165">**object**</span></span> | <span data-ttu-id="2a53a-166">Y</span><span class="sxs-lookup"><span data-stu-id="2a53a-166">Y</span></span>        | <span data-ttu-id="2a53a-167">Az "ObjectType":"UserMember" adatokat tartalmazza</span><span class="sxs-lookup"><span data-stu-id="2a53a-167">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="2a53a-168">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2a53a-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2a53a-169">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2a53a-169">REST response</span></span>

<span data-ttu-id="2a53a-170">Ez a metódus visszaadja a szerepkör-azonosítóval csatolt felhasználói fiókot, amikor a felhasználóhoz sikeresen hozzá lett rendelve a szerepkör.</span><span class="sxs-lookup"><span data-stu-id="2a53a-170">This method returns the user account with the role ID attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2a53a-171">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2a53a-171">Response success and error codes</span></span>

<span data-ttu-id="2a53a-172">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="2a53a-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2a53a-173">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="2a53a-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2a53a-174">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2a53a-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2a53a-175">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2a53a-175">Response example</span></span>

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
