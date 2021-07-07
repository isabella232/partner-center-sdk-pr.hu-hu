---
title: Az ügyfél használati költségkeretének frissítése
description: Frissítse az ügyfél használati költségéhez lefoglalt költségkeretet.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 043bd442266d081105e5e8767b6d597e89fc9e8b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529715"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="a46bb-103">Az ügyfél használati költségkeretének frissítése</span><span class="sxs-lookup"><span data-stu-id="a46bb-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="a46bb-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="a46bb-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a46bb-105">Frissítse [az ügyfél](customer-usage-resources.md#customerusagesummary) használati költségéhez lefoglalt költségkeretet.</span><span class="sxs-lookup"><span data-stu-id="a46bb-105">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a46bb-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a46bb-106">Prerequisites</span></span>

- <span data-ttu-id="a46bb-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a46bb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a46bb-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="a46bb-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a46bb-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a46bb-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a46bb-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a46bb-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a46bb-111">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a46bb-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a46bb-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a46bb-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a46bb-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="a46bb-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a46bb-114">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a46bb-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="a46bb-115">C\#</span><span class="sxs-lookup"><span data-stu-id="a46bb-115">C\#</span></span>

<span data-ttu-id="a46bb-116">Az ügyfél használati költségkeretének frissítéséhez először hozzon létre egy új [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) objektumot a frissített összeggel.</span><span class="sxs-lookup"><span data-stu-id="a46bb-116">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="a46bb-117">Ezután használja az [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) gyűjteményt, és hívja meg a [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust a megadott ügyfél azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="a46bb-117">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="a46bb-118">Ezután hozzáférés a [**UsageBudget tulajdonsághoz,**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) és adja át a frissített használati költségvetést a [**Patch() vagy**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) [**a PatchAsync() metódusnak.**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync)</span><span class="sxs-lookup"><span data-stu-id="a46bb-118">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="a46bb-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="a46bb-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a46bb-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a46bb-120">Request syntax</span></span>

| <span data-ttu-id="a46bb-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="a46bb-121">Method</span></span>    | <span data-ttu-id="a46bb-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a46bb-122">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a46bb-123">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="a46bb-123">**PATCH**</span></span> | <span data-ttu-id="a46bb-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a46bb-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a46bb-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a46bb-125">URI parameter</span></span>

<span data-ttu-id="a46bb-126">A számlázási profil frissítéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="a46bb-126">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="a46bb-127">Név</span><span class="sxs-lookup"><span data-stu-id="a46bb-127">Name</span></span>                   | <span data-ttu-id="a46bb-128">Típus</span><span class="sxs-lookup"><span data-stu-id="a46bb-128">Type</span></span>     | <span data-ttu-id="a46bb-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a46bb-129">Required</span></span> | <span data-ttu-id="a46bb-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="a46bb-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a46bb-131">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="a46bb-131">**customer-tenant-id**</span></span> | <span data-ttu-id="a46bb-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="a46bb-132">**guid**</span></span> | <span data-ttu-id="a46bb-133">Y</span><span class="sxs-lookup"><span data-stu-id="a46bb-133">Y</span></span>        | <span data-ttu-id="a46bb-134">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="a46bb-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a46bb-135">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a46bb-135">Request headers</span></span>

<span data-ttu-id="a46bb-136">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a46bb-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a46bb-137">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="a46bb-137">Request body</span></span>

<span data-ttu-id="a46bb-138">A teljes erőforrás.</span><span class="sxs-lookup"><span data-stu-id="a46bb-138">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="a46bb-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a46bb-139">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a46bb-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a46bb-140">REST response</span></span>

<span data-ttu-id="a46bb-141">Ha ez a módszer sikeres, a felhasználó költségkeretét adja vissza a frissített összeggel.</span><span class="sxs-lookup"><span data-stu-id="a46bb-141">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a46bb-142">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a46bb-142">Response success and error codes</span></span>

<span data-ttu-id="a46bb-143">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="a46bb-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a46bb-144">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="a46bb-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a46bb-145">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a46bb-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a46bb-146">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a46bb-146">Response example</span></span>

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
