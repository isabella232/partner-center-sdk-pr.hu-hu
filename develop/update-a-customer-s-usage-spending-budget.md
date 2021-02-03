---
title: Ügyfél használati költségkeretének frissítése
description: Frissítse az ügyfél használati feladatokhoz lefoglalt költségkeretét.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 839305fb8fad3ce2442ab93e1d8a4a170b4d41c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768380"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="1ba60-103">Ügyfél használati költségkeretének frissítése</span><span class="sxs-lookup"><span data-stu-id="1ba60-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="1ba60-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="1ba60-104">**Applies To**</span></span>

- <span data-ttu-id="1ba60-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="1ba60-105">Partner Center</span></span>
- <span data-ttu-id="1ba60-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="1ba60-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="1ba60-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="1ba60-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1ba60-108">Frissítse az ügyfél használati feladatokhoz lefoglalt [költségkeretét](customer-usage-resources.md#customerusagesummary) .</span><span class="sxs-lookup"><span data-stu-id="1ba60-108">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ba60-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1ba60-109">Prerequisites</span></span>

- <span data-ttu-id="1ba60-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="1ba60-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ba60-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="1ba60-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1ba60-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ba60-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1ba60-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="1ba60-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1ba60-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="1ba60-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1ba60-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="1ba60-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1ba60-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="1ba60-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1ba60-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1ba60-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1ba60-118">C\#</span><span class="sxs-lookup"><span data-stu-id="1ba60-118">C\#</span></span>

<span data-ttu-id="1ba60-119">Az ügyfél használati költségkeretének frissítéséhez először hozzon létre egy új [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) -objektumot a frissített mennyiséggel.</span><span class="sxs-lookup"><span data-stu-id="1ba60-119">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="1ba60-120">Ezután használja a [**IAggregatePartner. Customs**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) gyűjteményt, és hívja meg a [**ById ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="1ba60-120">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="1ba60-121">Ezután nyissa meg a [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) tulajdonságot, és adja át a frissített használati költségvetést a [**Patch ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) vagy a [**PatchAsync ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) metódusnak.</span><span class="sxs-lookup"><span data-stu-id="1ba60-121">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```

## <a name="rest-request"></a><span data-ttu-id="1ba60-122">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="1ba60-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1ba60-123">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="1ba60-123">Request syntax</span></span>

| <span data-ttu-id="1ba60-124">Metódus</span><span class="sxs-lookup"><span data-stu-id="1ba60-124">Method</span></span>    | <span data-ttu-id="1ba60-125">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="1ba60-125">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ba60-126">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="1ba60-126">**PATCH**</span></span> | <span data-ttu-id="1ba60-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagebudget http/1.1</span><span class="sxs-lookup"><span data-stu-id="1ba60-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1ba60-128">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="1ba60-128">URI parameter</span></span>

<span data-ttu-id="1ba60-129">A számlázási profil frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="1ba60-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="1ba60-130">Név</span><span class="sxs-lookup"><span data-stu-id="1ba60-130">Name</span></span>                   | <span data-ttu-id="1ba60-131">Típus</span><span class="sxs-lookup"><span data-stu-id="1ba60-131">Type</span></span>     | <span data-ttu-id="1ba60-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="1ba60-132">Required</span></span> | <span data-ttu-id="1ba60-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="1ba60-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1ba60-134">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="1ba60-134">**customer-tenant-id**</span></span> | <span data-ttu-id="1ba60-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="1ba60-135">**guid**</span></span> | <span data-ttu-id="1ba60-136">Y</span><span class="sxs-lookup"><span data-stu-id="1ba60-136">Y</span></span>        | <span data-ttu-id="1ba60-137">Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="1ba60-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1ba60-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="1ba60-138">Request headers</span></span>

<span data-ttu-id="1ba60-139">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1ba60-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1ba60-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="1ba60-140">Request body</span></span>

<span data-ttu-id="1ba60-141">A teljes erőforrás.</span><span class="sxs-lookup"><span data-stu-id="1ba60-141">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="1ba60-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="1ba60-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```

## <a name="rest-response"></a><span data-ttu-id="1ba60-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="1ba60-143">REST response</span></span>

<span data-ttu-id="1ba60-144">Ha ez sikeres, ez a módszer a felhasználó költségkeretét adja vissza a frissített mennyiséggel.</span><span class="sxs-lookup"><span data-stu-id="1ba60-144">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1ba60-145">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="1ba60-145">Response success and error codes</span></span>

<span data-ttu-id="1ba60-146">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="1ba60-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1ba60-147">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="1ba60-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1ba60-148">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1ba60-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1ba60-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="1ba60-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

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
            "method":"PATCH",
            "headers":[]
        }
    }
}
```
