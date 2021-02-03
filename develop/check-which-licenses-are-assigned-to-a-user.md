---
title: Adott felhasználóhoz rendelt licencek lekérése
description: Ismerje meg, hogyan használhatja a partner Center API-kat a felhasználóhoz tartozó licencek listájának lekéréséhez egy ügyfél-fiókon belül.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b754ba4ecba7067f78c6868b387bac0190bfd230
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768604"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="e2819-103">Felhasználói fiókon belüli felhasználóhoz rendelt licencek lekérése</span><span class="sxs-lookup"><span data-stu-id="e2819-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="e2819-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="e2819-104">**Applies to:**</span></span>

- <span data-ttu-id="e2819-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e2819-105">Partner Center</span></span>

<span data-ttu-id="e2819-106">A felhasználóhoz rendelt licencek listájának lekérése egy ügyfél-fiókon belül.</span><span class="sxs-lookup"><span data-stu-id="e2819-106">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="e2819-107">Az itt bemutatott példák a Group1-ból hozzárendelt licenceket adják vissza, amely az Azure Active Directory által felügyelt licenceket jelképező alapértelmezett licenckód.</span><span class="sxs-lookup"><span data-stu-id="e2819-107">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="e2819-108">A megadott licencfeltételek alapján hozzárendelt licencek lekéréséhez lásd: [licencek hozzárendelése egy felhasználóhoz a licencfeltételeket](get-licenses-assigned-to-a-user-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="e2819-108">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2819-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e2819-109">Prerequisites</span></span>

- <span data-ttu-id="e2819-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="e2819-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e2819-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="e2819-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e2819-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e2819-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e2819-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="e2819-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e2819-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="e2819-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e2819-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="e2819-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e2819-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="e2819-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e2819-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e2819-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e2819-118">Egy felhasználói azonosító.</span><span class="sxs-lookup"><span data-stu-id="e2819-118">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="e2819-119">C\#</span><span class="sxs-lookup"><span data-stu-id="e2819-119">C\#</span></span>

<span data-ttu-id="e2819-120">Annak megállapításához, hogy mely licencek vannak hozzárendelve egy felhasználóhoz az alapértelmezett Group1, először használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="e2819-120">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="e2819-121">Ezután hívja meg a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a felhasználói azonosítóval a felhasználó azonosításához.</span><span class="sxs-lookup"><span data-stu-id="e2819-121">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="e2819-122">Ezután szerezzen be egy felületet az ügyfél felhasználói licencelési műveleteihez a [**licencek**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="e2819-122">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="e2819-123">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) metódust a felhasználóhoz rendelt licencek gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="e2819-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="e2819-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e2819-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e2819-125">**Projekt**: partner Center SDK Samples **osztály**: CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="e2819-125">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e2819-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="e2819-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e2819-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e2819-127">Request syntax</span></span>

| <span data-ttu-id="e2819-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="e2819-128">Method</span></span>  | <span data-ttu-id="e2819-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e2819-129">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e2819-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="e2819-130">**GET**</span></span> | <span data-ttu-id="e2819-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenses http/1.1</span><span class="sxs-lookup"><span data-stu-id="e2819-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e2819-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="e2819-132">URI parameter</span></span>

<span data-ttu-id="e2819-133">Az ügyfél és a felhasználó azonosításához használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="e2819-133">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="e2819-134">Név</span><span class="sxs-lookup"><span data-stu-id="e2819-134">Name</span></span>        | <span data-ttu-id="e2819-135">Típus</span><span class="sxs-lookup"><span data-stu-id="e2819-135">Type</span></span>   | <span data-ttu-id="e2819-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e2819-136">Required</span></span> | <span data-ttu-id="e2819-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="e2819-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="e2819-138">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="e2819-138">customer-id</span></span> | <span data-ttu-id="e2819-139">sztring</span><span class="sxs-lookup"><span data-stu-id="e2819-139">string</span></span> | <span data-ttu-id="e2819-140">Igen</span><span class="sxs-lookup"><span data-stu-id="e2819-140">Yes</span></span>      | <span data-ttu-id="e2819-141">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="e2819-141">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="e2819-142">felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="e2819-142">user-id</span></span>     | <span data-ttu-id="e2819-143">sztring</span><span class="sxs-lookup"><span data-stu-id="e2819-143">string</span></span> | <span data-ttu-id="e2819-144">Igen</span><span class="sxs-lookup"><span data-stu-id="e2819-144">Yes</span></span>      | <span data-ttu-id="e2819-145">Egy GUID formátumú karakterlánc, amely azonosítja a felhasználót.</span><span class="sxs-lookup"><span data-stu-id="e2819-145">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="e2819-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e2819-146">Request headers</span></span>

<span data-ttu-id="e2819-147">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e2819-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e2819-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e2819-148">Request body</span></span>

<span data-ttu-id="e2819-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="e2819-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e2819-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e2819-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e2819-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e2819-151">REST response</span></span>

<span data-ttu-id="e2819-152">Ha ez sikeres, a válasz törzse tartalmazza a [licenc](license-resources.md#license) -erőforrások gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="e2819-152">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e2819-153">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e2819-153">Response success and error codes</span></span>

<span data-ttu-id="e2819-154">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="e2819-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e2819-155">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="e2819-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e2819-156">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e2819-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e2819-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e2819-157">Response example</span></span>

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