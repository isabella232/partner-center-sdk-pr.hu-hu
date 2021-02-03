---
title: Díjak lekérése a Microsoft Azure-tól
description: Azure Rate-kártya beszerzése valós idejű díjszabással az Azure-ajánlathoz. Az Azure díjszabása meglehetősen dinamikus, és gyakran változnak.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0716f0428b13604105b435a2ce8287a8b4609fea
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/19/2020
ms.locfileid: "97768691"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="e44cc-104">Díjak lekérése a Microsoft Azure-tól</span><span class="sxs-lookup"><span data-stu-id="e44cc-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="e44cc-105">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="e44cc-105">**Applies To**</span></span>

- <span data-ttu-id="e44cc-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e44cc-106">Partner Center</span></span>
- <span data-ttu-id="e44cc-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="e44cc-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e44cc-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="e44cc-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e44cc-109">Azure [Rate-kártya](azure-rate-card-resources.md) beszerzése valós idejű díjszabással az Azure-ajánlathoz.</span><span class="sxs-lookup"><span data-stu-id="e44cc-109">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="e44cc-110">Az Azure díjszabása meglehetősen dinamikus, és gyakran változnak.</span><span class="sxs-lookup"><span data-stu-id="e44cc-110">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="e44cc-111">Ha nyomon szeretné követni a használatot, és segít megjósolni a havi számlát és az egyes ügyfelek számláit, kombinálhatja ezt az Azure Rate Card-lekérdezést úgy, hogy lekérje az [ügyfél által az Azure-hoz tartozó kihasználtsági rekordok beszerzésére](get-a-customer-s-utilization-record-for-azure.md)irányuló kéréssel Microsoft Azure árát.</span><span class="sxs-lookup"><span data-stu-id="e44cc-111">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="e44cc-112">Az árak a piac és a pénznem alapján eltérnek, és ez az API figyelembe veszi a helyet.</span><span class="sxs-lookup"><span data-stu-id="e44cc-112">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="e44cc-113">Alapértelmezés szerint az API a partner-profil beállításait a partner Centerben és a böngésző nyelvén használja, és ezek a beállítások testreszabhatók.</span><span class="sxs-lookup"><span data-stu-id="e44cc-113">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="e44cc-114">A hely ismertsége különösen akkor fontos, ha egyetlen, központosított irodában több piacon kezel értékesítéseket.</span><span class="sxs-lookup"><span data-stu-id="e44cc-114">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="e44cc-115">További információ: URI- [Paraméterek](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="e44cc-115">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="e44cc-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e44cc-116">C\#</span></span>

<span data-ttu-id="e44cc-117">Az Azure Rate kártya beszerzéséhez hívja meg a [**IAzureRateCard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) metódust egy olyan [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) -erőforrás visszaadásához, amely tartalmazza az Azure-árakat.</span><span class="sxs-lookup"><span data-stu-id="e44cc-117">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="e44cc-118">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e44cc-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e44cc-119">**Projekt**: partner Center SDK Samples **osztály**: GetAzureRateCard.cs</span><span class="sxs-lookup"><span data-stu-id="e44cc-119">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="e44cc-120">Java</span><span class="sxs-lookup"><span data-stu-id="e44cc-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="e44cc-121">Az Azure Rate kártya beszerzéséhez hívja meg a **IAzureRateCard. Get** függvényt, amely visszaküldi az Azure-árakat tartalmazó kártya adatait.</span><span class="sxs-lookup"><span data-stu-id="e44cc-121">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="e44cc-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e44cc-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="e44cc-123">Az Azure-kártya beszerzéséhez hajtsa végre a [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) parancsot az Azure-árakat tartalmazó kártya adatainak visszaküldéséhez.</span><span class="sxs-lookup"><span data-stu-id="e44cc-123">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="e44cc-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="e44cc-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e44cc-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e44cc-125">Request syntax</span></span>

| <span data-ttu-id="e44cc-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="e44cc-126">Method</span></span>  | <span data-ttu-id="e44cc-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e44cc-127">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="e44cc-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="e44cc-128">**GET**</span></span> | <span data-ttu-id="e44cc-129">*{baseURL}*/v1/ratecards/Azure? pénznem = {pénznem} &régió = {régió}</span><span class="sxs-lookup"><span data-stu-id="e44cc-129">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="e44cc-130">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="e44cc-130">URI parameters</span></span>

| <span data-ttu-id="e44cc-131">Név</span><span class="sxs-lookup"><span data-stu-id="e44cc-131">Name</span></span>     | <span data-ttu-id="e44cc-132">Típus</span><span class="sxs-lookup"><span data-stu-id="e44cc-132">Type</span></span>   | <span data-ttu-id="e44cc-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e44cc-133">Required</span></span> | <span data-ttu-id="e44cc-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="e44cc-134">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e44cc-135">currency</span><span class="sxs-lookup"><span data-stu-id="e44cc-135">currency</span></span> | <span data-ttu-id="e44cc-136">sztring</span><span class="sxs-lookup"><span data-stu-id="e44cc-136">string</span></span> | <span data-ttu-id="e44cc-137">No</span><span class="sxs-lookup"><span data-stu-id="e44cc-137">No</span></span>       | <span data-ttu-id="e44cc-138">Nem kötelező három betűs ISO-kódot megadni ahhoz a pénznemhez, amelyben az erőforrás-díjszabást megadja (például `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="e44cc-138">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="e44cc-139">A mező alapértelmezett értéke: `USD`.</span><span class="sxs-lookup"><span data-stu-id="e44cc-139">The default is `USD`.</span></span> |
| <span data-ttu-id="e44cc-140">régió</span><span class="sxs-lookup"><span data-stu-id="e44cc-140">region</span></span>   | <span data-ttu-id="e44cc-141">sztring</span><span class="sxs-lookup"><span data-stu-id="e44cc-141">string</span></span> | <span data-ttu-id="e44cc-142">No</span><span class="sxs-lookup"><span data-stu-id="e44cc-142">No</span></span>       | <span data-ttu-id="e44cc-143">Opcionális kétbetűs ISO ország-vagy régiókód, amely azt jelzi, hogy az ajánlat melyik piacon vásárolható meg (például `FR` ).</span><span class="sxs-lookup"><span data-stu-id="e44cc-143">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="e44cc-144">A mező alapértelmezett értéke: `US`.</span><span class="sxs-lookup"><span data-stu-id="e44cc-144">The default is `US`.</span></span>        |

<span data-ttu-id="e44cc-145">A kérelemben megadhatja a választható X-locale [fejlécet](headers.md#rest-request-headers) is.</span><span class="sxs-lookup"><span data-stu-id="e44cc-145">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="e44cc-146">Ha nem tartalmazza az X-locale fejlécet, a rendszer az alapértelmezett értéket ("en-US") használja.</span><span class="sxs-lookup"><span data-stu-id="e44cc-146">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="e44cc-147">Ha a kérelemben megadja a pénznem és a régió paramétereit, a rendszer az X területi beállítás értékét használja a válasz nyelvének meghatározására.</span><span class="sxs-lookup"><span data-stu-id="e44cc-147">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="e44cc-148">Ha nem ad meg régió-és pénznem-paramétereket a kérelemben, a rendszer az X-locale értéket használja a válasz régiójának, pénznemének és nyelvének meghatározására.</span><span class="sxs-lookup"><span data-stu-id="e44cc-148">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="e44cc-149">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="e44cc-149">Request header</span></span>

<span data-ttu-id="e44cc-150">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e44cc-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e44cc-151">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e44cc-151">Request body</span></span>

<span data-ttu-id="e44cc-152">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="e44cc-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e44cc-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e44cc-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e44cc-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e44cc-154">REST response</span></span>

<span data-ttu-id="e44cc-155">Ha a kérelem sikeres, egy [Azure Rate Card](azure-rate-card-resources.md) -erőforrást ad vissza.</span><span class="sxs-lookup"><span data-stu-id="e44cc-155">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e44cc-156">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e44cc-156">Response success and error codes</span></span>

<span data-ttu-id="e44cc-157">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="e44cc-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e44cc-158">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="e44cc-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e44cc-159">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="e44cc-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e44cc-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e44cc-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
