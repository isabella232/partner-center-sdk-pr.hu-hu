---
title: Egy ügyfél szolgáltatásdíjai összegzésének lekérése
description: Lekéri az ügyfél szolgáltatási költségeit a megadott számlázási időszakra vonatkozóan.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 635e61342e13c3676120ec0df02f1e8bffda64ac
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768107"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="0a4f4-103">Egy ügyfél szolgáltatásdíjai összegzésének lekérése</span><span class="sxs-lookup"><span data-stu-id="0a4f4-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="0a4f4-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="0a4f4-104">**Applies to:**</span></span>

- <span data-ttu-id="0a4f4-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="0a4f4-105">Partner Center</span></span>

<span data-ttu-id="0a4f4-106">Lekéri az ügyfél szolgáltatási költségeit a megadott számlázási időszakra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-106">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a4f4-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="0a4f4-107">Prerequisites</span></span>

- <span data-ttu-id="0a4f4-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0a4f4-109">Ez a forgatókönyv támogatja a hitelesítést az App + User hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="0a4f4-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a4f4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0a4f4-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="0a4f4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0a4f4-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0a4f4-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0a4f4-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0a4f4-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0a4f4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0a4f4-116">Számlázási időszak jelzője ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="0a4f4-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="0a4f4-117">C\#</span><span class="sxs-lookup"><span data-stu-id="0a4f4-117">C\#</span></span>

<span data-ttu-id="0a4f4-118">A megadott ügyfélhez tartozó szolgáltatási költségek összegzésének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="0a4f4-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="0a4f4-119">Hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="0a4f4-120">Az [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) tulajdonság használatával beszerezhet egy felületet az ügyfélszolgálati költségek gyűjtési műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="0a4f4-121">Hívja meg a [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) metódust a [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumerálás egyik tagjával a [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)visszaadásához.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="0a4f4-122">Használja az [**IServiceCostsCollection. summary. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) metódust az ügyfél szolgáltatási költségei összegzésének beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-122">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="0a4f4-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="0a4f4-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0a4f4-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="0a4f4-124">Request syntax</span></span>

| <span data-ttu-id="0a4f4-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="0a4f4-125">Method</span></span>  | <span data-ttu-id="0a4f4-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="0a4f4-126">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a4f4-127">**GET**</span><span class="sxs-lookup"><span data-stu-id="0a4f4-127">**GET**</span></span> | <span data-ttu-id="0a4f4-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/servicecosts/{Billing-period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="0a4f4-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="0a4f4-129">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="0a4f4-129">URI parameters</span></span>

<span data-ttu-id="0a4f4-130">A következő elérésiút-paraméterek használatával azonosíthatja az ügyfelet és a számlázási időszakot.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="0a4f4-131">Név</span><span class="sxs-lookup"><span data-stu-id="0a4f4-131">Name</span></span>           | <span data-ttu-id="0a4f4-132">Típus</span><span class="sxs-lookup"><span data-stu-id="0a4f4-132">Type</span></span>   | <span data-ttu-id="0a4f4-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="0a4f4-133">Required</span></span> | <span data-ttu-id="0a4f4-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="0a4f4-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0a4f4-135">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="0a4f4-135">customer-id</span></span>    | <span data-ttu-id="0a4f4-136">guid</span><span class="sxs-lookup"><span data-stu-id="0a4f4-136">guid</span></span>   | <span data-ttu-id="0a4f4-137">Igen</span><span class="sxs-lookup"><span data-stu-id="0a4f4-137">Yes</span></span>      | <span data-ttu-id="0a4f4-138">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="0a4f4-139">számlázási időszak</span><span class="sxs-lookup"><span data-stu-id="0a4f4-139">billing-period</span></span> | <span data-ttu-id="0a4f4-140">sztring</span><span class="sxs-lookup"><span data-stu-id="0a4f4-140">string</span></span> | <span data-ttu-id="0a4f4-141">Igen</span><span class="sxs-lookup"><span data-stu-id="0a4f4-141">Yes</span></span>      | <span data-ttu-id="0a4f4-142">A számlázási időszakot jelölő mutató.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="0a4f4-143">Az egyetlen támogatott érték a MostRecent.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="0a4f4-144">A karakterlánc esetében nincs jelentősége.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0a4f4-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="0a4f4-145">Request headers</span></span>

<span data-ttu-id="0a4f4-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0a4f4-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0a4f4-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="0a4f4-147">Request body</span></span>

<span data-ttu-id="0a4f4-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0a4f4-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="0a4f4-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0a4f4-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="0a4f4-150">REST response</span></span>

<span data-ttu-id="0a4f4-151">Ha a művelet sikeres, a válasz törzse egy [ServiceCostsSummary](service-costs-resources.md) -erőforrást tartalmaz, amely információt nyújt a szolgáltatás költségeiről.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-151">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0a4f4-152">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="0a4f4-152">Response success and error codes</span></span>

<span data-ttu-id="0a4f4-153">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0a4f4-154">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0a4f4-155">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="0a4f4-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0a4f4-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="0a4f4-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 766
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "billingStartDate": "2015-12-12T00:00:00Z",
    "billingEndDate": "2016-01-11T00:00:00Z",
    "pretaxTotal": 17.22,
    "tax": 0.0,
    "afterTaxTotal": 17.22,
    "currencySymbol": "$",
    "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
    "details":
     [
        {
            "invoiceType": "Recurring",
            "summary": {
                "billingStartDate": "2015-12-12T00:00:00Z",
                "billingEndDate": "2016-01-11T00:00:00Z",
                "pretaxTotal": 17.22,
                "tax": 0.0,
                "afterTaxTotal": 17.22,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "billingStartDate": "2019-04-01T00:00:00Z",
                "billingEndDate": "2019-04-30T23:59:59.9999999Z",
                "pretaxTotal": 2,
                "tax": 0.2,
                "afterTaxTotal": 2.2,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        }
    ],
    "links": {
        "serviceCostLineItems": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "ServiceCostsSummary"
    }
}
```
