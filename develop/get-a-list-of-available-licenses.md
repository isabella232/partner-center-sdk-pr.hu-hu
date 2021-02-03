---
title: A rendelkezésre álló licencek listájának lekérése
description: A megadott ügyfél felhasználói számára elérhető licencek listájának beolvasása.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f675e5b96b2f2040d662c0dc7f1e06625f267689
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768239"
---
# <a name="get-a-list-of-available-licenses"></a><span data-ttu-id="40532-103">A rendelkezésre álló licencek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="40532-103">Get a list of available licenses</span></span>

<span data-ttu-id="40532-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="40532-104">**Applies to:**</span></span>

- <span data-ttu-id="40532-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="40532-105">Partner Center</span></span>

<span data-ttu-id="40532-106">Ez a cikk azt ismerteti, hogyan kérhető le a megadott ügyfél felhasználói számára elérhető licencek listája.</span><span class="sxs-lookup"><span data-stu-id="40532-106">This article describes how to get a list of licenses available to users of the specified customer.</span></span>

<span data-ttu-id="40532-107">Az alábbi példák a **Group1**-ból elérhető licenceket adják vissza, amely az Azure Active Directory (Azure ad) által felügyelt licenceket jelképező alapértelmezett licenckód.</span><span class="sxs-lookup"><span data-stu-id="40532-107">The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="40532-108">A megadott licencfeltételek elérhető licencek lekéréséhez lásd: a [rendelkezésre álló licencek listájának](get-a-list-of-available-licenses-by-license-group.md)beolvasása a licencfeltételeket.</span><span class="sxs-lookup"><span data-stu-id="40532-108">To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40532-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="40532-109">Prerequisites</span></span>

- <span data-ttu-id="40532-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="40532-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="40532-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="40532-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="40532-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40532-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="40532-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="40532-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="40532-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="40532-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="40532-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="40532-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="40532-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="40532-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="40532-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="40532-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="40532-118">C\#</span><span class="sxs-lookup"><span data-stu-id="40532-118">C\#</span></span>

<span data-ttu-id="40532-119">Az alapértelmezett licenckiszolgálóról elérhető licencek listájának lekérése az ügyfél felhasználói számára:</span><span class="sxs-lookup"><span data-stu-id="40532-119">To retrieve the list of licenses available from the default license group to users of a customer:</span></span>

1. <span data-ttu-id="40532-120">Az ügyfél azonosításához használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="40532-120">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="40532-121">Szerezze be a [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) tulajdonság értékét, hogy lekérje az ügyfél által előfizetett SKU-gyűjtési műveletekhez tartozó felületet.</span><span class="sxs-lookup"><span data-stu-id="40532-121">Get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span>

3. <span data-ttu-id="40532-122">A licencek listájának lekéréséhez hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="40532-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

<span data-ttu-id="40532-123">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="40532-123">For an example, see the following:</span></span>

- <span data-ttu-id="40532-124">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="40532-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="40532-125">Projekt: **partner Center SDK-minták**</span><span class="sxs-lookup"><span data-stu-id="40532-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="40532-126">Osztály: **GetCustomerSubscribedSkus.cs**</span><span class="sxs-lookup"><span data-stu-id="40532-126">Class: **GetCustomerSubscribedSkus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="40532-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="40532-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="40532-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="40532-128">Request syntax</span></span>

| <span data-ttu-id="40532-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="40532-129">Method</span></span>  | <span data-ttu-id="40532-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="40532-130">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="40532-131">**GET**</span><span class="sxs-lookup"><span data-stu-id="40532-131">**GET**</span></span> | <span data-ttu-id="40532-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/subscribedskus http/1.1</span><span class="sxs-lookup"><span data-stu-id="40532-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="40532-133">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="40532-133">URI parameter</span></span>

<span data-ttu-id="40532-134">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="40532-134">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="40532-135">Név</span><span class="sxs-lookup"><span data-stu-id="40532-135">Name</span></span>        | <span data-ttu-id="40532-136">Típus</span><span class="sxs-lookup"><span data-stu-id="40532-136">Type</span></span>   | <span data-ttu-id="40532-137">Kötelező</span><span class="sxs-lookup"><span data-stu-id="40532-137">Required</span></span> | <span data-ttu-id="40532-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="40532-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="40532-139">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="40532-139">customer-id</span></span> | <span data-ttu-id="40532-140">sztring</span><span class="sxs-lookup"><span data-stu-id="40532-140">string</span></span> | <span data-ttu-id="40532-141">Igen</span><span class="sxs-lookup"><span data-stu-id="40532-141">Yes</span></span>      | <span data-ttu-id="40532-142">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="40532-142">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="40532-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="40532-143">Request headers</span></span>

<span data-ttu-id="40532-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="40532-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="40532-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="40532-145">Request body</span></span>

<span data-ttu-id="40532-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="40532-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="40532-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="40532-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="40532-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="40532-148">REST response</span></span>

<span data-ttu-id="40532-149">Ha ez sikeres, a válasz törzse [SubscribedSku](license-resources.md#subscribedsku) -erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="40532-149">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="40532-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="40532-150">Response success and error codes</span></span>

<span data-ttu-id="40532-151">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="40532-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="40532-152">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="40532-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="40532-153">Teljes listát a következő témakörben talál: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="40532-153">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="40532-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="40532-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 4859
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CV: 7BQ0jitzXUCLwRM6.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 17:50:46 GMT

 {
    "totalCount": 2,
    "items": [{
            "availableUnits": 4,
            "activeUnits": 5,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 5,
            "warningUnits": 0,
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        },  {
            "availableUnits": 0,
            "activeUnits": 1,
            "consumedUnits": 1,
            "suspendedUnits": 0,
            "totalUnits": 1,
            "warningUnits": 0,
            "productSku": {
                "id": "f8a1db68-be16-40ed-86d5-cb42ce701560",
                "name": "Power BI Pro",
                "skuPartNumber": "POWER_BI_PRO",
                "targetType": "User",
                "licenseGroupId": "group1"
            },
            "servicePlans": [{
                    "displayName": "Exchange Foundation",
                    "serviceName": "EXCHANGE_S_FOUNDATION",
                    "id": "113feb6c-3fe4-4440-bddc-54d774bf0318",
                    "capabilityStatus": "Enabled",
                    "targetType": "Tenant"
                }, {
                    "displayName": "Power BI Pro",
                    "serviceName": "BI_AZURE_P2",
                    "id": "70d33638-9c74-4d01-bfd3-562de28bd4ba",
                    "capabilityStatus": "Enabled",
                    "targetType": "User"
                }
            ],
            "capabilityStatus": "Enabled",
            "attributes": {
                "objectType": "SubscribedSku"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
