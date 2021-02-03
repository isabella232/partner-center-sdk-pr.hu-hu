---
title: Törölt felhasználó visszaállítása egy ügyfélnél
description: Törölt felhasználó visszaállítása ügyfél-azonosító és felhasználói azonosító alapján.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768407"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="fc8f1-103">Törölt felhasználó visszaállítása egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="fc8f1-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="fc8f1-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="fc8f1-104">**Applies To**</span></span>

- <span data-ttu-id="fc8f1-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="fc8f1-105">Partner Center</span></span>

<span data-ttu-id="fc8f1-106">Törölt **felhasználó** visszaállítása ügyfél-azonosító és felhasználói azonosító alapján.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-106">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc8f1-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fc8f1-107">Prerequisites</span></span>

- <span data-ttu-id="fc8f1-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc8f1-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="fc8f1-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc8f1-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fc8f1-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="fc8f1-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fc8f1-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fc8f1-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fc8f1-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fc8f1-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc8f1-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fc8f1-116">A felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-116">The user ID.</span></span> <span data-ttu-id="fc8f1-117">Ha nem rendelkezik a felhasználói AZONOSÍTÓval, tekintse [meg az ügyfél törölt felhasználóinak megtekintése](view-a-deleted-user.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-117">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="fc8f1-118">Mikor állíthatja vissza a törölt felhasználói fiókot?</span><span class="sxs-lookup"><span data-stu-id="fc8f1-118">When can you restore a deleted user account?</span></span>

<span data-ttu-id="fc8f1-119">Felhasználói fiók törlésekor a felhasználói állapot "inaktív" értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="fc8f1-120">Így harminc napig marad, amely után a felhasználói fiók és a hozzá tartozó adatok törlődnek, és helyreállíthatatlanul történnek.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-120">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="fc8f1-121">A törölt felhasználói fiókokat csak ezen a harminc napos időszakban lehet visszaállítani.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-121">You can only restore a deleted user account during this thirty-day window.</span></span> <span data-ttu-id="fc8f1-122">Ha törölve lett, és "inaktív" jelöléssel jelölte meg, a felhasználói fiók már nem lesz visszaküldve a felhasználói gyűjtemény tagjaként (például az [ügyfél összes felhasználói fiókjának lekérése lista](get-a-list-of-all-user-accounts-for-a-customer.md)használatával).</span><span class="sxs-lookup"><span data-stu-id="fc8f1-122">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="fc8f1-123">C\#</span><span class="sxs-lookup"><span data-stu-id="fc8f1-123">C\#</span></span>

<span data-ttu-id="fc8f1-124">Egy felhasználó visszaállításához hozza létre a [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) osztály új példányát, és állítsa be a [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) tulajdonság értékét a [**UserState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)értékre.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-124">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="fc8f1-125">A törölt felhasználókat úgy állíthatja vissza, hogy a felhasználó állapotát aktívra állítja.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-125">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="fc8f1-126">A felhasználói erőforrásban nem kell újratöltenie a fennmaradó mezőket.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-126">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="fc8f1-127">Ezeket az értékeket a rendszer automatikusan visszaállítja a törölt, inaktív felhasználói erőforrásból.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-127">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="fc8f1-128">Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához, valamint a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-128">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="fc8f1-129">Végül hívja meg a [**patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) metódust, és adja át a **CustomerUser** -példányt a felhasználó visszaállítására vonatkozó kérés elküldéséhez.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-129">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

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

<span data-ttu-id="fc8f1-130">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fc8f1-130">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fc8f1-131">**Projekt**: partner Center SDK Samples **osztály**: CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="fc8f1-131">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc8f1-132">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="fc8f1-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc8f1-133">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fc8f1-133">Request syntax</span></span>

| <span data-ttu-id="fc8f1-134">Metódus</span><span class="sxs-lookup"><span data-stu-id="fc8f1-134">Method</span></span>    | <span data-ttu-id="fc8f1-135">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="fc8f1-135">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc8f1-136">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="fc8f1-136">**PATCH**</span></span> | <span data-ttu-id="fc8f1-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="fc8f1-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fc8f1-138">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="fc8f1-138">URI parameter</span></span>

