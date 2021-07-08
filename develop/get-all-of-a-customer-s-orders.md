---
title: Egy ügyfél összes megrendelésének lekérése
description: Lekért egy adott ügyfél összes rendelésének gyűjteményét.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e8f23e90cbb5afb45e519e2c58fd0d3b9ea2de6a
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760300"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="79fd2-103">Egy ügyfél összes megrendelésének lekérése</span><span class="sxs-lookup"><span data-stu-id="79fd2-103">Get all of a customer's orders</span></span>

<span data-ttu-id="79fd2-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="79fd2-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="79fd2-105">Lekért egy adott ügyfél összes rendelésének gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="79fd2-105">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="79fd2-106">A rendelés beküldési ideje és az ügyfél rendelésgyűjteményében való megjelenése között akár 15 perces késés is lehet.</span><span class="sxs-lookup"><span data-stu-id="79fd2-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79fd2-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="79fd2-107">Prerequisites</span></span>

- <span data-ttu-id="79fd2-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="79fd2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="79fd2-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="79fd2-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="79fd2-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="79fd2-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="79fd2-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="79fd2-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="79fd2-112">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="79fd2-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="79fd2-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="79fd2-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="79fd2-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="79fd2-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="79fd2-115">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="79fd2-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="79fd2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="79fd2-116">C\#</span></span>

<span data-ttu-id="79fd2-117">Egy ügyfél összes rendelésének gyűjteményét a következővel szerezheti be:</span><span class="sxs-lookup"><span data-stu-id="79fd2-117">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="79fd2-118">Használja az [**IAggregatePartner.Customers gyűjteményt,**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) és hívja meg a [**ById() metódust.**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="79fd2-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="79fd2-119">Hívja meg [**az Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) tulajdonságot, majd a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) a [**GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="79fd2-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="79fd2-120">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="79fd2-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="79fd2-121">**Project**: PartnerSDK.FeatureSamples **osztály:** GetOrders.cs</span><span class="sxs-lookup"><span data-stu-id="79fd2-121">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="79fd2-122">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="79fd2-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="79fd2-123">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="79fd2-123">Request syntax</span></span>

| <span data-ttu-id="79fd2-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="79fd2-124">Method</span></span>  | <span data-ttu-id="79fd2-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="79fd2-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="79fd2-126">**Kap**</span><span class="sxs-lookup"><span data-stu-id="79fd2-126">**GET**</span></span> | <span data-ttu-id="79fd2-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="79fd2-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="79fd2-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="79fd2-128">URI parameter</span></span>

<span data-ttu-id="79fd2-129">Az alábbi lekérdezési paraméterrel lekérdezheti az összes rendelést.</span><span class="sxs-lookup"><span data-stu-id="79fd2-129">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="79fd2-130">Név</span><span class="sxs-lookup"><span data-stu-id="79fd2-130">Name</span></span>                   | <span data-ttu-id="79fd2-131">Típus</span><span class="sxs-lookup"><span data-stu-id="79fd2-131">Type</span></span>     | <span data-ttu-id="79fd2-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="79fd2-132">Required</span></span> | <span data-ttu-id="79fd2-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="79fd2-133">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="79fd2-134">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="79fd2-134">customer-tenant-id</span></span>     | <span data-ttu-id="79fd2-135">sztring</span><span class="sxs-lookup"><span data-stu-id="79fd2-135">string</span></span>   | <span data-ttu-id="79fd2-136">Igen</span><span class="sxs-lookup"><span data-stu-id="79fd2-136">Yes</span></span>      | <span data-ttu-id="79fd2-137">Az ügyfélnek megfelelő GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="79fd2-137">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="79fd2-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="79fd2-138">Request headers</span></span>

<span data-ttu-id="79fd2-139">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="79fd2-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="79fd2-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="79fd2-140">Request body</span></span>

<span data-ttu-id="79fd2-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="79fd2-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="79fd2-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="79fd2-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="79fd2-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="79fd2-143">REST response</span></span>

<span data-ttu-id="79fd2-144">Ha a művelet sikeres, ez a metódus az [Order](order-resources.md) erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="79fd2-144">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="79fd2-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="79fd2-145">Response success and error codes</span></span>

<span data-ttu-id="79fd2-146">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="79fd2-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="79fd2-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="79fd2-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="79fd2-148">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="79fd2-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="79fd2-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="79fd2-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
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
            "id": "eeba9d00-7b46-443a-917e-22887a8fc993",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "E59159FC-6F67-4599-B3CB-17FF4020F643",
                    "subscriptionId": "DB8C695B-1C3C-4C55-B697-771503DD46BF",
                    "friendlyName": "Azure Active Directory Premium P2",
                    "quantity": 1,
                    "links": {
                        "subscription": {
                            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/84A661C4-E949-4BD2-A560-ED7766FCAF2B/skus/E59159FC-6F67-4599-B3CB-17FF4020F643",
                            "method": "GET",
                            "headers": []
                        },
                        "provisioningStatus": {
                            "uri": "/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF/provisioningstatus",
                            "method": "GET",
                            "headers": []
                        }
                    }
            ],
            "creationDate": "2018-03-06T17:37:05.253-08:00",
            "status": "completed",
            "links": {
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/eeba9d00-7b46-443a-917e-22887a8fc993",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "etag": "eyJpZCI6ImVlYmE5ZDAwLTdiNDYtNDQzYS05MTdlLTIyODg3YThmYzk5MyIsInZlcnNpb24iOjF9",
                "objectType": "Order"
            }
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
         "objectType": "Collection"
    }
}
```
