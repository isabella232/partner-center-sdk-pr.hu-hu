---
title: A rendelkezésre álló licencek listájának lekérése
description: A megadott ügyfél felhasználói számára elérhető licencek listájának lekért listája.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 02a6fccc2cf7f3f4dc929b96ec0f17e0f4a31b06
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874499"
---
# <a name="get-a-list-of-available-licenses"></a><span data-ttu-id="f76cd-103">A rendelkezésre álló licencek listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="f76cd-103">Get a list of available licenses</span></span>

<span data-ttu-id="f76cd-104">Ez a cikk azt ismerteti, hogyan lehet lekérhetők a megadott ügyfél felhasználói számára elérhető licencek.</span><span class="sxs-lookup"><span data-stu-id="f76cd-104">This article describes how to get a list of licenses available to users of the specified customer.</span></span>

<span data-ttu-id="f76cd-105">Az alábbi példák az **1.** csoportban elérhető licenceket adja vissza, az alapértelmezett licenccsoportot, amely a Azure Active Directory (Azure AD) által kezelt licenceket jelöli.</span><span class="sxs-lookup"><span data-stu-id="f76cd-105">The following examples return licenses available from **group1**, the default license group that represents licenses managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f76cd-106">Egy adott licenccsoporthoz elérhető licencek lekért listáját lásd: Az elérhető licencek listájának lekérhetők [licenccsoport szerint.](get-a-list-of-available-licenses-by-license-group.md)</span><span class="sxs-lookup"><span data-stu-id="f76cd-106">To get available licenses for a specified license group, see [Get a list of available licenses by license group](get-a-list-of-available-licenses-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f76cd-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f76cd-107">Prerequisites</span></span>

- <span data-ttu-id="f76cd-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f76cd-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f76cd-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="f76cd-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f76cd-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f76cd-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f76cd-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="f76cd-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f76cd-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f76cd-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f76cd-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f76cd-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f76cd-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="f76cd-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f76cd-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f76cd-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f76cd-116">C\#</span><span class="sxs-lookup"><span data-stu-id="f76cd-116">C\#</span></span>

<span data-ttu-id="f76cd-117">Az ügyfél felhasználói számára az alapértelmezett licenccsoportból elérhető licencek listájának lekérése:</span><span class="sxs-lookup"><span data-stu-id="f76cd-117">To retrieve the list of licenses available from the default license group to users of a customer:</span></span>

1. <span data-ttu-id="f76cd-118">Az [**ügyfél azonosításához használja az IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="f76cd-118">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="f76cd-119">A [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) tulajdonság értékének lekérésével lekérhet egy felületet az ügyfél által előfizetett termékváltozat-gyűjtési műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="f76cd-119">Get the value of the [**SubscribedSkus**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscribedskus) property to retrieve an interface to customer subscribed SKU collection operations.</span></span>

3. <span data-ttu-id="f76cd-120">A [**licencek listájának**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) lekéréshez hívja meg a Get vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="f76cd-120">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to retrieve the list of licenses.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
```

<span data-ttu-id="f76cd-121">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="f76cd-121">For an example, see the following:</span></span>

- <span data-ttu-id="f76cd-122">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f76cd-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f76cd-123">Project: **Partnerközpont SDK minták**</span><span class="sxs-lookup"><span data-stu-id="f76cd-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="f76cd-124">Osztály: **GetCustomerSubscribedSkus.cs**</span><span class="sxs-lookup"><span data-stu-id="f76cd-124">Class: **GetCustomerSubscribedSkus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f76cd-125">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="f76cd-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f76cd-126">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f76cd-126">Request syntax</span></span>

| <span data-ttu-id="f76cd-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="f76cd-127">Method</span></span>  | <span data-ttu-id="f76cd-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f76cd-128">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f76cd-129">**Kap**</span><span class="sxs-lookup"><span data-stu-id="f76cd-129">**GET**</span></span> | <span data-ttu-id="f76cd-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscribedskus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f76cd-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscribedskus HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="f76cd-131">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f76cd-131">URI parameter</span></span>

<span data-ttu-id="f76cd-132">Az ügyfél azonosításához használja a következő path paramétert.</span><span class="sxs-lookup"><span data-stu-id="f76cd-132">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="f76cd-133">Név</span><span class="sxs-lookup"><span data-stu-id="f76cd-133">Name</span></span>        | <span data-ttu-id="f76cd-134">Típus</span><span class="sxs-lookup"><span data-stu-id="f76cd-134">Type</span></span>   | <span data-ttu-id="f76cd-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f76cd-135">Required</span></span> | <span data-ttu-id="f76cd-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="f76cd-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="f76cd-137">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="f76cd-137">customer-id</span></span> | <span data-ttu-id="f76cd-138">sztring</span><span class="sxs-lookup"><span data-stu-id="f76cd-138">string</span></span> | <span data-ttu-id="f76cd-139">Igen</span><span class="sxs-lookup"><span data-stu-id="f76cd-139">Yes</span></span>      | <span data-ttu-id="f76cd-140">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="f76cd-140">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f76cd-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f76cd-141">Request headers</span></span>

<span data-ttu-id="f76cd-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f76cd-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f76cd-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f76cd-143">Request body</span></span>

<span data-ttu-id="f76cd-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f76cd-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f76cd-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f76cd-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscribedskus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53308f82-1bf7-44e2-8dda-4517e4688bd4
MS-CorrelationId: 95660db2-7425-4021-babe-a26ddbcb0187
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f76cd-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f76cd-146">REST response</span></span>

<span data-ttu-id="f76cd-147">Ha a művelet sikeres, a válasz törzse a [SubscribedSku](license-resources.md#subscribedsku) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="f76cd-147">If successful, the response body contains a collection of [SubscribedSku](license-resources.md#subscribedsku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f76cd-148">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f76cd-148">Response success and error codes</span></span>

<span data-ttu-id="f76cd-149">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="f76cd-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f76cd-150">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="f76cd-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f76cd-151">A teljes listát a REST Partnerközpont [hibakódokat.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f76cd-151">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f76cd-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f76cd-152">Response example</span></span>

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
