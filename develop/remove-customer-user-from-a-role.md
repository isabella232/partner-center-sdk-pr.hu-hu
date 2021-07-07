---
title: Egy ügyfélfelhasználó eltávolítása egy szerepkörből
description: Felhasználó eltávolítása egy címtár-szerepkörből az ügyfélfiókon belül.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 36dc742c4f713131b4996d7dc945b6dd008a3ef5
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445646"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="5b1ec-103">Egy ügyfélfelhasználó eltávolítása egy szerepkörből</span><span class="sxs-lookup"><span data-stu-id="5b1ec-103">Remove a customer user from a role</span></span>

<span data-ttu-id="5b1ec-104">Felhasználó eltávolítása egy címtár-szerepkörből az ügyfélfiókon belül.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-104">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b1ec-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5b1ec-105">Prerequisites</span></span>

- <span data-ttu-id="5b1ec-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5b1ec-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5b1ec-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5b1ec-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b1ec-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5b1ec-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="5b1ec-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5b1ec-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5b1ec-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5b1ec-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5b1ec-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b1ec-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5b1ec-114">C\#</span><span class="sxs-lookup"><span data-stu-id="5b1ec-114">C\#</span></span>

<span data-ttu-id="5b1ec-115">Ha el szeretne távolítani egy felhasználót egy címtárszerepkörből, válassza ki a módosítani kívánt felhasználót az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus hívásával. Innen adja meg a szerepkört a [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metódussal és a címtárszerepkör-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-115">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="5b1ec-116">Ezután a [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) metódussal azonosíthatja az eltávolítani kívánt felhasználót, a [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) metódussal pedig eltávolíthatja a felhasználót a szerepkörből.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-116">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="5b1ec-117">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5b1ec-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5b1ec-118">**Project**: Partnerközpont SDK **Osztály:** RemoveCustomerUserMemberFromDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="5b1ec-118">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5b1ec-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="5b1ec-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5b1ec-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5b1ec-120">Request syntax</span></span>

| <span data-ttu-id="5b1ec-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="5b1ec-121">Method</span></span>     | <span data-ttu-id="5b1ec-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5b1ec-122">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5b1ec-123">**Töröl**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-123">**DELETE**</span></span> | <span data-ttu-id="5b1ec-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfél-bérlő-azonosító}/directoryroles/{szerepkör-azonosító}/usermembers/{felhasználói-azonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="5b1ec-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5b1ec-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="5b1ec-125">URI parameter</span></span>

<span data-ttu-id="5b1ec-126">Az alábbi URI-paraméterekkel azonosíthatja a megfelelő ügyfelet, szerepkört és felhasználót.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-126">Use the following URI parameters to identify the correct customer, role, and user.</span></span>

| <span data-ttu-id="5b1ec-127">Név</span><span class="sxs-lookup"><span data-stu-id="5b1ec-127">Name</span></span>                   | <span data-ttu-id="5b1ec-128">Típus</span><span class="sxs-lookup"><span data-stu-id="5b1ec-128">Type</span></span>     | <span data-ttu-id="5b1ec-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5b1ec-129">Required</span></span> | <span data-ttu-id="5b1ec-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="5b1ec-130">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="5b1ec-131">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-131">**customer-tenant-id**</span></span> | <span data-ttu-id="5b1ec-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-132">**guid**</span></span> | <span data-ttu-id="5b1ec-133">Y</span><span class="sxs-lookup"><span data-stu-id="5b1ec-133">Y</span></span>        | <span data-ttu-id="5b1ec-134">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-134">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="5b1ec-135">**szerepkör-azonosító**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-135">**role-id**</span></span>            | <span data-ttu-id="5b1ec-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-136">**guid**</span></span> | <span data-ttu-id="5b1ec-137">Y</span><span class="sxs-lookup"><span data-stu-id="5b1ec-137">Y</span></span>        | <span data-ttu-id="5b1ec-138">Az érték egy GUID formátumú **szerepkör-azonosító,** amely azonosítja a szerepkört.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-138">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="5b1ec-139">**felhasználóazonosító**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-139">**user-id**</span></span>            | <span data-ttu-id="5b1ec-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="5b1ec-140">**guid**</span></span> | <span data-ttu-id="5b1ec-141">Y</span><span class="sxs-lookup"><span data-stu-id="5b1ec-141">Y</span></span>        | <span data-ttu-id="5b1ec-142">Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókot azonosít.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-142">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="5b1ec-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5b1ec-143">Request headers</span></span>

<span data-ttu-id="5b1ec-144">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="5b1ec-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5b1ec-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5b1ec-145">Request body</span></span>

<span data-ttu-id="5b1ec-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5b1ec-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5b1ec-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5b1ec-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5b1ec-148">REST response</span></span>

<span data-ttu-id="5b1ec-149">Ha a felhasználót sikeresen eltávolítják a szerepkörből, a válasz törzse üres lesz.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-149">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5b1ec-150">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5b1ec-150">Response success and error codes</span></span>

<span data-ttu-id="5b1ec-151">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5b1ec-152">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="5b1ec-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5b1ec-153">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="5b1ec-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5b1ec-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5b1ec-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
