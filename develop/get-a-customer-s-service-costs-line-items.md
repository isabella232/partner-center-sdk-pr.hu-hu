---
title: Egy ügyfél szolgáltatásdíjai sorelemeinek lekérése
description: Lekéri az ügyfél szolgáltatási költségeit a megadott számlázási időszakra vonatkozóan.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2034eaf11342493797688b44b634b8e9598e2e4
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768119"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="8cd0c-103">Egy ügyfél szolgáltatásdíjai sorelemeinek lekérése</span><span class="sxs-lookup"><span data-stu-id="8cd0c-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="8cd0c-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="8cd0c-104">**Applies to:**</span></span>

- <span data-ttu-id="8cd0c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8cd0c-105">Partner Center</span></span>

<span data-ttu-id="8cd0c-106">Lekéri az ügyfél szolgáltatási költségeit a megadott számlázási időszakra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-106">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cd0c-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8cd0c-107">Prerequisites</span></span>

- <span data-ttu-id="8cd0c-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8cd0c-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="8cd0c-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8cd0c-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8cd0c-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="8cd0c-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8cd0c-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8cd0c-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8cd0c-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8cd0c-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8cd0c-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8cd0c-116">Számlázási időszak jelzője ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="8cd0c-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="8cd0c-117">C\#</span><span class="sxs-lookup"><span data-stu-id="8cd0c-117">C\#</span></span>

<span data-ttu-id="8cd0c-118">A megadott ügyfélhez tartozó szolgáltatási költségek összegzésének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="8cd0c-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="8cd0c-119">Hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="8cd0c-120">Az [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) tulajdonság használatával beszerezhet egy felületet az ügyfélszolgálati költségek gyűjtési műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="8cd0c-121">Hívja meg a [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) metódust a [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumerálás egyik tagjával a [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)visszaadásához.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="8cd0c-122">A [**IServiceCostsCollection. listaelemek. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) metódus használatával beolvashatja az ügyfél szolgáltatási költségeinek sorát.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-122">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="8cd0c-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="8cd0c-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8cd0c-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8cd0c-124">Request syntax</span></span>

| <span data-ttu-id="8cd0c-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="8cd0c-125">Method</span></span>  | <span data-ttu-id="8cd0c-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8cd0c-126">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cd0c-127">**GET**</span><span class="sxs-lookup"><span data-stu-id="8cd0c-127">**GET**</span></span> | <span data-ttu-id="8cd0c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/servicecosts/{Billing-period}/lineitems http/1.1</span><span class="sxs-lookup"><span data-stu-id="8cd0c-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8cd0c-129">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="8cd0c-129">URI parameters</span></span>

<span data-ttu-id="8cd0c-130">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és a számlázási időszakot.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="8cd0c-131">Név</span><span class="sxs-lookup"><span data-stu-id="8cd0c-131">Name</span></span>           | <span data-ttu-id="8cd0c-132">Típus</span><span class="sxs-lookup"><span data-stu-id="8cd0c-132">Type</span></span>   | <span data-ttu-id="8cd0c-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8cd0c-133">Required</span></span> | <span data-ttu-id="8cd0c-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="8cd0c-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cd0c-135">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="8cd0c-135">customer-id</span></span>    | <span data-ttu-id="8cd0c-136">guid</span><span class="sxs-lookup"><span data-stu-id="8cd0c-136">guid</span></span>   | <span data-ttu-id="8cd0c-137">Igen</span><span class="sxs-lookup"><span data-stu-id="8cd0c-137">Yes</span></span>      | <span data-ttu-id="8cd0c-138">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="8cd0c-139">számlázási időszak</span><span class="sxs-lookup"><span data-stu-id="8cd0c-139">billing-period</span></span> | <span data-ttu-id="8cd0c-140">sztring</span><span class="sxs-lookup"><span data-stu-id="8cd0c-140">string</span></span> | <span data-ttu-id="8cd0c-141">Igen</span><span class="sxs-lookup"><span data-stu-id="8cd0c-141">Yes</span></span>      | <span data-ttu-id="8cd0c-142">A számlázási időszakot jelölő mutató.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="8cd0c-143">Az egyetlen támogatott érték a MostRecent.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="8cd0c-144">A karakterlánc esetében nincs jelentősége.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8cd0c-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8cd0c-145">Request headers</span></span>

<span data-ttu-id="8cd0c-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8cd0c-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8cd0c-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8cd0c-147">Request body</span></span>

<span data-ttu-id="8cd0c-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8cd0c-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8cd0c-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8cd0c-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8cd0c-150">REST response</span></span>

<span data-ttu-id="8cd0c-151">Ha a művelet sikeres, a válasz törzse egy [ServiceCostLineItem](service-costs-resources.md) -erőforrást tartalmaz, amely információt nyújt a szolgáltatás költségeiről.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-151">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cd0c-152">A következő tulajdonságok *csak* a Service Cost line-elemekre vonatkoznak, ahol a termék *egyszeri vásárlás*: **Termékkód**, **productName**, **SkuID**, **skuName**, **availabilityId**, **publisherId**, **közzétevő neve**, **termAndBillingCycle**, **discountDetails**.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-152">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="8cd0c-153">Ezek a tulajdonságok *nem vonatkoznak* azokra a szervizsorok elemekre, amelyekben a termék *ismétlődő vásárlás*.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-153">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="8cd0c-154">Ezek a tulajdonságok például *nem vonatkoznak* az előfizetés-alapú Office 365-re és az Azure-ra.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-154">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8cd0c-155">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8cd0c-155">Response success and error codes</span></span>

<span data-ttu-id="8cd0c-156">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8cd0c-157">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8cd0c-158">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="8cd0c-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8cd0c-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8cd0c-159">Response example</span></span>

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
