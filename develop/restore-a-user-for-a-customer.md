---
title: Törölt felhasználó visszaállítása egy ügyfélnél
description: Törölt felhasználó visszaállítása ügyfél- és felhasználói azonosító alapján.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445714"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="53507-103">Törölt felhasználó visszaállítása egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="53507-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="53507-104">Törölt felhasználó visszaállítása  ügyfél- és felhasználói azonosító alapján.</span><span class="sxs-lookup"><span data-stu-id="53507-104">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53507-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="53507-105">Prerequisites</span></span>

- <span data-ttu-id="53507-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="53507-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="53507-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="53507-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="53507-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="53507-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="53507-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="53507-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="53507-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="53507-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="53507-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="53507-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="53507-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="53507-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="53507-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="53507-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="53507-114">A felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="53507-114">The user ID.</span></span> <span data-ttu-id="53507-115">Ha nem tudja a felhasználói azonosítót, lásd: Törölt felhasználók [megtekintése egy ügyfélhez.](view-a-deleted-user.md)</span><span class="sxs-lookup"><span data-stu-id="53507-115">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="53507-116">Mikor lehet visszaállítani egy törölt felhasználói fiókot?</span><span class="sxs-lookup"><span data-stu-id="53507-116">When can you restore a deleted user account?</span></span>

