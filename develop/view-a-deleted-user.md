---
title: Egy ügyfél törölt felhasználóinak megtekintése
description: Lekéri az ügyfél által a törölt CustomerUser-erőforrások listáját az ügyfél azonosítója alapján. Igény szerint beállíthatja az oldalméret méretét. Meg kell adnia egy szűrőt.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768231"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="6abba-105">Egy ügyfél törölt felhasználóinak megtekintése</span><span class="sxs-lookup"><span data-stu-id="6abba-105">View deleted users for a customer</span></span>

<span data-ttu-id="6abba-106">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="6abba-106">**Applies To**</span></span>

- <span data-ttu-id="6abba-107">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="6abba-107">Partner Center</span></span>

<span data-ttu-id="6abba-108">Lekéri az ügyfél által a törölt CustomerUser-erőforrások listáját az ügyfél azonosítója alapján.</span><span class="sxs-lookup"><span data-stu-id="6abba-108">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="6abba-109">Igény szerint beállíthatja az oldalméret méretét.</span><span class="sxs-lookup"><span data-stu-id="6abba-109">You can optionally set a page size.</span></span> <span data-ttu-id="6abba-110">Meg kell adnia egy szűrőt.</span><span class="sxs-lookup"><span data-stu-id="6abba-110">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6abba-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6abba-111">Prerequisites</span></span>

- <span data-ttu-id="6abba-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="6abba-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6abba-113">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="6abba-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6abba-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6abba-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6abba-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="6abba-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6abba-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="6abba-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6abba-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="6abba-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6abba-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="6abba-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6abba-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6abba-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="6abba-120">Mi történik, amikor töröl egy felhasználói fiókot?</span><span class="sxs-lookup"><span data-stu-id="6abba-120">What happens when you delete a user account?</span></span>

<span data-ttu-id="6abba-121">Felhasználói fiók törlésekor a felhasználói állapot "inaktív" értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="6abba-121">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="6abba-122">Így harminc napig marad, amely után a felhasználói fiók és a hozzá tartozó adatok törlődnek, és helyreállíthatatlanul történnek.</span><span class="sxs-lookup"><span data-stu-id="6abba-122">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="6abba-123">Ha a harminc napos ablakban szeretné visszaállítani a törölt felhasználói fiókot, tekintse meg a [törölt felhasználó visszaállítása az ügyfélre](restore-a-user-for-a-customer.md)című témakört.</span><span class="sxs-lookup"><span data-stu-id="6abba-123">If you want to restore a deleted user account within the thirty day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="6abba-124">Ha törölve lett, és "inaktív" jelöléssel jelölte meg, a felhasználói fiókot a rendszer már nem adja vissza a felhasználói gyűjtemény tagjaként (például az [ügyfél összes felhasználói fiókjának lekérése lista](get-a-list-of-all-user-accounts-for-a-customer.md)használatával).</span><span class="sxs-lookup"><span data-stu-id="6abba-124">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="6abba-125">A még nem törölt felhasználók listájának lekéréséhez le kell kérdezni az inaktív felhasználói fiókokat.</span><span class="sxs-lookup"><span data-stu-id="6abba-125">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="6abba-126">C\#</span><span class="sxs-lookup"><span data-stu-id="6abba-126">C\#</span></span>

<span data-ttu-id="6abba-127">A törölt felhasználók listájának lekéréséhez hozzon létre egy lekérdezést, amely azokat az ügyfelek felhasználóinak szűri, akiknek az állapota inaktív.</span><span class="sxs-lookup"><span data-stu-id="6abba-127">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="6abba-128">Először hozza létre a szűrőt egy [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) objektumnak a paraméterekkel való létrehozásával, ahogy az a következő kódrészletben látható.</span><span class="sxs-lookup"><span data-stu-id="6abba-128">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="6abba-129">Ezután hozza létre a lekérdezést a [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) metódus használatával.</span><span class="sxs-lookup"><span data-stu-id="6abba-129">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="6abba-130">Ha nem szeretné, hogy a lapozható eredmények legyenek, használja helyette a [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) metódust.</span><span class="sxs-lookup"><span data-stu-id="6abba-130">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="6abba-131">Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="6abba-131">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="6abba-132">Végül hívja meg a [**lekérdezési**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) módszert a kérelem elküldéséhez.</span><span class="sxs-lookup"><span data-stu-id="6abba-132">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

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

