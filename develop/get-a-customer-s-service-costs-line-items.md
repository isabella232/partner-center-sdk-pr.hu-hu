---
title: Egy ügyfél szolgáltatásdíjai sorelemeinek lekérése
description: Lekérte az ügyfél szolgáltatási költségsorának elemeit a megadott számlázási időszakra vonatkozóan.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1bc2914d7c8d41c6d806131444fdc241aa1feb90
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874941"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="d11e2-103">Egy ügyfél szolgáltatásdíjai sorelemeinek lekérése</span><span class="sxs-lookup"><span data-stu-id="d11e2-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="d11e2-104">Lekérte az ügyfél szolgáltatási költségsorának elemeit a megadott számlázási időszakra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="d11e2-104">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d11e2-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d11e2-105">Prerequisites</span></span>

- <span data-ttu-id="d11e2-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d11e2-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d11e2-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="d11e2-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="d11e2-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d11e2-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d11e2-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d11e2-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d11e2-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d11e2-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d11e2-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="d11e2-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d11e2-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="d11e2-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d11e2-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d11e2-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d11e2-114">A számlázási időszak jelzője ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="d11e2-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="d11e2-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d11e2-115">C\#</span></span>

<span data-ttu-id="d11e2-116">A megadott ügyfél szolgáltatási költségeinek összegzése:</span><span class="sxs-lookup"><span data-stu-id="d11e2-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="d11e2-117">Az ügyfél azonosításához hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="d11e2-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="d11e2-118">A [**ServiceCosts tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) használatával lekért felület az ügyfélszolgálati költségek gyűjtési műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="d11e2-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="d11e2-119">Hívja meg a [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) metódust a [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumerálás egy tagjára egy [**IServiceCostsCollection érték visszaadásaként.**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)</span><span class="sxs-lookup"><span data-stu-id="d11e2-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="d11e2-120">Az [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) metódussal lekérte az ügyfél szolgáltatásiköltség-sor tételét.</span><span class="sxs-lookup"><span data-stu-id="d11e2-120">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="d11e2-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d11e2-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d11e2-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d11e2-122">Request syntax</span></span>

| <span data-ttu-id="d11e2-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="d11e2-123">Method</span></span>  | <span data-ttu-id="d11e2-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d11e2-124">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d11e2-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d11e2-125">**GET**</span></span> | <span data-ttu-id="d11e2-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/servicecosts/{számlázási időszak}/lineitems HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d11e2-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="d11e2-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="d11e2-127">URI parameters</span></span>

<span data-ttu-id="d11e2-128">Az ügyfél és a számlázási időszak azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="d11e2-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="d11e2-129">Név</span><span class="sxs-lookup"><span data-stu-id="d11e2-129">Name</span></span>           | <span data-ttu-id="d11e2-130">Típus</span><span class="sxs-lookup"><span data-stu-id="d11e2-130">Type</span></span>   | <span data-ttu-id="d11e2-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d11e2-131">Required</span></span> | <span data-ttu-id="d11e2-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="d11e2-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d11e2-133">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="d11e2-133">customer-id</span></span>    | <span data-ttu-id="d11e2-134">guid</span><span class="sxs-lookup"><span data-stu-id="d11e2-134">guid</span></span>   | <span data-ttu-id="d11e2-135">Igen</span><span class="sxs-lookup"><span data-stu-id="d11e2-135">Yes</span></span>      | <span data-ttu-id="d11e2-136">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d11e2-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="d11e2-137">számlázási időszak</span><span class="sxs-lookup"><span data-stu-id="d11e2-137">billing-period</span></span> | <span data-ttu-id="d11e2-138">sztring</span><span class="sxs-lookup"><span data-stu-id="d11e2-138">string</span></span> | <span data-ttu-id="d11e2-139">Igen</span><span class="sxs-lookup"><span data-stu-id="d11e2-139">Yes</span></span>      | <span data-ttu-id="d11e2-140">A számlázási időszakot jelölő jelző.</span><span class="sxs-lookup"><span data-stu-id="d11e2-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="d11e2-141">Az egyetlen támogatott érték a MostRecent.</span><span class="sxs-lookup"><span data-stu-id="d11e2-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="d11e2-142">A sztringben nem számít a kis- és a nagy- és a kis- és a nagy- és a nagy-nagyszomba</span><span class="sxs-lookup"><span data-stu-id="d11e2-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d11e2-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d11e2-143">Request headers</span></span>

<span data-ttu-id="d11e2-144">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d11e2-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d11e2-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d11e2-145">Request body</span></span>

<span data-ttu-id="d11e2-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d11e2-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d11e2-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d11e2-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d11e2-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d11e2-148">REST response</span></span>

<span data-ttu-id="d11e2-149">Ha ez sikeres, a válasz törzse tartalmaz egy [ServiceCostLineItem](service-costs-resources.md) erőforrást, amely információkat nyújt a szolgáltatás költségeiről.</span><span class="sxs-lookup"><span data-stu-id="d11e2-149">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d11e2-150">A következő  tulajdonságok csak azokra a szolgáltatási *költségsorelemekre* vonatkoznak, ahol a termék egy alkalommal vásárolható meg: **productId**, **productName,** **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span><span class="sxs-lookup"><span data-stu-id="d11e2-150">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="d11e2-151">Ezek a *tulajdonságok nem vonatkoznak azokra* a szolgáltatássorelemekre, ahol a termék ismétlődő *vásárlás.*</span><span class="sxs-lookup"><span data-stu-id="d11e2-151">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="d11e2-152">Ezek a tulajdonságok például *nem vonatkoznak az* előfizetés-alapú Office 365 azure-ban.</span><span class="sxs-lookup"><span data-stu-id="d11e2-152">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d11e2-153">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d11e2-153">Response success and error codes</span></span>

<span data-ttu-id="d11e2-154">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d11e2-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d11e2-155">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d11e2-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d11e2-156">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d11e2-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d11e2-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d11e2-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2148
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "attributes": {
        "objectType": "Collection"
    },
    "items":
    [{
            "afterTaxTotal": 0.0,
            "chargeType": "PURCHASE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-01-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 0.0,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2015-12-15T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 0.0,
            "invoiceNumber": "T000003163",
            "invoiceType": "OneTime",
            "productId": "DZH318Z0BJR6",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BMFK",
            "productName": "Azure Managed Experience",
            "skuName": "Azure Managed Experience - Optimize",
            "publisherName": "Microsoft",
            "publisherId": "01323244",
            "termAndBillingCycle": "",
            "discountDetails": "N/A"
        }, {
            "afterTaxTotal": 17.219999999999999,
            "chargeType": "CYCLE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-02-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 17.219999999999999,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2016-01-12T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 17.219999999999999,
            "invoiceNumber": "D000003163",
            "invoiceType": "Recurring",
            "productId": "DZH318Z0BJR7",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BTTTT",
            "productName": "NGINX Plus",
            "skuName": "NGINX Plus (Ubuntu 14.04)",
            "publisherName": "Nginx, Inc.",
            "publisherId": "212336222",
            "termAndBillingCycle": "30 Days Trial",
            "discountDetails": "20%"
        }
    ],
    "links": {
        "self": {
            "headers": [],
            "method": "GET",
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems"
        }
    },
    "totalCount": 2
}
```
