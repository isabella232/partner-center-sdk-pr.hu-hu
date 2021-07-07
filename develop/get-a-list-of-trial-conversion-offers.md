---
title: A próbaverzió átalakításával kapcsolatos ajánlatok listájának lekérése
description: Próbaverziós konverziós ajánlatok listájának lekérése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 981910560faf7b7957b28e643c09a003826b9cff
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873921"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="b2808-103">A próbaverzió átalakításával kapcsolatos ajánlatok listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="b2808-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="b2808-104">Próbaverziós konverziós ajánlatok listájának lekérése.</span><span class="sxs-lookup"><span data-stu-id="b2808-104">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2808-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b2808-105">Prerequisites</span></span>

- <span data-ttu-id="b2808-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b2808-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b2808-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b2808-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b2808-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b2808-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b2808-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="b2808-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b2808-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b2808-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b2808-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="b2808-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b2808-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="b2808-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b2808-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b2808-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b2808-114">Egy aktív próba-előfizetés előfizetés-azonosítója.</span><span class="sxs-lookup"><span data-stu-id="b2808-114">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="b2808-115">C\#</span><span class="sxs-lookup"><span data-stu-id="b2808-115">C\#</span></span>

<span data-ttu-id="b2808-116">Az elérhető próbaverziós konverziók listájának lekérhetők az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódussal és az ügyfél azonosítójával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="b2808-116">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b2808-117">Ezután az előfizetési műveletek felületének lehívásához hívja meg a [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust a próba-előfizetés azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="b2808-117">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="b2808-118">Ezután a [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) tulajdonság használatával szerezzen be egy felületet az elérhető konverziós műveletekhez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust az elérhető konverziós ajánlatok [**gyűjteményének lekéréséhez.**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion)</span><span class="sxs-lookup"><span data-stu-id="b2808-118">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="b2808-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="b2808-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b2808-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b2808-120">Request syntax</span></span>

| <span data-ttu-id="b2808-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="b2808-121">Method</span></span>  | <span data-ttu-id="b2808-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b2808-122">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b2808-123">**Kap**</span><span class="sxs-lookup"><span data-stu-id="b2808-123">**GET**</span></span> | <span data-ttu-id="b2808-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/subscriptions/{előfizetés-azonosító}/conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b2808-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b2808-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b2808-125">URI parameter</span></span>

<span data-ttu-id="b2808-126">Az ügyfél és a próbaverziós előfizetés azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="b2808-126">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="b2808-127">Név</span><span class="sxs-lookup"><span data-stu-id="b2808-127">Name</span></span>            | <span data-ttu-id="b2808-128">Típus</span><span class="sxs-lookup"><span data-stu-id="b2808-128">Type</span></span>   | <span data-ttu-id="b2808-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b2808-129">Required</span></span> | <span data-ttu-id="b2808-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="b2808-130">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="b2808-131">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="b2808-131">customer-id</span></span>     | <span data-ttu-id="b2808-132">sztring</span><span class="sxs-lookup"><span data-stu-id="b2808-132">string</span></span> | <span data-ttu-id="b2808-133">Igen</span><span class="sxs-lookup"><span data-stu-id="b2808-133">Yes</span></span>      | <span data-ttu-id="b2808-134">Egy GUID formátumú sztring, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="b2808-134">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="b2808-135">subscription-id (előfizetés-azonosító)</span><span class="sxs-lookup"><span data-stu-id="b2808-135">subscription-id</span></span> | <span data-ttu-id="b2808-136">sztring</span><span class="sxs-lookup"><span data-stu-id="b2808-136">string</span></span> | <span data-ttu-id="b2808-137">Igen</span><span class="sxs-lookup"><span data-stu-id="b2808-137">Yes</span></span>      | <span data-ttu-id="b2808-138">A próba-előfizetést azonosító GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="b2808-138">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b2808-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b2808-139">Request headers</span></span>

<span data-ttu-id="b2808-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b2808-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b2808-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b2808-141">Request body</span></span>

<span data-ttu-id="b2808-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b2808-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b2808-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b2808-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="b2808-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b2808-144">REST response</span></span>

<span data-ttu-id="b2808-145">Ha a művelet sikeres, a válasz törzse konverziós erőforrások [gyűjteményét](conversions-resources.md#conversionresult) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b2808-145">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b2808-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b2808-146">Response success and error codes</span></span>

<span data-ttu-id="b2808-147">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="b2808-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b2808-148">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="b2808-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b2808-149">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b2808-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b2808-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b2808-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

 {
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
