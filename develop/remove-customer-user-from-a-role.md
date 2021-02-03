---
title: Egy ügyfélfelhasználó eltávolítása egy szerepkörből
description: Felhasználó eltávolítása egy ügyfél-fiókban lévő címtárbeli szerepkörből.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253e86f3733bbf2b9c593c5ca3f3e2fccce7c2c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768307"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="c8e40-103">Egy ügyfélfelhasználó eltávolítása egy szerepkörből</span><span class="sxs-lookup"><span data-stu-id="c8e40-103">Remove a customer user from a role</span></span>

<span data-ttu-id="c8e40-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="c8e40-104">**Applies To**</span></span>

- <span data-ttu-id="c8e40-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c8e40-105">Partner Center</span></span>

<span data-ttu-id="c8e40-106">Felhasználó eltávolítása egy ügyfél-fiókban lévő címtárbeli szerepkörből.</span><span class="sxs-lookup"><span data-stu-id="c8e40-106">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8e40-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c8e40-107">Prerequisites</span></span>

- <span data-ttu-id="c8e40-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c8e40-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c8e40-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="c8e40-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c8e40-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8e40-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c8e40-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="c8e40-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c8e40-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="c8e40-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c8e40-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="c8e40-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c8e40-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="c8e40-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c8e40-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c8e40-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c8e40-116">C\#</span><span class="sxs-lookup"><span data-stu-id="c8e40-116">C\#</span></span>

<span data-ttu-id="c8e40-117">Ha el szeretne távolítani egy felhasználót egy címtárbeli szerepkörből, válassza ki azt az ügyfelet, akit a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus hívásával szeretne módosítani, majd adja meg a szerepkört a [**DirectoryRoles. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metódus használatával a címtár szerepkör-azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="c8e40-117">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="c8e40-118">Ezután nyissa meg a [**UserMembers. ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) metódust az eltávolítandó felhasználó azonosításához, valamint a [**törlési**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) metódust a felhasználó a szerepkörből való eltávolításához.</span><span class="sxs-lookup"><span data-stu-id="c8e40-118">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="c8e40-119">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c8e40-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c8e40-120">**Projekt**: partner Center SDK Samples **osztály**: RemoveCustomerUserMemberFromDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="c8e40-120">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c8e40-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c8e40-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c8e40-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c8e40-122">Request syntax</span></span>

| <span data-ttu-id="c8e40-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="c8e40-123">Method</span></span>     | <span data-ttu-id="c8e40-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c8e40-124">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c8e40-125">**TÖRLÉSE**</span><span class="sxs-lookup"><span data-stu-id="c8e40-125">**DELETE**</span></span> | <span data-ttu-id="c8e40-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c8e40-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c8e40-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c8e40-127">URI parameter</span></span>

<span data-ttu-id="c8e40-128">A megfelelő ügyfél, szerepkör és felhasználó azonosításához használja a következő URI-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="c8e40-128">Use the following URI parameters to identify the correct customer, role and user.</span></span>

| <span data-ttu-id="c8e40-129">Név</span><span class="sxs-lookup"><span data-stu-id="c8e40-129">Name</span></span>                   | <span data-ttu-id="c8e40-130">Típus</span><span class="sxs-lookup"><span data-stu-id="c8e40-130">Type</span></span>     | <span data-ttu-id="c8e40-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c8e40-131">Required</span></span> | <span data-ttu-id="c8e40-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="c8e40-132">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="c8e40-133">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="c8e40-133">**customer-tenant-id**</span></span> | <span data-ttu-id="c8e40-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="c8e40-134">**guid**</span></span> | <span data-ttu-id="c8e40-135">Y</span><span class="sxs-lookup"><span data-stu-id="c8e40-135">Y</span></span>        | <span data-ttu-id="c8e40-136">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító** , amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="c8e40-136">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="c8e40-137">**szerepkör-azonosító**</span><span class="sxs-lookup"><span data-stu-id="c8e40-137">**role-id**</span></span>            | <span data-ttu-id="c8e40-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="c8e40-138">**guid**</span></span> | <span data-ttu-id="c8e40-139">Y</span><span class="sxs-lookup"><span data-stu-id="c8e40-139">Y</span></span>        | <span data-ttu-id="c8e40-140">Az érték egy GUID formátumú **szerepkör-azonosító** , amely azonosítja a szerepkört.</span><span class="sxs-lookup"><span data-stu-id="c8e40-140">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="c8e40-141">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="c8e40-141">**user-id**</span></span>            | <span data-ttu-id="c8e40-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="c8e40-142">**guid**</span></span> | <span data-ttu-id="c8e40-143">Y</span><span class="sxs-lookup"><span data-stu-id="c8e40-143">Y</span></span>        | <span data-ttu-id="c8e40-144">Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókot azonosít.</span><span class="sxs-lookup"><span data-stu-id="c8e40-144">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="c8e40-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c8e40-145">Request headers</span></span>

<span data-ttu-id="c8e40-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c8e40-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c8e40-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c8e40-147">Request body</span></span>

<span data-ttu-id="c8e40-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c8e40-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c8e40-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c8e40-149">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="c8e40-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c8e40-150">REST response</span></span>

<span data-ttu-id="c8e40-151">Ha a felhasználó eltávolítása sikeresen megtörtént a szerepkörből, a válasz törzse üres.</span><span class="sxs-lookup"><span data-stu-id="c8e40-151">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c8e40-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c8e40-152">Response success and error codes</span></span>

<span data-ttu-id="c8e40-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c8e40-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c8e40-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c8e40-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c8e40-155">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="c8e40-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c8e40-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c8e40-156">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
