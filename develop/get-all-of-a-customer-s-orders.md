---
title: Egy ügyfél összes megrendelésének lekérése
description: Egy adott ügyfélhez tartozó összes megrendelés gyűjteményének beolvasása.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4d71cd138421704d94a55a9fe21e074d92638815
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768359"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="edc22-103">Egy ügyfél összes megrendelésének lekérése</span><span class="sxs-lookup"><span data-stu-id="edc22-103">Get all of a customer's orders</span></span>

<span data-ttu-id="edc22-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="edc22-104">**Applies to:**</span></span>

- <span data-ttu-id="edc22-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="edc22-105">Partner Center</span></span>
- <span data-ttu-id="edc22-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="edc22-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="edc22-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="edc22-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="edc22-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="edc22-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="edc22-109">Egy adott ügyfélhez tartozó összes megrendelés gyűjteményének beolvasása.</span><span class="sxs-lookup"><span data-stu-id="edc22-109">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="edc22-110">A megrendelés elküldése és az ügyfél rendeléseinek gyűjteménye között akár 15 percet is igénybe vehet.</span><span class="sxs-lookup"><span data-stu-id="edc22-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edc22-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="edc22-111">Prerequisites</span></span>

- <span data-ttu-id="edc22-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="edc22-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="edc22-113">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="edc22-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="edc22-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="edc22-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="edc22-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="edc22-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="edc22-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="edc22-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="edc22-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="edc22-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="edc22-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="edc22-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="edc22-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="edc22-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="edc22-120">C\#</span><span class="sxs-lookup"><span data-stu-id="edc22-120">C\#</span></span>

<span data-ttu-id="edc22-121">Az ügyfél összes rendelése gyűjteményének beszerzése:</span><span class="sxs-lookup"><span data-stu-id="edc22-121">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="edc22-122">Használja a [**IAggregatePartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="edc22-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="edc22-123">Hívja meg a [**megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) tulajdonságot, majd a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="edc22-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="edc22-124">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="edc22-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="edc22-125">**Projekt**: PartnerSDK. FeatureSamples **osztály**: GetOrders.cs</span><span class="sxs-lookup"><span data-stu-id="edc22-125">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="edc22-126">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="edc22-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="edc22-127">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="edc22-127">Request syntax</span></span>

| <span data-ttu-id="edc22-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="edc22-128">Method</span></span>  | <span data-ttu-id="edc22-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="edc22-129">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="edc22-130">**GET**</span><span class="sxs-lookup"><span data-stu-id="edc22-130">**GET**</span></span> | <span data-ttu-id="edc22-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="edc22-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="edc22-132">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="edc22-132">URI parameter</span></span>

<span data-ttu-id="edc22-133">Az összes megrendelés beolvasásához használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="edc22-133">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="edc22-134">Név</span><span class="sxs-lookup"><span data-stu-id="edc22-134">Name</span></span>                   | <span data-ttu-id="edc22-135">Típus</span><span class="sxs-lookup"><span data-stu-id="edc22-135">Type</span></span>     | <span data-ttu-id="edc22-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="edc22-136">Required</span></span> | <span data-ttu-id="edc22-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="edc22-137">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="edc22-138">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="edc22-138">customer-tenant-id</span></span>     | <span data-ttu-id="edc22-139">sztring</span><span class="sxs-lookup"><span data-stu-id="edc22-139">string</span></span>   | <span data-ttu-id="edc22-140">Igen</span><span class="sxs-lookup"><span data-stu-id="edc22-140">Yes</span></span>      | <span data-ttu-id="edc22-141">Az ügyfélhez tartozó GUID formátumú karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="edc22-141">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="edc22-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="edc22-142">Request headers</span></span>

<span data-ttu-id="edc22-143">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="edc22-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="edc22-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="edc22-144">Request body</span></span>

<span data-ttu-id="edc22-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="edc22-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="edc22-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="edc22-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="edc22-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="edc22-147">REST response</span></span>

<span data-ttu-id="edc22-148">Ha ez sikeres, ez a metódus a [megrendelési](order-resources.md) erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="edc22-148">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="edc22-149">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="edc22-149">Response success and error codes</span></span>

<span data-ttu-id="edc22-150">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="edc22-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="edc22-151">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="edc22-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="edc22-152">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="edc22-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="edc22-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="edc22-153">Response example</span></span>

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
