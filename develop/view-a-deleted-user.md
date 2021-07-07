---
title: Egy ügyfél törölt felhasználóinak megtekintése
description: Lekérte az ügyfél törölt CustomerUser erőforrásainak listáját ügyfélazonosító alapján. Igény szerint meg is állíthatja az oldalméretet. Meg kell adnunk egy szűrőt.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f4fec958a9a6bb580d35de1cf3007e1db3b2b650
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445306"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="4ff69-105">Egy ügyfél törölt felhasználóinak megtekintése</span><span class="sxs-lookup"><span data-stu-id="4ff69-105">View deleted users for a customer</span></span>

<span data-ttu-id="4ff69-106">Lekérte az ügyfél törölt CustomerUser erőforrásainak listáját ügyfélazonosító alapján.</span><span class="sxs-lookup"><span data-stu-id="4ff69-106">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="4ff69-107">Igény szerint meg is állíthatja az oldalméretet.</span><span class="sxs-lookup"><span data-stu-id="4ff69-107">You can optionally set a page size.</span></span> <span data-ttu-id="4ff69-108">Meg kell adnunk egy szűrőt.</span><span class="sxs-lookup"><span data-stu-id="4ff69-108">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ff69-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4ff69-109">Prerequisites</span></span>

- <span data-ttu-id="4ff69-110">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4ff69-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4ff69-111">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="4ff69-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4ff69-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4ff69-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4ff69-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4ff69-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4ff69-114">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4ff69-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4ff69-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="4ff69-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4ff69-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="4ff69-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4ff69-117">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4ff69-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="4ff69-118">Mi történik, ha töröl egy felhasználói fiókot?</span><span class="sxs-lookup"><span data-stu-id="4ff69-118">What happens when you delete a user account?</span></span>

<span data-ttu-id="4ff69-119">Felhasználói fiók törlésekor a felhasználói állapot "inaktív" lesz.</span><span class="sxs-lookup"><span data-stu-id="4ff69-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="4ff69-120">Ez 30 napig így marad, ezt követően a rendszer kiüríti a felhasználói fiókot és a hozzá tartozó adatokat, és nem állítható vissza.</span><span class="sxs-lookup"><span data-stu-id="4ff69-120">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="4ff69-121">Ha egy törölt felhasználói fiókot szeretne visszaállítani a 30 napos időkereten belül, tekintse meg a Törölt felhasználó visszaállítása egy [ügyfélre vonatkozó útmutatót.](restore-a-user-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="4ff69-121">If you want to restore a deleted user account within the 30-day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="4ff69-122">A törlést és az "inaktívként" megjelölt felhasználói fiókot a rendszer már nem a felhasználói gyűjtemény tagjaként visszaadja (például egy ügyfél összes felhasználói fiókjának lekért [listáját használva).](get-a-list-of-all-user-accounts-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="4ff69-122">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="4ff69-123">A törölt, még nem véglegesen törölt felhasználók listájának lekérdezéséhez le kellkérdeznie az inaktívra beállított felhasználói fiókokat.</span><span class="sxs-lookup"><span data-stu-id="4ff69-123">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="4ff69-124">C\#</span><span class="sxs-lookup"><span data-stu-id="4ff69-124">C\#</span></span>

