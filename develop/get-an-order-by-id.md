---
title: Megrendelés lekérése azonosító alapján
description: Lekért egy rendelési erőforrást, amely megfelel az ügyfél és a rendelés azonosítójának.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2cb2822935113fe1c5337b4ffc899fccff333d2f
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760181"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="6ce15-103">Megrendelés lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="6ce15-103">Get an order by ID</span></span>

<span data-ttu-id="6ce15-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6ce15-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6ce15-105">Lekért [egy rendelési](order-resources.md) erőforrást, amely megfelel az ügyfél és a rendelés azonosítójának.</span><span class="sxs-lookup"><span data-stu-id="6ce15-105">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ce15-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6ce15-106">Prerequisites</span></span>

- <span data-ttu-id="6ce15-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6ce15-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6ce15-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="6ce15-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6ce15-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6ce15-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6ce15-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6ce15-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6ce15-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6ce15-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6ce15-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="6ce15-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6ce15-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="6ce15-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6ce15-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6ce15-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6ce15-115">Egy rendelésazonosító.</span><span class="sxs-lookup"><span data-stu-id="6ce15-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="6ce15-116">C\#</span><span class="sxs-lookup"><span data-stu-id="6ce15-116">C\#</span></span>

<span data-ttu-id="6ce15-117">Az ügyfél megrendelésének lekért azonosítója:</span><span class="sxs-lookup"><span data-stu-id="6ce15-117">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="6ce15-118">Használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="6ce15-118">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="6ce15-119">Hívja meg [**ismét az Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) tulajdonságot, majd a [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="6ce15-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="6ce15-120">Hívja meg a [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) vagy [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync)</span><span class="sxs-lookup"><span data-stu-id="6ce15-120">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="6ce15-121">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6ce15-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6ce15-122">**Project:** PartnerSDK.FeatureSample **osztály:** GetOrder.cs</span><span class="sxs-lookup"><span data-stu-id="6ce15-122">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="6ce15-123">Java</span><span class="sxs-lookup"><span data-stu-id="6ce15-123">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="6ce15-124">Az ügyfél megrendelésének lekért azonosítója:</span><span class="sxs-lookup"><span data-stu-id="6ce15-124">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="6ce15-125">Használja az **IAggregatePartner.getCustomers** függvényt, és hívja meg a **byId()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="6ce15-125">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="6ce15-126">Hívja meg ismét a **getOrders** függvényt, majd a **byID()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="6ce15-126">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="6ce15-127">Hívja meg a **get()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="6ce15-127">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="6ce15-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ce15-128">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="6ce15-129">Ha azonosító alapján le kell szereznie egy ügyfél megrendelését, hajtsa végre a [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) parancsot, és adja meg a **CustomerId** és **az OrderId** paramétereket.</span><span class="sxs-lookup"><span data-stu-id="6ce15-129">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="6ce15-130">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="6ce15-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6ce15-131">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="6ce15-131">Request syntax</span></span>

| <span data-ttu-id="6ce15-132">Metódus</span><span class="sxs-lookup"><span data-stu-id="6ce15-132">Method</span></span>  | <span data-ttu-id="6ce15-133">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6ce15-133">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6ce15-134">**Kap**</span><span class="sxs-lookup"><span data-stu-id="6ce15-134">**GET**</span></span> | <span data-ttu-id="6ce15-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6ce15-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="6ce15-136">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="6ce15-136">URI parameters</span></span>

<span data-ttu-id="6ce15-137">Ez a táblázat a rendelés azonosító alapján való lekérdezéséhez szükséges lekérdezési paramétereket sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="6ce15-137">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="6ce15-138">Név</span><span class="sxs-lookup"><span data-stu-id="6ce15-138">Name</span></span>                   | <span data-ttu-id="6ce15-139">Típus</span><span class="sxs-lookup"><span data-stu-id="6ce15-139">Type</span></span>     | <span data-ttu-id="6ce15-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6ce15-140">Required</span></span> | <span data-ttu-id="6ce15-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="6ce15-141">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="6ce15-142">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="6ce15-142">customer-tenant-id</span></span>     | <span data-ttu-id="6ce15-143">sztring</span><span class="sxs-lookup"><span data-stu-id="6ce15-143">string</span></span>   | <span data-ttu-id="6ce15-144">Igen</span><span class="sxs-lookup"><span data-stu-id="6ce15-144">Yes</span></span>      | <span data-ttu-id="6ce15-145">Az ügyfélnek megfelelő GUID formátumú sztring.</span><span class="sxs-lookup"><span data-stu-id="6ce15-145">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="6ce15-146">id-for-order</span><span class="sxs-lookup"><span data-stu-id="6ce15-146">id-for-order</span></span>           | <span data-ttu-id="6ce15-147">sztring</span><span class="sxs-lookup"><span data-stu-id="6ce15-147">string</span></span>   | <span data-ttu-id="6ce15-148">Igen</span><span class="sxs-lookup"><span data-stu-id="6ce15-148">Yes</span></span>      | <span data-ttu-id="6ce15-149">A rendelésazonosítónak megfelelő sztring.</span><span class="sxs-lookup"><span data-stu-id="6ce15-149">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="6ce15-150">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6ce15-150">Request headers</span></span>

<span data-ttu-id="6ce15-151">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6ce15-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6ce15-152">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6ce15-152">Request body</span></span>

<span data-ttu-id="6ce15-153">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="6ce15-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6ce15-154">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6ce15-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="6ce15-155">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6ce15-155">REST response</span></span>

<span data-ttu-id="6ce15-156">Ha sikeres, ez a metódus egy [Order](order-resources.md) erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="6ce15-156">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6ce15-157">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6ce15-157">Response success and error codes</span></span>

<span data-ttu-id="6ce15-158">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="6ce15-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6ce15-159">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="6ce15-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6ce15-160">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6ce15-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6ce15-161">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6ce15-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