<span data-ttu-id="6abba-133">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6abba-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6abba-134">**Projekt**: partner Center SDK Samples **osztály**: GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="6abba-134">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6abba-135">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="6abba-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6abba-136">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6abba-136">Request syntax</span></span>

| <span data-ttu-id="6abba-137">Metódus</span><span class="sxs-lookup"><span data-stu-id="6abba-137">Method</span></span>  | <span data-ttu-id="6abba-138">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6abba-138">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6abba-139">**GET**</span><span class="sxs-lookup"><span data-stu-id="6abba-139">**GET**</span></span> | <span data-ttu-id="6abba-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? méret = {size} &szűrő = {Filter} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6abba-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6abba-141">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="6abba-141">URI parameter</span></span>

<span data-ttu-id="6abba-142">A kérelem létrehozásakor használja az alábbi elérési utat és a lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="6abba-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="6abba-143">Név</span><span class="sxs-lookup"><span data-stu-id="6abba-143">Name</span></span>        | <span data-ttu-id="6abba-144">Típus</span><span class="sxs-lookup"><span data-stu-id="6abba-144">Type</span></span>   | <span data-ttu-id="6abba-145">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6abba-145">Required</span></span> | <span data-ttu-id="6abba-146">Leírás</span><span class="sxs-lookup"><span data-stu-id="6abba-146">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6abba-147">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="6abba-147">customer-id</span></span> | <span data-ttu-id="6abba-148">guid</span><span class="sxs-lookup"><span data-stu-id="6abba-148">guid</span></span>   | <span data-ttu-id="6abba-149">Igen</span><span class="sxs-lookup"><span data-stu-id="6abba-149">Yes</span></span>      | <span data-ttu-id="6abba-150">Az érték egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="6abba-150">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="6abba-151">size</span><span class="sxs-lookup"><span data-stu-id="6abba-151">size</span></span>        | <span data-ttu-id="6abba-152">int</span><span class="sxs-lookup"><span data-stu-id="6abba-152">int</span></span>    | <span data-ttu-id="6abba-153">Nem</span><span class="sxs-lookup"><span data-stu-id="6abba-153">No</span></span>       | <span data-ttu-id="6abba-154">Az egyszerre megjelenítendő eredmények száma.</span><span class="sxs-lookup"><span data-stu-id="6abba-154">The number of results to be displayed at one time.</span></span> <span data-ttu-id="6abba-155">Ezt a paramétert nem kötelező megadni.</span><span class="sxs-lookup"><span data-stu-id="6abba-155">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="6abba-156">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="6abba-156">filter</span></span>      | <span data-ttu-id="6abba-157">filter (szűrő)</span><span class="sxs-lookup"><span data-stu-id="6abba-157">filter</span></span> | <span data-ttu-id="6abba-158">Igen</span><span class="sxs-lookup"><span data-stu-id="6abba-158">Yes</span></span>      | <span data-ttu-id="6abba-159">A felhasználói keresést szűrő lekérdezés.</span><span class="sxs-lookup"><span data-stu-id="6abba-159">The query that filters the user search.</span></span> <span data-ttu-id="6abba-160">A törölt felhasználók beolvasásához a következő karakterláncot kell tartalmaznia és kódolnia: {"Field": "UserState", "value": "inaktív", "operátor": "Equals"}.</span><span class="sxs-lookup"><span data-stu-id="6abba-160">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6abba-161">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6abba-161">Request headers</span></span>

<span data-ttu-id="6abba-162">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6abba-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6abba-163">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6abba-163">Request body</span></span>

<span data-ttu-id="6abba-164">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="6abba-164">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6abba-165">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6abba-165">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6abba-166">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6abba-166">REST response</span></span>

<span data-ttu-id="6abba-167">Ha ez sikeres, ez a metódus [CustomerUser](user-resources.md#customeruser) -erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="6abba-167">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6abba-168">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6abba-168">Response success and error codes</span></span>

<span data-ttu-id="6abba-169">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="6abba-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6abba-170">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="6abba-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6abba-171">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="6abba-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6abba-172">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6abba-172">Response example</span></span>

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
