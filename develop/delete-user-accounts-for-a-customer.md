---
title: Felhasználói fiók törlése egy ügyfélnél
description: Meglévő felhasználói fiók törlése egy ügyfélhez.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768128"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="1bf3f-103">Felhasználói fiók törlése egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="1bf3f-103">Delete a user account for a customer</span></span>

<span data-ttu-id="1bf3f-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="1bf3f-104">**Applies to:**</span></span>

- <span data-ttu-id="1bf3f-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="1bf3f-105">Partner Center</span></span>

<span data-ttu-id="1bf3f-106">Ez a cikk azt ismerteti, hogyan törölheti az ügyfelek meglévő felhasználói fiókját.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-106">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bf3f-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1bf3f-107">Prerequisites</span></span>

- <span data-ttu-id="1bf3f-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1bf3f-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1bf3f-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1bf3f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1bf3f-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1bf3f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1bf3f-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1bf3f-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1bf3f-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1bf3f-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1bf3f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1bf3f-116">Egy felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-116">A user ID.</span></span> <span data-ttu-id="1bf3f-117">Ha nem rendelkezik a felhasználói AZONOSÍTÓval, tekintse [meg az ügyfélhez tartozó összes felhasználói fiók listájának beolvasása](get-a-list-of-all-user-accounts-for-a-customer.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-117">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="1bf3f-118">Felhasználói fiók törlése</span><span class="sxs-lookup"><span data-stu-id="1bf3f-118">Deleting a user account</span></span>

<span data-ttu-id="1bf3f-119">Felhasználói fiók törlésekor a felhasználói állapot 30 napig **inaktívra** van állítva.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-119">When you delete a user account, the user state is set to **inactive** for thirty days.</span></span> <span data-ttu-id="1bf3f-120">Harminc nap elteltével a felhasználói fiók és a hozzá tartozó adatok törlődnek, és helyreállíthatatlanul történnek.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-120">After thirty days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="1bf3f-121">Ha az inaktív fiók a harminc napos időszakon belül van, [visszaállíthatja az ügyfél törölt felhasználói fiókját](restore-a-user-for-a-customer.md) .</span><span class="sxs-lookup"><span data-stu-id="1bf3f-121">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the thirty day window.</span></span> <span data-ttu-id="1bf3f-122">Ha azonban olyan fiókot állít vissza, amely törölve lett, és inaktívként jelölt meg, a fiók már nem lesz visszaküldve a felhasználói gyűjtemény tagjaként (például ha az [ügyfél összes felhasználói fiókjának listáját kapja](get-a-list-of-all-user-accounts-for-a-customer.md)).</span><span class="sxs-lookup"><span data-stu-id="1bf3f-122">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="1bf3f-123">C\#</span><span class="sxs-lookup"><span data-stu-id="1bf3f-123">C\#</span></span>

<span data-ttu-id="1bf3f-124">Meglévő ügyfél-felhasználói fiók törlése:</span><span class="sxs-lookup"><span data-stu-id="1bf3f-124">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="1bf3f-125">Az ügyfél azonosításához használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-125">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="1bf3f-126">A felhasználó azonosításához hívja meg a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-126">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="1bf3f-127">A [**törlési**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) metódus hívásával törölje a felhasználót, és állítsa inaktívra a felhasználói állapotot.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-127">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="1bf3f-128">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1bf3f-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1bf3f-129">**Projekt**: partner Center SDK Samples **osztály**: DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="1bf3f-129">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1bf3f-130">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="1bf3f-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1bf3f-131">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1bf3f-131">Request syntax</span></span>

| <span data-ttu-id="1bf3f-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="1bf3f-132">Method</span></span>     | <span data-ttu-id="1bf3f-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1bf3f-133">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1bf3f-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="1bf3f-134">DELETE</span></span>     | <span data-ttu-id="1bf3f-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="1bf3f-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1bf3f-136">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="1bf3f-136">URI parameters</span></span>

<span data-ttu-id="1bf3f-137">Az ügyfél és a felhasználó azonosításához használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-137">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="1bf3f-138">Név</span><span class="sxs-lookup"><span data-stu-id="1bf3f-138">Name</span></span>                   | <span data-ttu-id="1bf3f-139">Típus</span><span class="sxs-lookup"><span data-stu-id="1bf3f-139">Type</span></span>     | <span data-ttu-id="1bf3f-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1bf3f-140">Required</span></span> | <span data-ttu-id="1bf3f-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="1bf3f-141">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1bf3f-142">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="1bf3f-142">customer-tenant-id</span></span>     | <span data-ttu-id="1bf3f-143">GUID</span><span class="sxs-lookup"><span data-stu-id="1bf3f-143">GUID</span></span>     | <span data-ttu-id="1bf3f-144">Y</span><span class="sxs-lookup"><span data-stu-id="1bf3f-144">Y</span></span>        | <span data-ttu-id="1bf3f-145">Az érték egy GUID-formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi a viszonteladónak az adott ügyfél eredményeinek szűrését.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-145">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="1bf3f-146">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="1bf3f-146">user-id</span></span>                | <span data-ttu-id="1bf3f-147">GUID</span><span class="sxs-lookup"><span data-stu-id="1bf3f-147">GUID</span></span>     | <span data-ttu-id="1bf3f-148">Y</span><span class="sxs-lookup"><span data-stu-id="1bf3f-148">Y</span></span>        | <span data-ttu-id="1bf3f-149">Az érték egy GUID-formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-149">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="1bf3f-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="1bf3f-150">Request headers</span></span>

<span data-ttu-id="1bf3f-151">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1bf3f-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1bf3f-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1bf3f-152">Request body</span></span>

<span data-ttu-id="1bf3f-153">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1bf3f-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1bf3f-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="1bf3f-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1bf3f-155">REST response</span></span>

<span data-ttu-id="1bf3f-156">Ha ez sikeres, a metódus egy **204** -as értéket ad vissza, amely nem a tartalom állapotkód.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-156">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1bf3f-157">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1bf3f-157">Response success and error codes</span></span>

<span data-ttu-id="1bf3f-158">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1bf3f-159">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1bf3f-160">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="1bf3f-160">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1bf3f-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1bf3f-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
