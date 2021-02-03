---
title: Az előfizetéshez tartozó összes havi használati rekord beolvasása.
description: A AzureResourceMonthlyUsageRecord erőforrás-gyűjtemény használatával lekérheti az ügyfél előfizetésén belüli szolgáltatások listáját, valamint a hozzájuk rendelt használati adatokat.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1dd09d4976c9626e088cda02ce36669dd7121a99
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768364"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="5cd35-103">Az előfizetéshez tartozó összes havi használati rekord beolvasása.</span><span class="sxs-lookup"><span data-stu-id="5cd35-103">Get all monthly usage records for a subscription.</span></span>

<span data-ttu-id="5cd35-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="5cd35-104">**Applies to:**</span></span>

- <span data-ttu-id="5cd35-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5cd35-105">Partner Center</span></span>
- <span data-ttu-id="5cd35-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5cd35-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5cd35-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5cd35-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5cd35-108">A [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) erőforrás-gyűjtemény használatával lekérheti az ügyfél előfizetésén belüli szolgáltatások listáját, valamint a hozzájuk rendelt használati adatokat.</span><span class="sxs-lookup"><span data-stu-id="5cd35-108">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cd35-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5cd35-109">Prerequisites</span></span>

- <span data-ttu-id="5cd35-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5cd35-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5cd35-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="5cd35-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5cd35-112">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5cd35-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5cd35-113">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="5cd35-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5cd35-114">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="5cd35-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5cd35-115">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="5cd35-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5cd35-116">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="5cd35-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5cd35-117">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5cd35-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5cd35-118">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="5cd35-118">A subscription identifier.</span></span>

<span data-ttu-id="5cd35-119">*Ez az API csak Microsoft Azure (MS-AZR-0145P) előfizetéseket támogatja. Ha Azure-csomagot használ, tekintse [meg a használati adatok beolvasása az előfizetéshez mérőszám alapján](get-a-customer-subscription-meter-usage-records.md) című témakört.*</span><span class="sxs-lookup"><span data-stu-id="5cd35-119">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="5cd35-120">C\#</span><span class="sxs-lookup"><span data-stu-id="5cd35-120">C\#</span></span>

<span data-ttu-id="5cd35-121">Az előfizetés erőforrás-használati adatainak beszerzése:</span><span class="sxs-lookup"><span data-stu-id="5cd35-121">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="5cd35-122">A **IAggregatePartner. Customs** gyűjtemény használatával hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="5cd35-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="5cd35-123">Hívja meg az **előfizetések** tulajdonságot, valamint a **UsageRecords**, majd a **Resources (erőforrások** ) tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="5cd35-123">Call the **Subscriptions** property, as well as **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="5cd35-124">Hívja meg a **Get ()** vagy a **GetAsync ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="5cd35-124">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="5cd35-125">Példaként tekintse meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="5cd35-125">For an example, see the following:</span></span>

- <span data-ttu-id="5cd35-126">Minta: [konzol tesztelési alkalmazás](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5cd35-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5cd35-127">Projekt: **PartnerSDK. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="5cd35-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="5cd35-128">Osztály: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="5cd35-128">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5cd35-129">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5cd35-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5cd35-130">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5cd35-130">Request syntax</span></span>

| <span data-ttu-id="5cd35-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="5cd35-131">Method</span></span>  | <span data-ttu-id="5cd35-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5cd35-132">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5cd35-133">**GET**</span><span class="sxs-lookup"><span data-stu-id="5cd35-133">**GET**</span></span> | <span data-ttu-id="5cd35-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/usagerecords/Resources http/1.1</span><span class="sxs-lookup"><span data-stu-id="5cd35-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="5cd35-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="5cd35-135">URI parameters</span></span>

<span data-ttu-id="5cd35-136">Ez a táblázat felsorolja a szükséges lekérdezési paramétereket a névleges használati adatok lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="5cd35-136">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="5cd35-137">Név</span><span class="sxs-lookup"><span data-stu-id="5cd35-137">Name</span></span>                    | <span data-ttu-id="5cd35-138">Típus</span><span class="sxs-lookup"><span data-stu-id="5cd35-138">Type</span></span>     | <span data-ttu-id="5cd35-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5cd35-139">Required</span></span> | <span data-ttu-id="5cd35-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="5cd35-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="5cd35-141">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="5cd35-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="5cd35-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="5cd35-142">**guid**</span></span> | <span data-ttu-id="5cd35-143">Y</span><span class="sxs-lookup"><span data-stu-id="5cd35-143">Y</span></span>        | <span data-ttu-id="5cd35-144">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="5cd35-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="5cd35-145">**előfizetés-azonosító**</span><span class="sxs-lookup"><span data-stu-id="5cd35-145">**subscription-id**</span></span> | <span data-ttu-id="5cd35-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="5cd35-146">**guid**</span></span> | <span data-ttu-id="5cd35-147">Y</span><span class="sxs-lookup"><span data-stu-id="5cd35-147">Y</span></span>        | <span data-ttu-id="5cd35-148">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="5cd35-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5cd35-149">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5cd35-149">Request headers</span></span>

<span data-ttu-id="5cd35-150">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5cd35-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5cd35-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5cd35-151">Request body</span></span>

<span data-ttu-id="5cd35-152">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="5cd35-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5cd35-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5cd35-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="5cd35-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5cd35-154">REST response</span></span>

<span data-ttu-id="5cd35-155">Ha ez sikeres, ez a metódus **AzureResourceMonthlyUsageRecord** -erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="5cd35-155">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5cd35-156">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5cd35-156">Response success and error codes</span></span>

<span data-ttu-id="5cd35-157">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5cd35-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5cd35-158">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5cd35-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5cd35-159">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5cd35-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5cd35-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5cd35-160">Response example</span></span>

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
