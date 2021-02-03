---
title: A próbaverzió átalakításával kapcsolatos ajánlatok listájának lekérése
description: Próbaverziós konvertálási ajánlatok listájának beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e1eadecde9efa0b59fc7790bd474889bb32821dc
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768235"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="3929f-103">A próbaverzió átalakításával kapcsolatos ajánlatok listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="3929f-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="3929f-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="3929f-104">**Applies To**</span></span>

- <span data-ttu-id="3929f-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3929f-105">Partner Center</span></span>

<span data-ttu-id="3929f-106">Próbaverziós konvertálási ajánlatok listájának beolvasása.</span><span class="sxs-lookup"><span data-stu-id="3929f-106">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3929f-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3929f-107">Prerequisites</span></span>

- <span data-ttu-id="3929f-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="3929f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3929f-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="3929f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3929f-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3929f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3929f-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="3929f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3929f-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="3929f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3929f-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="3929f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3929f-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="3929f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3929f-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3929f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3929f-116">Egy aktív próbaverziós előfizetés előfizetési azonosítója.</span><span class="sxs-lookup"><span data-stu-id="3929f-116">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="3929f-117">C\#</span><span class="sxs-lookup"><span data-stu-id="3929f-117">C\#</span></span>

<span data-ttu-id="3929f-118">A próbaverziós konverziók listájának lekéréséhez először használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="3929f-118">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="3929f-119">Ezután kérjen meg egy illesztőfelületet az előfizetési műveletekhez az [**előfizetések. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódus meghívásával a próbaverziós előfizetés azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="3929f-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="3929f-120">Ezután az [**átalakítások**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) [**tulajdonsággal**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) szerezzen be egy felületet az elérhető műveletekhez a konverziók között, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) metódust a rendelkezésre álló konverziós ajánlatok gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="3929f-120">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="3929f-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="3929f-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3929f-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3929f-122">Request syntax</span></span>

| <span data-ttu-id="3929f-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="3929f-123">Method</span></span>  | <span data-ttu-id="3929f-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3929f-124">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3929f-125">**GET**</span><span class="sxs-lookup"><span data-stu-id="3929f-125">**GET**</span></span> | <span data-ttu-id="3929f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Subscriptions/{Subscription-ID}/Conversions http/1.1</span><span class="sxs-lookup"><span data-stu-id="3929f-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3929f-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="3929f-127">URI parameter</span></span>

<span data-ttu-id="3929f-128">Az ügyfél és a próbaverzió előfizetésének azonosításához használja a következő elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="3929f-128">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="3929f-129">Név</span><span class="sxs-lookup"><span data-stu-id="3929f-129">Name</span></span>            | <span data-ttu-id="3929f-130">Típus</span><span class="sxs-lookup"><span data-stu-id="3929f-130">Type</span></span>   | <span data-ttu-id="3929f-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3929f-131">Required</span></span> | <span data-ttu-id="3929f-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="3929f-132">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="3929f-133">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="3929f-133">customer-id</span></span>     | <span data-ttu-id="3929f-134">sztring</span><span class="sxs-lookup"><span data-stu-id="3929f-134">string</span></span> | <span data-ttu-id="3929f-135">Igen</span><span class="sxs-lookup"><span data-stu-id="3929f-135">Yes</span></span>      | <span data-ttu-id="3929f-136">Egy GUID formátumú karakterlánc, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="3929f-136">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="3929f-137">előfizetés-azonosító</span><span class="sxs-lookup"><span data-stu-id="3929f-137">subscription-id</span></span> | <span data-ttu-id="3929f-138">sztring</span><span class="sxs-lookup"><span data-stu-id="3929f-138">string</span></span> | <span data-ttu-id="3929f-139">Igen</span><span class="sxs-lookup"><span data-stu-id="3929f-139">Yes</span></span>      | <span data-ttu-id="3929f-140">Egy GUID formátumú karakterlánc, amely azonosítja a próba-előfizetést.</span><span class="sxs-lookup"><span data-stu-id="3929f-140">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3929f-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3929f-141">Request headers</span></span>

<span data-ttu-id="3929f-142">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3929f-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3929f-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3929f-143">Request body</span></span>

<span data-ttu-id="3929f-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="3929f-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3929f-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3929f-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3929f-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3929f-146">REST response</span></span>

<span data-ttu-id="3929f-147">Ha ez sikeres, a válasz törzse [konverziós](conversions-resources.md#conversionresult) erőforrások gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3929f-147">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3929f-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3929f-148">Response success and error codes</span></span>

<span data-ttu-id="3929f-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="3929f-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3929f-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="3929f-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3929f-151">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3929f-151">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3929f-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="3929f-152">Response example</span></span>

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