<span data-ttu-id="53507-117">A felhasználói fiók törlésekor a felhasználói állapot "inaktív" lesz.</span><span class="sxs-lookup"><span data-stu-id="53507-117">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="53507-118">Ez 30 napig így marad, ezt követően a rendszer kiüríti a felhasználói fiókot és a hozzá tartozó adatokat, és nem állítható vissza.</span><span class="sxs-lookup"><span data-stu-id="53507-118">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="53507-119">Törölt felhasználói fiókot csak ebben a 30 napos időszakban lehet visszaállítani.</span><span class="sxs-lookup"><span data-stu-id="53507-119">You can only restore a deleted user account during this 30-day window.</span></span> <span data-ttu-id="53507-120">A törlést és az "inaktívként" megjelölt felhasználói fiókot a rendszer már nem a felhasználói gyűjtemény tagjaként visszaadja (például a Get a list of all user accounts for a customer (Ügyfél összes felhasználói fiókjának [lekért listája) használatával).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="53507-120">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="53507-121">C\#</span><span class="sxs-lookup"><span data-stu-id="53507-121">C\#</span></span>

<span data-ttu-id="53507-122">Felhasználó visszaállításához hozza létre a [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) osztály egy új példányát, és állítsa a [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) tulajdonság értékét [**UserState.Active értékre.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)</span><span class="sxs-lookup"><span data-stu-id="53507-122">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="53507-123">Egy törölt felhasználót úgy lehet visszaállítani, hogy a felhasználó állapotát aktívra állítani.</span><span class="sxs-lookup"><span data-stu-id="53507-123">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="53507-124">A felhasználói erőforrás többi mezőjét nem kell újra kitöltenünk.</span><span class="sxs-lookup"><span data-stu-id="53507-124">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="53507-125">Ezek az értékek automatikusan visszaállnak a törölt, inaktív felhasználói erőforrásból.</span><span class="sxs-lookup"><span data-stu-id="53507-125">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="53507-126">Ezután használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához, és a [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="53507-126">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="53507-127">Végül hívja meg a [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) metódust, és adja át a **CustomerUser** példányt, hogy elküldje a felhasználó visszaállítására vonatkozó kérést.</span><span class="sxs-lookup"><span data-stu-id="53507-127">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

<span data-ttu-id="53507-128">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="53507-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="53507-129">**Project:** Partnerközpont SDK Samples **Osztály:** CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="53507-129">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="53507-130">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="53507-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="53507-131">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="53507-131">Request syntax</span></span>

| <span data-ttu-id="53507-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="53507-132">Method</span></span>    | <span data-ttu-id="53507-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="53507-133">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="53507-134">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="53507-134">**PATCH**</span></span> | <span data-ttu-id="53507-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{felhasználói azonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="53507-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="53507-136">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="53507-136">URI parameter</span></span>

<span data-ttu-id="53507-137">A következő lekérdezési paraméterekkel adhatja meg az ügyfél-azonosítót és a felhasználói azonosítót.</span><span class="sxs-lookup"><span data-stu-id="53507-137">Use the following query parameters to specify the customer ID and user ID.</span></span>

| <span data-ttu-id="53507-138">Név</span><span class="sxs-lookup"><span data-stu-id="53507-138">Name</span></span>                   | <span data-ttu-id="53507-139">Típus</span><span class="sxs-lookup"><span data-stu-id="53507-139">Type</span></span>     | <span data-ttu-id="53507-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="53507-140">Required</span></span> | <span data-ttu-id="53507-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="53507-141">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="53507-142">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="53507-142">**customer-tenant-id**</span></span> | <span data-ttu-id="53507-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="53507-143">**guid**</span></span> | <span data-ttu-id="53507-144">Y</span><span class="sxs-lookup"><span data-stu-id="53507-144">Y</span></span>        | <span data-ttu-id="53507-145">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy az eredményeket egy adott ügyfélre szűrje.</span><span class="sxs-lookup"><span data-stu-id="53507-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="53507-146">**felhasználóazonosító**</span><span class="sxs-lookup"><span data-stu-id="53507-146">**user-id**</span></span>            | <span data-ttu-id="53507-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="53507-147">**guid**</span></span> | <span data-ttu-id="53507-148">Y</span><span class="sxs-lookup"><span data-stu-id="53507-148">Y</span></span>        | <span data-ttu-id="53507-149">Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="53507-149">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="53507-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="53507-150">Request headers</span></span>

<span data-ttu-id="53507-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="53507-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="53507-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="53507-152">Request body</span></span>

<span data-ttu-id="53507-153">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="53507-153">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="53507-154">Név</span><span class="sxs-lookup"><span data-stu-id="53507-154">Name</span></span>       | <span data-ttu-id="53507-155">Típus</span><span class="sxs-lookup"><span data-stu-id="53507-155">Type</span></span>   | <span data-ttu-id="53507-156">Kötelező</span><span class="sxs-lookup"><span data-stu-id="53507-156">Required</span></span> | <span data-ttu-id="53507-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="53507-157">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="53507-158">Állapot</span><span class="sxs-lookup"><span data-stu-id="53507-158">State</span></span>      | <span data-ttu-id="53507-159">sztring</span><span class="sxs-lookup"><span data-stu-id="53507-159">string</span></span> | <span data-ttu-id="53507-160">Y</span><span class="sxs-lookup"><span data-stu-id="53507-160">Y</span></span>        | <span data-ttu-id="53507-161">A felhasználói állapot.</span><span class="sxs-lookup"><span data-stu-id="53507-161">The user state.</span></span> <span data-ttu-id="53507-162">Törölt felhasználó visszaállításához ennek a sztringnek "aktívnak" kell lennie.</span><span class="sxs-lookup"><span data-stu-id="53507-162">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="53507-163">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="53507-163">Attributes</span></span> | <span data-ttu-id="53507-164">object</span><span class="sxs-lookup"><span data-stu-id="53507-164">object</span></span> | <span data-ttu-id="53507-165">N</span><span class="sxs-lookup"><span data-stu-id="53507-165">N</span></span>        | <span data-ttu-id="53507-166">Tartalmazza az "ObjectType": "CustomerUser" adatokat.</span><span class="sxs-lookup"><span data-stu-id="53507-166">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="53507-167">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="53507-167">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="53507-168">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="53507-168">REST response</span></span>

<span data-ttu-id="53507-169">Ha ez sikeres, a válasz visszaadja a visszaállított felhasználói adatokat a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="53507-169">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="53507-170">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="53507-170">Response success and error codes</span></span>

<span data-ttu-id="53507-171">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="53507-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="53507-172">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="53507-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="53507-173">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="53507-173">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="53507-174">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="53507-174">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
