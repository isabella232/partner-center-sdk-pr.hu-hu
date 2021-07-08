---
title: A megrendelések listájának lekérése ügyfél és a számlázási ciklus típusa alapján
description: Lekérte a megadott ügyfél- és számlázási ciklustípus megrendelési erőforrásainak gyűjteményét.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c52a556887dba065c4ccd1a82d6223624d0ad1f2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874227"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="7b081-103">A megrendelések listájának lekérése ügyfél és a számlázási ciklus típusa alapján</span><span class="sxs-lookup"><span data-stu-id="7b081-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="7b081-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7b081-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7b081-105">Lekért rendelési erőforrások egy adott ügyfél- és számlázási ciklustípusnak megfelelő gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="7b081-105">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="7b081-106">A rendelés beküldési ideje és az ügyfél rendelésgyűjteményében való megjelenése között akár 15 perces késés is lehet.</span><span class="sxs-lookup"><span data-stu-id="7b081-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b081-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7b081-107">Prerequisites</span></span>

- <span data-ttu-id="7b081-108">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7b081-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7b081-109">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="7b081-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7b081-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7b081-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7b081-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="7b081-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7b081-112">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="7b081-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7b081-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="7b081-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7b081-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="7b081-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7b081-115">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7b081-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7b081-116">C\#</span><span class="sxs-lookup"><span data-stu-id="7b081-116">C\#</span></span>

<span data-ttu-id="7b081-117">Ügyfélrendelések gyűjteményének lekért száma:</span><span class="sxs-lookup"><span data-stu-id="7b081-117">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="7b081-118">Használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a kiválasztott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="7b081-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="7b081-119">Hívja meg [**az Orders tulajdonságot**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) és a **ByBillingCycleType() metódust** a megadott [**BillingCycleType típussal.**](product-resources.md#billingcycletype)</span><span class="sxs-lookup"><span data-stu-id="7b081-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="7b081-120">Hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="7b081-120">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="7b081-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="7b081-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7b081-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7b081-122">Request syntax</span></span>

| <span data-ttu-id="7b081-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="7b081-123">Method</span></span>  | <span data-ttu-id="7b081-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7b081-124">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b081-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7b081-125">**GET**</span></span> | <span data-ttu-id="7b081-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7b081-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="7b081-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7b081-127">URI parameters</span></span>

<span data-ttu-id="7b081-128">Ez a táblázat a megrendelések gyűjteményének az ügyfélazonosító és a számlázási ciklus típusa alapján való lekérdezhető lekérdezési paramétereit sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="7b081-128">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="7b081-129">Név</span><span class="sxs-lookup"><span data-stu-id="7b081-129">Name</span></span>                   | <span data-ttu-id="7b081-130">Típus</span><span class="sxs-lookup"><span data-stu-id="7b081-130">Type</span></span>     | <span data-ttu-id="7b081-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7b081-131">Required</span></span> | <span data-ttu-id="7b081-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="7b081-132">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="7b081-133">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="7b081-133">customer-tenant-id</span></span>     | <span data-ttu-id="7b081-134">sztring</span><span class="sxs-lookup"><span data-stu-id="7b081-134">string</span></span>   | <span data-ttu-id="7b081-135">Igen</span><span class="sxs-lookup"><span data-stu-id="7b081-135">Yes</span></span>      | <span data-ttu-id="7b081-136">Az ügyfélnek megfelelő GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="7b081-136">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="7b081-137">számlázási ciklus típusa</span><span class="sxs-lookup"><span data-stu-id="7b081-137">billing-cycle-type</span></span>     | <span data-ttu-id="7b081-138">sztring</span><span class="sxs-lookup"><span data-stu-id="7b081-138">string</span></span>   | <span data-ttu-id="7b081-139">No</span><span class="sxs-lookup"><span data-stu-id="7b081-139">No</span></span>       | <span data-ttu-id="7b081-140">A számlázási ciklus típusának megfelelő sztring.</span><span class="sxs-lookup"><span data-stu-id="7b081-140">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="7b081-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7b081-141">Request headers</span></span>

<span data-ttu-id="7b081-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7b081-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7b081-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7b081-143">Request body</span></span>

<span data-ttu-id="7b081-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7b081-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7b081-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7b081-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="7b081-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7b081-146">REST response</span></span>

<span data-ttu-id="7b081-147">Ha a művelet sikeres, ez a metódus az Order erőforrások [gyűjteményét](order-resources.md) adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="7b081-147">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7b081-148">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7b081-148">Response success and error codes</span></span>

<span data-ttu-id="7b081-149">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="7b081-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7b081-150">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="7b081-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7b081-151">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7b081-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7b081-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7b081-152">Response example</span></span>

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
