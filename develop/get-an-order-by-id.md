---
title: Megrendelés lekérése azonosító alapján
description: Lekéri az ügyfél és a megrendelés AZONOSÍTÓjának megfelelő rendelési erőforrást.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 0a39d7142e5bf97f9fb345416964d4ed6bb935ad
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768455"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="2c903-103">Megrendelés lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="2c903-103">Get an order by ID</span></span>

<span data-ttu-id="2c903-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="2c903-104">**Applies to:**</span></span>

- <span data-ttu-id="2c903-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="2c903-105">Partner Center</span></span>
- <span data-ttu-id="2c903-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="2c903-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2c903-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2c903-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2c903-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2c903-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2c903-109">Lekéri az ügyfél és a megrendelés AZONOSÍTÓjának megfelelő [rendelési](order-resources.md) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="2c903-109">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c903-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2c903-110">Prerequisites</span></span>

- <span data-ttu-id="2c903-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="2c903-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2c903-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="2c903-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2c903-113">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2c903-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2c903-114">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2c903-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2c903-115">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="2c903-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2c903-116">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="2c903-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2c903-117">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="2c903-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2c903-118">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2c903-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2c903-119">Egy megrendelés azonosítója.</span><span class="sxs-lookup"><span data-stu-id="2c903-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="2c903-120">C\#</span><span class="sxs-lookup"><span data-stu-id="2c903-120">C\#</span></span>

<span data-ttu-id="2c903-121">Ügyfél rendelésének beszerzése azonosító alapján:</span><span class="sxs-lookup"><span data-stu-id="2c903-121">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="2c903-122">Használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="2c903-122">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="2c903-123">Hívja meg az [**orders (megrendelések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) ) tulajdonságot, majd a [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="2c903-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="2c903-124">A [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync)hívása.</span><span class="sxs-lookup"><span data-stu-id="2c903-124">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="2c903-125">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2c903-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2c903-126">**Projekt**: PartnerSDK. FeatureSample **osztály**: GetOrder.cs</span><span class="sxs-lookup"><span data-stu-id="2c903-126">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="2c903-127">Java</span><span class="sxs-lookup"><span data-stu-id="2c903-127">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="2c903-128">Ügyfél rendelésének beszerzése azonosító alapján:</span><span class="sxs-lookup"><span data-stu-id="2c903-128">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="2c903-129">Használja a **IAggregatePartner. getCustomers** függvényt, és hívja meg a **byId ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="2c903-129">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="2c903-130">Hívja meg a **getOrders** függvényt, majd a **byID ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="2c903-130">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="2c903-131">Hívja meg a **Get ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="2c903-131">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="2c903-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c903-132">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="2c903-133">Az ügyfél Order by ID azonosítójának lekéréséhez futtassa a [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) parancsot, és határozza meg a **Vevőkód** és a **Rendeléskód** paramétereket.</span><span class="sxs-lookup"><span data-stu-id="2c903-133">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="2c903-134">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="2c903-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2c903-135">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2c903-135">Request syntax</span></span>

| <span data-ttu-id="2c903-136">Metódus</span><span class="sxs-lookup"><span data-stu-id="2c903-136">Method</span></span>  | <span data-ttu-id="2c903-137">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2c903-137">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2c903-138">**GET**</span><span class="sxs-lookup"><span data-stu-id="2c903-138">**GET**</span></span> | <span data-ttu-id="2c903-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders/{ID-for-Order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2c903-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="2c903-140">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="2c903-140">URI parameters</span></span>

<span data-ttu-id="2c903-141">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket, amelyek alapján a rendelést azonosító alapján lehet beolvasni.</span><span class="sxs-lookup"><span data-stu-id="2c903-141">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="2c903-142">Név</span><span class="sxs-lookup"><span data-stu-id="2c903-142">Name</span></span>                   | <span data-ttu-id="2c903-143">Típus</span><span class="sxs-lookup"><span data-stu-id="2c903-143">Type</span></span>     | <span data-ttu-id="2c903-144">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2c903-144">Required</span></span> | <span data-ttu-id="2c903-145">Leírás</span><span class="sxs-lookup"><span data-stu-id="2c903-145">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="2c903-146">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="2c903-146">customer-tenant-id</span></span>     | <span data-ttu-id="2c903-147">sztring</span><span class="sxs-lookup"><span data-stu-id="2c903-147">string</span></span>   | <span data-ttu-id="2c903-148">Igen</span><span class="sxs-lookup"><span data-stu-id="2c903-148">Yes</span></span>      | <span data-ttu-id="2c903-149">Az ügyfélhez tartozó GUID formátumú karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="2c903-149">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="2c903-150">azonosító – sorrend</span><span class="sxs-lookup"><span data-stu-id="2c903-150">id-for-order</span></span>           | <span data-ttu-id="2c903-151">sztring</span><span class="sxs-lookup"><span data-stu-id="2c903-151">string</span></span>   | <span data-ttu-id="2c903-152">Igen</span><span class="sxs-lookup"><span data-stu-id="2c903-152">Yes</span></span>      | <span data-ttu-id="2c903-153">A megrendelés AZONOSÍTÓjának megfelelő karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="2c903-153">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="2c903-154">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2c903-154">Request headers</span></span>

<span data-ttu-id="2c903-155">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2c903-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2c903-156">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2c903-156">Request body</span></span>

<span data-ttu-id="2c903-157">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="2c903-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2c903-158">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2c903-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="2c903-159">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2c903-159">REST response</span></span>

<span data-ttu-id="2c903-160">Ha ez sikeres, ez a metódus egy [Order](order-resources.md) erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="2c903-160">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2c903-161">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2c903-161">Response success and error codes</span></span>

<span data-ttu-id="2c903-162">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="2c903-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2c903-163">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="2c903-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2c903-164">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2c903-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2c903-165">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2c903-165">Response example</span></span>

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
