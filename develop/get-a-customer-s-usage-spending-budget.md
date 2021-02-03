---
title: Ügyfél használati költségkeretének beszerzése
description: A SpendingBudget objektummal frissítheti az ügyfél-használati összegzést (a CustomerUsageSummary-erőforrást).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8be9ceaab6b7546de8eacba1e52e8766719e5125
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768104"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="14465-103">Ügyfél használati költségkeretének beszerzése</span><span class="sxs-lookup"><span data-stu-id="14465-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="14465-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="14465-104">**Applies to:**</span></span>

- <span data-ttu-id="14465-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="14465-105">Partner Center</span></span>
- <span data-ttu-id="14465-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="14465-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="14465-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="14465-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="14465-108">Frissítheti a **SpendingBudget** objektumot az [ügyfél-használati összegzésben (a **CustomerUsageSummary** -erőforrás)](customer-usage-resources.md#customerusagesummary).</span><span class="sxs-lookup"><span data-stu-id="14465-108">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14465-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="14465-109">Prerequisites</span></span>

- <span data-ttu-id="14465-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="14465-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="14465-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="14465-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="14465-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14465-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="14465-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="14465-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="14465-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="14465-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="14465-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="14465-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="14465-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="14465-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="14465-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="14465-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="14465-118">C\#</span><span class="sxs-lookup"><span data-stu-id="14465-118">C\#</span></span>

<span data-ttu-id="14465-119">Az ügyfél használati költségkeretének frissítése:</span><span class="sxs-lookup"><span data-stu-id="14465-119">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="14465-120">Hozzon létre egy új [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) -objektumot a frissített mennyiséggel.</span><span class="sxs-lookup"><span data-stu-id="14465-120">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="14465-121">A [**IAggregatePartner. Customs**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) gyűjtemény használatával hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="14465-121">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="14465-122">Hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) metódust az ügyfél használati költségkeretének beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="14465-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest-request"></a><span data-ttu-id="14465-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="14465-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="14465-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="14465-124">Request syntax</span></span>

| <span data-ttu-id="14465-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="14465-125">Method</span></span>    | <span data-ttu-id="14465-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="14465-126">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14465-127">**GET**</span><span class="sxs-lookup"><span data-stu-id="14465-127">**GET**</span></span> | <span data-ttu-id="14465-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagebudget http/1.1</span><span class="sxs-lookup"><span data-stu-id="14465-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="14465-129">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="14465-129">URI parameter</span></span>

<span data-ttu-id="14465-130">A számlázási profil frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="14465-130">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="14465-131">Név</span><span class="sxs-lookup"><span data-stu-id="14465-131">Name</span></span>                   | <span data-ttu-id="14465-132">Típus</span><span class="sxs-lookup"><span data-stu-id="14465-132">Type</span></span>     | <span data-ttu-id="14465-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="14465-133">Required</span></span> | <span data-ttu-id="14465-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="14465-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="14465-135">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="14465-135">**customer-tenant-id**</span></span> | <span data-ttu-id="14465-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="14465-136">**guid**</span></span> | <span data-ttu-id="14465-137">Y</span><span class="sxs-lookup"><span data-stu-id="14465-137">Y</span></span>        | <span data-ttu-id="14465-138">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="14465-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="14465-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="14465-139">Request headers</span></span>

<span data-ttu-id="14465-140">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="14465-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="14465-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="14465-141">Request body</span></span>

<span data-ttu-id="14465-142">A teljes erőforrás.</span><span class="sxs-lookup"><span data-stu-id="14465-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="14465-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="14465-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="14465-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="14465-144">REST response</span></span>

<span data-ttu-id="14465-145">Ha ez sikeres, ez a módszer a felhasználó költségkeretét adja vissza a frissített mennyiséggel.</span><span class="sxs-lookup"><span data-stu-id="14465-145">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="14465-146">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="14465-146">Response success and error codes</span></span>

<span data-ttu-id="14465-147">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="14465-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="14465-148">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="14465-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="14465-149">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="14465-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="14465-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="14465-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"GET",
            "headers":[]
        }
    }
}
```
