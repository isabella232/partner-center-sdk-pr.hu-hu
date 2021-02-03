---
title: Kosár tartalmának kifizetése
description: Megtudhatja, hogyan tekintheti meg egy ügyfél rendelését egy kosárban a partner Center API-k használatával. Ezt megteheti az ügyfél megrendelésének befejezéséhez.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 094817a34cd29bc96788fcfb6a16610a8192d784
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768595"
---
# <a name="checkout-an-order-for-a-customer-in-a-cart"></a><span data-ttu-id="28508-104">Megrendelés megrendelése egy kosárban lévő ügyfél számára</span><span class="sxs-lookup"><span data-stu-id="28508-104">Checkout an order for a customer in a cart</span></span>

<span data-ttu-id="28508-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="28508-105">**Applies to:**</span></span>

- <span data-ttu-id="28508-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="28508-106">Partner Center</span></span>
- <span data-ttu-id="28508-107">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="28508-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="28508-108">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="28508-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="28508-109">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="28508-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="28508-110">Megrendelés megrendelése az ügyfelek számára a kosárban.</span><span class="sxs-lookup"><span data-stu-id="28508-110">How to checkout an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28508-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="28508-111">Prerequisites</span></span>

- <span data-ttu-id="28508-112">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="28508-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="28508-113">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="28508-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="28508-114">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="28508-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="28508-115">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="28508-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="28508-116">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="28508-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="28508-117">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="28508-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="28508-118">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="28508-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="28508-119">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="28508-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="28508-120">Egy meglévő kosárhoz tartozó kosár-azonosító.</span><span class="sxs-lookup"><span data-stu-id="28508-120">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="28508-121">C\#</span><span class="sxs-lookup"><span data-stu-id="28508-121">C\#</span></span>

<span data-ttu-id="28508-122">Egy ügyfél rendelésének kifizetéséhez a kosár és az ügyfél-azonosító használatával szerezzen be egy hivatkozást a kosárra.</span><span class="sxs-lookup"><span data-stu-id="28508-122">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="28508-123">Végül hívja meg a **create** vagy a **CreateAsync** függvényt a megrendelés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="28508-123">Finally, call the **Create** or **CreateAsync** functions to complete the order.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Checkout();
```

## <a name="java"></a><span data-ttu-id="28508-124">Java</span><span class="sxs-lookup"><span data-stu-id="28508-124">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="28508-125">Egy ügyfél rendelésének kifizetéséhez a kosár és az ügyfél-azonosító használatával szerezzen be egy hivatkozást a kosárra.</span><span class="sxs-lookup"><span data-stu-id="28508-125">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="28508-126">Végül hívja meg a **create** függvényt a megrendelés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="28508-126">Finally, call the **create** function to complete the order.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String cartId;

Cart cart = partnerOperations.getCustomers().byId(customerId).getCart().byId(cartId).checkout();
```

## <a name="powershell"></a><span data-ttu-id="28508-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="28508-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="28508-128">Egy ügyfél rendelésének kifizetéséhez hajtsa végre a [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) a rendelés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="28508-128">To checkout an order for a customer, execute the [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) to complete the order.</span></span>

```powershell
# $customerId
# $cartId

Submit-PartnerCustomerCart -CartId $cartId -CustomerId $customerId
```

## <a name="rest-request"></a><span data-ttu-id="28508-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="28508-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="28508-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="28508-130">Request syntax</span></span>

| <span data-ttu-id="28508-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="28508-131">Method</span></span>   | <span data-ttu-id="28508-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="28508-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="28508-133">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="28508-133">**POST**</span></span> | <span data-ttu-id="28508-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/carts/{cart-ID}/Checkout http/1.1</span><span class="sxs-lookup"><span data-stu-id="28508-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="28508-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="28508-135">URI parameters</span></span>

<span data-ttu-id="28508-136">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet, és megadhatja a kivenni kívánt szekéret.</span><span class="sxs-lookup"><span data-stu-id="28508-136">Use the following path parameters to identify the customer and specify the cart to be checked out.</span></span>

| <span data-ttu-id="28508-137">Név</span><span class="sxs-lookup"><span data-stu-id="28508-137">Name</span></span>            | <span data-ttu-id="28508-138">Típus</span><span class="sxs-lookup"><span data-stu-id="28508-138">Type</span></span>     | <span data-ttu-id="28508-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="28508-139">Required</span></span> | <span data-ttu-id="28508-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="28508-140">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="28508-141">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="28508-141">**customer-id**</span></span> | <span data-ttu-id="28508-142">sztring</span><span class="sxs-lookup"><span data-stu-id="28508-142">string</span></span>   | <span data-ttu-id="28508-143">Igen</span><span class="sxs-lookup"><span data-stu-id="28508-143">Yes</span></span>      | <span data-ttu-id="28508-144">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="28508-144">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="28508-145">**kosár-azonosító**</span><span class="sxs-lookup"><span data-stu-id="28508-145">**cart-id**</span></span>     | <span data-ttu-id="28508-146">sztring</span><span class="sxs-lookup"><span data-stu-id="28508-146">string</span></span>   | <span data-ttu-id="28508-147">Igen</span><span class="sxs-lookup"><span data-stu-id="28508-147">Yes</span></span>      | <span data-ttu-id="28508-148">A szekér azonosítására szolgáló GUID formátumú kosár-azonosító.</span><span class="sxs-lookup"><span data-stu-id="28508-148">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="28508-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="28508-149">Request headers</span></span>

<span data-ttu-id="28508-150">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="28508-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="28508-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="28508-151">Request body</span></span>

<span data-ttu-id="28508-152">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="28508-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="28508-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="28508-153">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/checkout HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
Expect: 100-continue

No-Content-Body
```

## <a name="rest-response"></a><span data-ttu-id="28508-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="28508-154">REST response</span></span>

<span data-ttu-id="28508-155">Ha a művelet sikeres, a válasz törzse tartalmazza a feltöltött [CartCheckoutResult](cart-resources.md#cartcheckoutresult) -erőforrást.</span><span class="sxs-lookup"><span data-stu-id="28508-155">If successful, the response body contains the populated [CartCheckoutResult](cart-resources.md#cartcheckoutresult) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="28508-156">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="28508-156">Response success and error codes</span></span>

<span data-ttu-id="28508-157">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="28508-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="28508-158">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="28508-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="28508-159">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="28508-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="28508-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="28508-160">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
?{
  "orders": [
    {
      "id": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "alternateId": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "MS-AZR-0145P",
          "subscriptionId": "EF2E1307-86E6-40E3-A794-872403FBD31C",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Microsoft Azure",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.76+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "311qiN8iFwkv-XARWMvXRYAwYKMACVqv1",
      "alternateId": "0a3624c6e47d",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "one_time",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 1 Year",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 1,
          "offerId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
          "termDuration": "P3Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 3 Years",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 2,
          "offerId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
          "transactionType": "New",
          "friendlyName": "BizTalk Server 2016 Branch",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:51.6578126Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "HVu_cO8Ea7fNRQP4ia1QTpZap-kg_7P71",
      "alternateId": "55a4e6854d54",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
          "termDuration": "P1M",
          "transactionType": "New",
          "friendlyName": "Barracuda WaaS - Medium Plan",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.4514129Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    }
  ],
  ...
}
```
