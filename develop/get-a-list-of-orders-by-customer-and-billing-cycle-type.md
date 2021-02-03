---
title: A megrendelések listájának lekérése ügyfél és a számlázási ciklus típusa alapján
description: Lekérdezi az ügyfél és a számlázási ciklus megadott típusához tartozó rendelési erőforrások gyűjteményét.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 43fe08b0791851f915e2b39a25394db5ffd022ca
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768232"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="9a785-103">A megrendelések listájának lekérése ügyfél és a számlázási ciklus típusa alapján</span><span class="sxs-lookup"><span data-stu-id="9a785-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="9a785-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="9a785-104">**Applies to:**</span></span>

- <span data-ttu-id="9a785-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="9a785-105">Partner Center</span></span>
- <span data-ttu-id="9a785-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="9a785-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9a785-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="9a785-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9a785-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="9a785-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9a785-109">Lekérdezi a megrendelés erőforrásainak egy gyűjteményét, amely megfelel egy adott ügyfél-és számlázási ciklus típusának.</span><span class="sxs-lookup"><span data-stu-id="9a785-109">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="9a785-110">A megrendelés elküldése és az ügyfél rendeléseinek gyűjteménye között akár 15 percet is igénybe vehet.</span><span class="sxs-lookup"><span data-stu-id="9a785-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a785-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9a785-111">Prerequisites</span></span>

- <span data-ttu-id="9a785-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="9a785-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9a785-113">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="9a785-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9a785-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9a785-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9a785-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="9a785-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9a785-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="9a785-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9a785-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="9a785-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9a785-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="9a785-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9a785-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9a785-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9a785-120">C\#</span><span class="sxs-lookup"><span data-stu-id="9a785-120">C\#</span></span>

<span data-ttu-id="9a785-121">Ügyfél rendeléseinek gyűjteménye:</span><span class="sxs-lookup"><span data-stu-id="9a785-121">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="9a785-122">Használja a [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a kiválasztott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="9a785-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="9a785-123">Hívja meg a [**megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) tulajdonságot és a **ByBillingCycleType ()** metódust a megadott  [**BillingCycleType**](product-resources.md#billingcycletype).</span><span class="sxs-lookup"><span data-stu-id="9a785-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="9a785-124">Hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="9a785-124">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="9a785-125">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="9a785-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9a785-126">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="9a785-126">Request syntax</span></span>

| <span data-ttu-id="9a785-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="9a785-127">Method</span></span>  | <span data-ttu-id="9a785-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9a785-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a785-129">**GET**</span><span class="sxs-lookup"><span data-stu-id="9a785-129">**GET**</span></span> | <span data-ttu-id="9a785-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders? billingType = {számlázási-ciklus-típus} http/1.1</span><span class="sxs-lookup"><span data-stu-id="9a785-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="9a785-131">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="9a785-131">URI parameters</span></span>

<span data-ttu-id="9a785-132">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket, amelyekkel az ügyfél-azonosító és a számlázási ciklus típusa alapján kérheti le a megrendelések gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="9a785-132">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="9a785-133">Név</span><span class="sxs-lookup"><span data-stu-id="9a785-133">Name</span></span>                   | <span data-ttu-id="9a785-134">Típus</span><span class="sxs-lookup"><span data-stu-id="9a785-134">Type</span></span>     | <span data-ttu-id="9a785-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="9a785-135">Required</span></span> | <span data-ttu-id="9a785-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="9a785-136">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="9a785-137">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="9a785-137">customer-tenant-id</span></span>     | <span data-ttu-id="9a785-138">sztring</span><span class="sxs-lookup"><span data-stu-id="9a785-138">string</span></span>   | <span data-ttu-id="9a785-139">Igen</span><span class="sxs-lookup"><span data-stu-id="9a785-139">Yes</span></span>      | <span data-ttu-id="9a785-140">Az ügyfélhez tartozó GUID formátumú karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="9a785-140">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="9a785-141">számlázási ciklus – típus</span><span class="sxs-lookup"><span data-stu-id="9a785-141">billing-cycle-type</span></span>     | <span data-ttu-id="9a785-142">sztring</span><span class="sxs-lookup"><span data-stu-id="9a785-142">string</span></span>   | <span data-ttu-id="9a785-143">No</span><span class="sxs-lookup"><span data-stu-id="9a785-143">No</span></span>       | <span data-ttu-id="9a785-144">A számlázási ciklus típusának megfelelő karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="9a785-144">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="9a785-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9a785-145">Request headers</span></span>

<span data-ttu-id="9a785-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9a785-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9a785-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9a785-147">Request body</span></span>

<span data-ttu-id="9a785-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="9a785-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9a785-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9a785-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9a785-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9a785-150">REST response</span></span>

<span data-ttu-id="9a785-151">Ha ez sikeres, ez a metódus a [megrendelési](order-resources.md) erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="9a785-151">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9a785-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9a785-152">Response success and error codes</span></span>

<span data-ttu-id="9a785-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="9a785-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9a785-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="9a785-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9a785-155">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9a785-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9a785-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9a785-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 97fa8b4f-6576-4cd9-dd19-ac7c97a023a7
MS-RequestId: 3c6a034c-82ee-4095-d50f-9b530a415f1f
MS-CV: nb4/b3Yl2keY0eYR.0
MS-ServerId: 202010607
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Order"
            }
        },
        {
            "id": "s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4Z:002P:DZH318Z0CL2D",
                    "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_3_Years",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4Z/skus/002P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T01:42:36.8440279Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": { "objectType": "Order" }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType":
        "Collection"
    }
}
```
