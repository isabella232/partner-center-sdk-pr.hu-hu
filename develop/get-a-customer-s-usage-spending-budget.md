---
title: Az ügyfél használati költségének lekért költségvetése
description: A költségkeret (a SpendingBudget objektum) használatával frissítheti az ügyfelek használati összegzését (a CustomerUsageSummary erőforrást).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b55f59fff7e5d7865811ecab3e901848126d31f7
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874873"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="0b2a1-103">Az ügyfél használati költségének lekért költségvetése</span><span class="sxs-lookup"><span data-stu-id="0b2a1-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="0b2a1-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0b2a1-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0b2a1-105">A költségkeretet **(a SpendingBudget** objektumot) az ügyfél használati összegzésében [ **(a CustomerUsageSummary** erőforrásban) frissítheti.](customer-usage-resources.md#customerusagesummary)</span><span class="sxs-lookup"><span data-stu-id="0b2a1-105">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b2a1-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="0b2a1-106">Prerequisites</span></span>

- <span data-ttu-id="0b2a1-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0b2a1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0b2a1-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0b2a1-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0b2a1-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0b2a1-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0b2a1-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0b2a1-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="0b2a1-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0b2a1-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="0b2a1-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0b2a1-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="0b2a1-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0b2a1-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0b2a1-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0b2a1-115">C\#</span><span class="sxs-lookup"><span data-stu-id="0b2a1-115">C\#</span></span>

<span data-ttu-id="0b2a1-116">Az ügyfél használati költségkeretének frissítése:</span><span class="sxs-lookup"><span data-stu-id="0b2a1-116">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="0b2a1-117">Hozzon létre egy [**új SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) objektumot a frissített mennyiséggel.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-117">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="0b2a1-118">Az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) gyűjtemény használatával hívja meg a [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="0b2a1-119">Hívja meg [**a Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) vagy [**GetAsync metódust**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) az ügyfél használati költségvetésének lehívása érdekében.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="0b2a1-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="0b2a1-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0b2a1-121">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="0b2a1-121">Request syntax</span></span>

| <span data-ttu-id="0b2a1-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="0b2a1-122">Method</span></span>    | <span data-ttu-id="0b2a1-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="0b2a1-123">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0b2a1-124">**Kap**</span><span class="sxs-lookup"><span data-stu-id="0b2a1-124">**GET**</span></span> | <span data-ttu-id="0b2a1-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0b2a1-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0b2a1-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="0b2a1-126">URI parameter</span></span>

<span data-ttu-id="0b2a1-127">A számlázási profil frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-127">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="0b2a1-128">Név</span><span class="sxs-lookup"><span data-stu-id="0b2a1-128">Name</span></span>                   | <span data-ttu-id="0b2a1-129">Típus</span><span class="sxs-lookup"><span data-stu-id="0b2a1-129">Type</span></span>     | <span data-ttu-id="0b2a1-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="0b2a1-130">Required</span></span> | <span data-ttu-id="0b2a1-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="0b2a1-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0b2a1-132">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="0b2a1-132">**customer-tenant-id**</span></span> | <span data-ttu-id="0b2a1-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="0b2a1-133">**guid**</span></span> | <span data-ttu-id="0b2a1-134">Y</span><span class="sxs-lookup"><span data-stu-id="0b2a1-134">Y</span></span>        | <span data-ttu-id="0b2a1-135">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-135">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0b2a1-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="0b2a1-136">Request headers</span></span>

<span data-ttu-id="0b2a1-137">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0b2a1-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0b2a1-138">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="0b2a1-138">Request body</span></span>

<span data-ttu-id="0b2a1-139">A teljes erőforrás.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-139">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="0b2a1-140">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="0b2a1-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="0b2a1-141">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="0b2a1-141">REST response</span></span>

<span data-ttu-id="0b2a1-142">Ha ez a módszer sikeres, a felhasználó költségkeretét adja vissza a frissített összeggel.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-142">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0b2a1-143">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="0b2a1-143">Response success and error codes</span></span>

<span data-ttu-id="0b2a1-144">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0b2a1-145">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="0b2a1-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0b2a1-146">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0b2a1-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0b2a1-147">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="0b2a1-147">Response example</span></span>

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
