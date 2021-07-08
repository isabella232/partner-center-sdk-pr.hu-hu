---
title: Egy ügyfél szolgáltatásdíjai összegzésének lekérése
description: Lekérte az ügyfél szolgáltatási költségeit a megadott számlázási időszakra vonatkozóan.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cab23238b5f62a02a5f7368f626648d5b1b5b7e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874907"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="59f4d-103">Egy ügyfél szolgáltatásdíjai összegzésének lekérése</span><span class="sxs-lookup"><span data-stu-id="59f4d-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="59f4d-104">Lekérte az ügyfél szolgáltatási költségeit a megadott számlázási időszakra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="59f4d-104">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59f4d-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="59f4d-105">Prerequisites</span></span>

- <span data-ttu-id="59f4d-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="59f4d-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="59f4d-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="59f4d-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="59f4d-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59f4d-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="59f4d-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="59f4d-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="59f4d-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="59f4d-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="59f4d-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="59f4d-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="59f4d-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="59f4d-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="59f4d-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59f4d-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="59f4d-114">A számlázási időszak jelzője ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="59f4d-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="59f4d-115">C\#</span><span class="sxs-lookup"><span data-stu-id="59f4d-115">C\#</span></span>

<span data-ttu-id="59f4d-116">A megadott ügyfél szolgáltatási költségeinek összegzése:</span><span class="sxs-lookup"><span data-stu-id="59f4d-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="59f4d-117">Az ügyfél azonosításához hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="59f4d-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="59f4d-118">A [**ServiceCosts tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) használatával lekért felület az ügyfélszolgálati költségek gyűjtési műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="59f4d-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="59f4d-119">Hívja meg a [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) metódust a [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumerálás egy tagjára egy [**IServiceCostsCollection érték visszaadásaként.**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)</span><span class="sxs-lookup"><span data-stu-id="59f4d-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="59f4d-120">Az [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) vagy [**a GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) metódussal lekérte az ügyfél szolgáltatási költségeinek összegzését.</span><span class="sxs-lookup"><span data-stu-id="59f4d-120">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="59f4d-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="59f4d-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="59f4d-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="59f4d-122">Request syntax</span></span>

| <span data-ttu-id="59f4d-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="59f4d-123">Method</span></span>  | <span data-ttu-id="59f4d-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="59f4d-124">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="59f4d-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="59f4d-125">**GET**</span></span> | <span data-ttu-id="59f4d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/servicecosts/{számlázási időszak} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="59f4d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="59f4d-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="59f4d-127">URI parameters</span></span>

<span data-ttu-id="59f4d-128">Az ügyfél és a számlázási időszak azonosításához használja az alábbi elérésiút-paramétereket.</span><span class="sxs-lookup"><span data-stu-id="59f4d-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="59f4d-129">Név</span><span class="sxs-lookup"><span data-stu-id="59f4d-129">Name</span></span>           | <span data-ttu-id="59f4d-130">Típus</span><span class="sxs-lookup"><span data-stu-id="59f4d-130">Type</span></span>   | <span data-ttu-id="59f4d-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="59f4d-131">Required</span></span> | <span data-ttu-id="59f4d-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="59f4d-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="59f4d-133">ügyfél-azonosító</span><span class="sxs-lookup"><span data-stu-id="59f4d-133">customer-id</span></span>    | <span data-ttu-id="59f4d-134">guid</span><span class="sxs-lookup"><span data-stu-id="59f4d-134">guid</span></span>   | <span data-ttu-id="59f4d-135">Igen</span><span class="sxs-lookup"><span data-stu-id="59f4d-135">Yes</span></span>      | <span data-ttu-id="59f4d-136">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="59f4d-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="59f4d-137">számlázási időszak</span><span class="sxs-lookup"><span data-stu-id="59f4d-137">billing-period</span></span> | <span data-ttu-id="59f4d-138">sztring</span><span class="sxs-lookup"><span data-stu-id="59f4d-138">string</span></span> | <span data-ttu-id="59f4d-139">Igen</span><span class="sxs-lookup"><span data-stu-id="59f4d-139">Yes</span></span>      | <span data-ttu-id="59f4d-140">A számlázási időszakot jelölő jelző.</span><span class="sxs-lookup"><span data-stu-id="59f4d-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="59f4d-141">Az egyetlen támogatott érték a MostRecent.</span><span class="sxs-lookup"><span data-stu-id="59f4d-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="59f4d-142">A sztringben nem számít a kis- és a nagy- és a kis- és a nagy- és a nagy-nagyszomba</span><span class="sxs-lookup"><span data-stu-id="59f4d-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="59f4d-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="59f4d-143">Request headers</span></span>

<span data-ttu-id="59f4d-144">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="59f4d-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="59f4d-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="59f4d-145">Request body</span></span>

<span data-ttu-id="59f4d-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="59f4d-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="59f4d-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="59f4d-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="59f4d-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="59f4d-148">REST response</span></span>

<span data-ttu-id="59f4d-149">Ha ez sikeres, a válasz törzse tartalmaz egy [ServiceCostsSummary](service-costs-resources.md) erőforrást, amely információkat nyújt a szolgáltatás költségeiről.</span><span class="sxs-lookup"><span data-stu-id="59f4d-149">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="59f4d-150">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="59f4d-150">Response success and error codes</span></span>

<span data-ttu-id="59f4d-151">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="59f4d-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="59f4d-152">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="59f4d-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="59f4d-153">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="59f4d-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="59f4d-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="59f4d-154">Response example</span></span>

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