<span data-ttu-id="fc8f1-139">Az ügyfél-azonosító és a felhasználói azonosító megadásához használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-139">Use the following query parameters to specify the customer id and user id.</span></span>

| <span data-ttu-id="fc8f1-140">Név</span><span class="sxs-lookup"><span data-stu-id="fc8f1-140">Name</span></span>                   | <span data-ttu-id="fc8f1-141">Típus</span><span class="sxs-lookup"><span data-stu-id="fc8f1-141">Type</span></span>     | <span data-ttu-id="fc8f1-142">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fc8f1-142">Required</span></span> | <span data-ttu-id="fc8f1-143">Leírás</span><span class="sxs-lookup"><span data-stu-id="fc8f1-143">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc8f1-144">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="fc8f1-144">**customer-tenant-id**</span></span> | <span data-ttu-id="fc8f1-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="fc8f1-145">**guid**</span></span> | <span data-ttu-id="fc8f1-146">Y</span><span class="sxs-lookup"><span data-stu-id="fc8f1-146">Y</span></span>        | <span data-ttu-id="fc8f1-147">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó az eredményeket egy adott ügyfélre szűrje.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-147">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="fc8f1-148">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="fc8f1-148">**user-id**</span></span>            | <span data-ttu-id="fc8f1-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="fc8f1-149">**guid**</span></span> | <span data-ttu-id="fc8f1-150">Y</span><span class="sxs-lookup"><span data-stu-id="fc8f1-150">Y</span></span>        | <span data-ttu-id="fc8f1-151">Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-151">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="fc8f1-152">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="fc8f1-152">Request headers</span></span>

<span data-ttu-id="fc8f1-153">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fc8f1-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc8f1-154">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="fc8f1-154">Request body</span></span>

<span data-ttu-id="fc8f1-155">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-155">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="fc8f1-156">Név</span><span class="sxs-lookup"><span data-stu-id="fc8f1-156">Name</span></span>       | <span data-ttu-id="fc8f1-157">Típus</span><span class="sxs-lookup"><span data-stu-id="fc8f1-157">Type</span></span>   | <span data-ttu-id="fc8f1-158">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fc8f1-158">Required</span></span> | <span data-ttu-id="fc8f1-159">Leírás</span><span class="sxs-lookup"><span data-stu-id="fc8f1-159">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="fc8f1-160">Állam</span><span class="sxs-lookup"><span data-stu-id="fc8f1-160">State</span></span>      | <span data-ttu-id="fc8f1-161">sztring</span><span class="sxs-lookup"><span data-stu-id="fc8f1-161">string</span></span> | <span data-ttu-id="fc8f1-162">Y</span><span class="sxs-lookup"><span data-stu-id="fc8f1-162">Y</span></span>        | <span data-ttu-id="fc8f1-163">A felhasználói állapot.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-163">The user state.</span></span> <span data-ttu-id="fc8f1-164">A törölt felhasználók visszaállításához a karakterláncnak "aktív" értéknek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-164">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="fc8f1-165">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="fc8f1-165">Attributes</span></span> | <span data-ttu-id="fc8f1-166">object</span><span class="sxs-lookup"><span data-stu-id="fc8f1-166">object</span></span> | <span data-ttu-id="fc8f1-167">N</span><span class="sxs-lookup"><span data-stu-id="fc8f1-167">N</span></span>        | <span data-ttu-id="fc8f1-168">A "objektumtípus": "CustomerUser" kifejezést tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-168">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="fc8f1-169">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="fc8f1-169">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fc8f1-170">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="fc8f1-170">REST response</span></span>

<span data-ttu-id="fc8f1-171">Ha a művelet sikeres, a válasz a visszaállított felhasználói adatokat adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-171">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc8f1-172">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fc8f1-172">Response success and error codes</span></span>

<span data-ttu-id="fc8f1-173">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-173">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc8f1-174">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-174">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc8f1-175">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="fc8f1-175">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fc8f1-176">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="fc8f1-176">Response example</span></span>

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
