---
title: Adott felhasználóhoz rendelt licencek lekérése
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat egy ügyfélfiókon belüli felhasználóhoz rendelt licencek listájának lekért listára.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a51fc4493e2476107206b03be66004d030e2aa47
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974063"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="3163b-103">Ügyfélfiókon belüli felhasználóhoz rendelt licencek lekérte</span><span class="sxs-lookup"><span data-stu-id="3163b-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="3163b-104">Az ügyfélfiókon belüli felhasználókhoz rendelt licencek listájának lekért listája.</span><span class="sxs-lookup"><span data-stu-id="3163b-104">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="3163b-105">Az itt látható példák a group1 (1. csoport) által hozzárendelt licenceket– az alapértelmezett licenccsoportot – jelennek meg, amelyek a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3163b-105">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="3163b-106">A megadott licenccsoportokból hozzárendelt licencek lekért licenceket lásd: Felhasználóhoz rendelt licencek lekért [licenccsoport szerint.](get-licenses-assigned-to-a-user-by-license-group.md)</span><span class="sxs-lookup"><span data-stu-id="3163b-106">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3163b-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3163b-107">Prerequisites</span></span>

- <span data-ttu-id="3163b-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3163b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3163b-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="3163b-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3163b-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3163b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3163b-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="3163b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3163b-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="3163b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3163b-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="3163b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3163b-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="3163b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3163b-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3163b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3163b-116">Egy felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="3163b-116">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="3163b-117">C\#</span><span class="sxs-lookup"><span data-stu-id="3163b-117">C\#</span></span>

<span data-ttu-id="3163b-118">Annak ellenőrzéshez, hogy mely licencek vannak hozzárendelve egy felhasználóhoz az alapértelmezett group1 licenccsoportból, először használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="3163b-118">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="3163b-119">Ezután hívja meg [**a Users.ById metódust**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) a felhasználói azonosítóval a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="3163b-119">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="3163b-120">Ezután a Licencek tulajdonságból szerezze be az ügyfélfelhasználói [**licencműveletekkel kapcsolatos**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) felületet.</span><span class="sxs-lookup"><span data-stu-id="3163b-120">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="3163b-121">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) metódust a felhasználóhoz rendelt licencek gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="3163b-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="3163b-122">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3163b-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3163b-123">**Project**: Partnerközpont SDK **Osztály:** CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="3163b-123">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3163b-124">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="3163b-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3163b-125">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3163b-125">Request syntax</span></span>

| <span data-ttu-id="3163b-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="3163b-126">Method</span></span>  | <span data-ttu-id="3163b-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3163b-127">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3163b-128">**Kap**</span><span class="sxs-lookup"><span data-stu-id="3163b-128">**GET**</span></span> | <span data-ttu-id="3163b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users/{felhasználói azonosító}/licenses HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3163b-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3163b-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="3163b-130">URI parameter</span></span>

<span data-ttu-id="3163b-131">Az ügyfél és a felhasználó azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="3163b-131">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="3163b-132">Név</span><span class="sxs-lookup"><span data-stu-id="3163b-132">Name</span></span>        | <span data-ttu-id="3163b-133">Típus</span><span class="sxs-lookup"><span data-stu-id="3163b-133">Type</span></span>   | <span data-ttu-id="3163b-134">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3163b-134">Required</span></span> | <span data-ttu-id="3163b-135">Leírás</span><span class="sxs-lookup"><span data-stu-id="3163b-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="3163b-136">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="3163b-136">customer-id</span></span> | <span data-ttu-id="3163b-137">sztring</span><span class="sxs-lookup"><span data-stu-id="3163b-137">string</span></span> | <span data-ttu-id="3163b-138">Igen</span><span class="sxs-lookup"><span data-stu-id="3163b-138">Yes</span></span>      | <span data-ttu-id="3163b-139">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="3163b-139">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="3163b-140">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="3163b-140">user-id</span></span>     | <span data-ttu-id="3163b-141">sztring</span><span class="sxs-lookup"><span data-stu-id="3163b-141">string</span></span> | <span data-ttu-id="3163b-142">Igen</span><span class="sxs-lookup"><span data-stu-id="3163b-142">Yes</span></span>      | <span data-ttu-id="3163b-143">A felhasználót azonosító GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="3163b-143">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="3163b-144">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3163b-144">Request headers</span></span>

<span data-ttu-id="3163b-145">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3163b-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3163b-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3163b-146">Request body</span></span>

<span data-ttu-id="3163b-147">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="3163b-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3163b-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3163b-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3163b-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3163b-149">REST response</span></span>

<span data-ttu-id="3163b-150">Ha a művelet sikeres, a válasz törzse tartalmazza a [licencerőforrások](license-resources.md#license) gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="3163b-150">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3163b-151">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3163b-151">Response success and error codes</span></span>

<span data-ttu-id="3163b-152">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="3163b-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3163b-153">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="3163b-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3163b-154">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3163b-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3163b-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="3163b-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3883
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CV: WYkHYMfWTUajFosK.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 00:29:24 GMT

{
    "totalCount": 1,
    "items": [{
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```