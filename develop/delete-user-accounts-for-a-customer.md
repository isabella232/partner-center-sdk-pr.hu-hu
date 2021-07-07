---
title: Felhasználói fiók törlése egy ügyfélnél
description: Egy ügyfél meglévő felhasználói fiókjának törlése.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c45646da43b8926f911942374de5da07f318c526
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973060"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="a22a5-103">Felhasználói fiók törlése egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="a22a5-103">Delete a user account for a customer</span></span>

<span data-ttu-id="a22a5-104">Ez a cikk egy ügyfél meglévő felhasználói fiókjának törlését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="a22a5-104">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a22a5-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a22a5-105">Prerequisites</span></span>

- <span data-ttu-id="a22a5-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a22a5-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a22a5-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="a22a5-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="a22a5-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a22a5-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a22a5-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a22a5-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a22a5-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a22a5-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a22a5-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a22a5-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a22a5-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="a22a5-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a22a5-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a22a5-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a22a5-114">Egy felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="a22a5-114">A user ID.</span></span> <span data-ttu-id="a22a5-115">Ha nem tudja a felhasználói azonosítót, tekintse meg az ügyfél összes felhasználói fiókjának [listáját.](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="a22a5-115">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="a22a5-116">Felhasználói fiók törlése</span><span class="sxs-lookup"><span data-stu-id="a22a5-116">Deleting a user account</span></span>

<span data-ttu-id="a22a5-117">Felhasználói fiók törlésekor a felhasználói állapot  30 napig inaktívra lesz állítva.</span><span class="sxs-lookup"><span data-stu-id="a22a5-117">When you delete a user account, the user state is set to **inactive** for 30 days.</span></span> <span data-ttu-id="a22a5-118">30 nap után a rendszer kiüríti a felhasználói fiókot és a hozzá tartozó adatokat, és nem állítható vissza.</span><span class="sxs-lookup"><span data-stu-id="a22a5-118">After thirty 30 days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="a22a5-119">Az ügyfelek [törölt felhasználói](restore-a-user-for-a-customer.md) fiókjai visszaállíthatóak, ha az inaktív fiók a 30 napos időkereten belül van.</span><span class="sxs-lookup"><span data-stu-id="a22a5-119">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the 30-day window.</span></span> <span data-ttu-id="a22a5-120">Ha azonban visszaállít egy törölt és inaktívként megjelölt fiókot, a rendszer nem ad vissza fiókot a felhasználógyűjtemény tagjaként (például amikor lekért egy listát az ügyfél összes felhasználói [fiókjáról).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="a22a5-120">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="a22a5-121">C\#</span><span class="sxs-lookup"><span data-stu-id="a22a5-121">C\#</span></span>

<span data-ttu-id="a22a5-122">Meglévő ügyfél-felhasználói fiók törlése:</span><span class="sxs-lookup"><span data-stu-id="a22a5-122">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="a22a5-123">Az [**ügyfél azonosításához használja az IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="a22a5-123">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="a22a5-124">A felhasználó azonosításához hívja meg a [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="a22a5-124">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="a22a5-125">Hívja meg [**a Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) metódust a felhasználó törléséhez, és állítsa a felhasználói állapotot inaktívra.</span><span class="sxs-lookup"><span data-stu-id="a22a5-125">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="a22a5-126">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a22a5-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a22a5-127">**Project**: Partnerközpont SDK **Osztály:** DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="a22a5-127">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="a22a5-128">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="a22a5-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a22a5-129">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a22a5-129">Request syntax</span></span>

| <span data-ttu-id="a22a5-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="a22a5-130">Method</span></span>     | <span data-ttu-id="a22a5-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a22a5-131">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a22a5-132">DELETE</span><span class="sxs-lookup"><span data-stu-id="a22a5-132">DELETE</span></span>     | <span data-ttu-id="a22a5-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{felhasználói azonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a22a5-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="a22a5-134">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="a22a5-134">URI parameters</span></span>

<span data-ttu-id="a22a5-135">A következő lekérdezési paraméterekkel azonosíthatja az ügyfelet és a felhasználót.</span><span class="sxs-lookup"><span data-stu-id="a22a5-135">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="a22a5-136">Név</span><span class="sxs-lookup"><span data-stu-id="a22a5-136">Name</span></span>                   | <span data-ttu-id="a22a5-137">Típus</span><span class="sxs-lookup"><span data-stu-id="a22a5-137">Type</span></span>     | <span data-ttu-id="a22a5-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a22a5-138">Required</span></span> | <span data-ttu-id="a22a5-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="a22a5-139">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a22a5-140">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="a22a5-140">customer-tenant-id</span></span>     | <span data-ttu-id="a22a5-141">GUID</span><span class="sxs-lookup"><span data-stu-id="a22a5-141">GUID</span></span>     | <span data-ttu-id="a22a5-142">Y</span><span class="sxs-lookup"><span data-stu-id="a22a5-142">Y</span></span>        | <span data-ttu-id="a22a5-143">Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára az eredmények szűrését egy adott ügyfélre.</span><span class="sxs-lookup"><span data-stu-id="a22a5-143">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="a22a5-144">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="a22a5-144">user-id</span></span>                | <span data-ttu-id="a22a5-145">GUID</span><span class="sxs-lookup"><span data-stu-id="a22a5-145">GUID</span></span>     | <span data-ttu-id="a22a5-146">Y</span><span class="sxs-lookup"><span data-stu-id="a22a5-146">Y</span></span>        | <span data-ttu-id="a22a5-147">Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="a22a5-147">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="a22a5-148">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a22a5-148">Request headers</span></span>

<span data-ttu-id="a22a5-149">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a22a5-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a22a5-150">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a22a5-150">Request body</span></span>

<span data-ttu-id="a22a5-151">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="a22a5-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a22a5-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a22a5-152">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a22a5-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a22a5-153">REST response</span></span>

<span data-ttu-id="a22a5-154">Sikeres művelet esetén ez a metódus **egy 204 Nincs** tartalom állapotkódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="a22a5-154">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a22a5-155">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a22a5-155">Response success and error codes</span></span>

<span data-ttu-id="a22a5-156">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="a22a5-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a22a5-157">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="a22a5-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a22a5-158">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a22a5-158">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a22a5-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a22a5-159">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