<span data-ttu-id="4ff69-125">A törölt felhasználók listájának lekéréséhez állítson össze egy olyan lekérdezést, amely az inaktív állapotú ügyfelekre szűr.</span><span class="sxs-lookup"><span data-stu-id="4ff69-125">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="4ff69-126">Először hozza létre a szűrőt egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektum példányosulatával a paraméterekkel az alábbi kódrészletben látható módon.</span><span class="sxs-lookup"><span data-stu-id="4ff69-126">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="4ff69-127">Ezután hozza létre a lekérdezést a [**BuildIndexedQuery metódussal.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery)</span><span class="sxs-lookup"><span data-stu-id="4ff69-127">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="4ff69-128">Ha nem szeretne lapozott eredményeket, használhatja helyette a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódust.</span><span class="sxs-lookup"><span data-stu-id="4ff69-128">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="4ff69-129">Ezután használja az [**IAggregatePartner.Customers.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="4ff69-129">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="4ff69-130">Végül hívja meg [**a Query metódust**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) a kérés elküldéhez.</span><span class="sxs-lookup"><span data-stu-id="4ff69-130">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

<span data-ttu-id="4ff69-131">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4ff69-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4ff69-132">**Project**: Partnerközpont SDK **Osztály:** GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="4ff69-132">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4ff69-133">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4ff69-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4ff69-134">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="4ff69-134">Request syntax</span></span>

| <span data-ttu-id="4ff69-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="4ff69-135">Method</span></span>  | <span data-ttu-id="4ff69-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4ff69-136">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4ff69-137">**Kap**</span><span class="sxs-lookup"><span data-stu-id="4ff69-137">**GET**</span></span> | <span data-ttu-id="4ff69-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users?size={méret}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4ff69-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4ff69-139">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4ff69-139">URI parameter</span></span>

<span data-ttu-id="4ff69-140">A kérelem létrehozásakor használja a következő elérési utat és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="4ff69-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="4ff69-141">Név</span><span class="sxs-lookup"><span data-stu-id="4ff69-141">Name</span></span>        | <span data-ttu-id="4ff69-142">Típus</span><span class="sxs-lookup"><span data-stu-id="4ff69-142">Type</span></span>   | <span data-ttu-id="4ff69-143">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4ff69-143">Required</span></span> | <span data-ttu-id="4ff69-144">Leírás</span><span class="sxs-lookup"><span data-stu-id="4ff69-144">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4ff69-145">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="4ff69-145">customer-id</span></span> | <span data-ttu-id="4ff69-146">guid</span><span class="sxs-lookup"><span data-stu-id="4ff69-146">guid</span></span>   | <span data-ttu-id="4ff69-147">Igen</span><span class="sxs-lookup"><span data-stu-id="4ff69-147">Yes</span></span>      | <span data-ttu-id="4ff69-148">Az érték egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="4ff69-148">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="4ff69-149">size</span><span class="sxs-lookup"><span data-stu-id="4ff69-149">size</span></span>        | <span data-ttu-id="4ff69-150">int</span><span class="sxs-lookup"><span data-stu-id="4ff69-150">int</span></span>    | <span data-ttu-id="4ff69-151">Nem</span><span class="sxs-lookup"><span data-stu-id="4ff69-151">No</span></span>       | <span data-ttu-id="4ff69-152">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="4ff69-152">The number of results to be displayed at one time.</span></span> <span data-ttu-id="4ff69-153">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="4ff69-153">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="4ff69-154">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="4ff69-154">filter</span></span>      | <span data-ttu-id="4ff69-155">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="4ff69-155">filter</span></span> | <span data-ttu-id="4ff69-156">Igen</span><span class="sxs-lookup"><span data-stu-id="4ff69-156">Yes</span></span>      | <span data-ttu-id="4ff69-157">A felhasználó keresését szűrő lekérdezés.</span><span class="sxs-lookup"><span data-stu-id="4ff69-157">The query that filters the user search.</span></span> <span data-ttu-id="4ff69-158">A törölt felhasználók lekéréséhez bele kell foglalnia és kódolnia kell a következő sztringet: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span><span class="sxs-lookup"><span data-stu-id="4ff69-158">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4ff69-159">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4ff69-159">Request headers</span></span>

<span data-ttu-id="4ff69-160">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4ff69-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4ff69-161">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4ff69-161">Request body</span></span>

<span data-ttu-id="4ff69-162">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="4ff69-162">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4ff69-163">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4ff69-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4ff69-164">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4ff69-164">REST response</span></span>

<span data-ttu-id="4ff69-165">Ha a művelet sikeres, ez a metódus [CustomerUser-erőforrások](user-resources.md#customeruser) gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="4ff69-165">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4ff69-166">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4ff69-166">Response success and error codes</span></span>

<span data-ttu-id="4ff69-167">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4ff69-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4ff69-168">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4ff69-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4ff69-169">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="4ff69-169">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4ff69-170">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4ff69-170">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
