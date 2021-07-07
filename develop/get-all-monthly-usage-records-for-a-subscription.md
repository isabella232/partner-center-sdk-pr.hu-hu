---
title: Egy előfizetés összes havi használati rekordjának lekérése
description: Az AzureResourceMonthlyUsageRecord erőforrás-gyűjtemény használatával lekérte az ügyfél előfizetésén belüli szolgáltatások listáját és a hozzájuk társított minősített használati adatokat.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ee4bd413eec7d5a2dddbe3803df8839589ab7504
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760283"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="f7216-103">Egy előfizetés összes havi használati rekordjának lekérése</span><span class="sxs-lookup"><span data-stu-id="f7216-103">Get all monthly usage records for a subscription</span></span>

<span data-ttu-id="f7216-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f7216-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f7216-105">Az [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) erőforrás-gyűjtemény használatával lekért lista az ügyfél előfizetésén belüli szolgáltatásokról és a társított minősített használati adatokról.</span><span class="sxs-lookup"><span data-stu-id="f7216-105">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7216-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f7216-106">Prerequisites</span></span>

- <span data-ttu-id="f7216-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f7216-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7216-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="f7216-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f7216-109">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7216-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f7216-110">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="f7216-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f7216-111">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f7216-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f7216-112">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f7216-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f7216-113">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="f7216-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f7216-114">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f7216-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f7216-115">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="f7216-115">A subscription identifier.</span></span>

<span data-ttu-id="f7216-116">*Ez az API csak Microsoft Azure (MS-AZR-0145P) előfizetéseket támogat. Azure-csomag használata esetén lásd: Használati adatok [lekérte az előfizetéshez mérő alapján.](get-a-customer-subscription-meter-usage-records.md)*</span><span class="sxs-lookup"><span data-stu-id="f7216-116">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="f7216-117">C\#</span><span class="sxs-lookup"><span data-stu-id="f7216-117">C\#</span></span>

<span data-ttu-id="f7216-118">Az előfizetés erőforrás-használati információinak lekért adatai:</span><span class="sxs-lookup"><span data-stu-id="f7216-118">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="f7216-119">Az **IAggregatePartner.Customers gyűjtemény** használatával hívja meg a **ById()** metódust.</span><span class="sxs-lookup"><span data-stu-id="f7216-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="f7216-120">Hívja meg **a Subscriptions (Előfizetések)** tulajdonságot, **a UsageRecords**(Használati adatok) tulajdonságot, majd a **Resources (Erőforrások)** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="f7216-120">Call the **Subscriptions** property, and **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="f7216-121">Hívja meg **a Get() vagy** **a GetAsync() metódust.**</span><span class="sxs-lookup"><span data-stu-id="f7216-121">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="f7216-122">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="f7216-122">For an example, see the following:</span></span>

- <span data-ttu-id="f7216-123">Minta: [Konzoltesztalkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f7216-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f7216-124">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="f7216-124">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="f7216-125">Osztály: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="f7216-125">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f7216-126">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="f7216-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7216-127">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f7216-127">Request syntax</span></span>

| <span data-ttu-id="f7216-128">Metódus</span><span class="sxs-lookup"><span data-stu-id="f7216-128">Method</span></span>  | <span data-ttu-id="f7216-129">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f7216-129">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f7216-130">**Kap**</span><span class="sxs-lookup"><span data-stu-id="f7216-130">**GET**</span></span> | <span data-ttu-id="f7216-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f7216-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f7216-132">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="f7216-132">URI parameters</span></span>

<span data-ttu-id="f7216-133">Ez a táblázat a minősített használati adatok lekérdező lekérdezési paramétereit sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="f7216-133">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="f7216-134">Név</span><span class="sxs-lookup"><span data-stu-id="f7216-134">Name</span></span>                    | <span data-ttu-id="f7216-135">Típus</span><span class="sxs-lookup"><span data-stu-id="f7216-135">Type</span></span>     | <span data-ttu-id="f7216-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f7216-136">Required</span></span> | <span data-ttu-id="f7216-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="f7216-137">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="f7216-138">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="f7216-138">**customer-tenant-id**</span></span>  | <span data-ttu-id="f7216-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7216-139">**guid**</span></span> | <span data-ttu-id="f7216-140">Y</span><span class="sxs-lookup"><span data-stu-id="f7216-140">Y</span></span>        | <span data-ttu-id="f7216-141">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="f7216-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="f7216-142">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="f7216-142">**subscription-id**</span></span> | <span data-ttu-id="f7216-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="f7216-143">**guid**</span></span> | <span data-ttu-id="f7216-144">Y</span><span class="sxs-lookup"><span data-stu-id="f7216-144">Y</span></span>        | <span data-ttu-id="f7216-145">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="f7216-145">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f7216-146">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f7216-146">Request headers</span></span>

<span data-ttu-id="f7216-147">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f7216-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f7216-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f7216-148">Request body</span></span>

<span data-ttu-id="f7216-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f7216-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f7216-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f7216-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="f7216-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f7216-151">REST response</span></span>

<span data-ttu-id="f7216-152">Ha a művelet sikeres, ez a metódus az **AzureResourceMonthlyUsageRecord** erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="f7216-152">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7216-153">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f7216-153">Response success and error codes</span></span>

<span data-ttu-id="f7216-154">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="f7216-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7216-155">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="f7216-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7216-156">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f7216-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f7216-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f7216-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
