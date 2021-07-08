---
title: Díjak lekérése a Microsoft Azure-tól
description: Azure-díjkártyák lekért valós idejű árai egy Azure-ajánlathoz. Az Azure díjszabása meglehetősen dinamikus, és gyakran változik.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4f66ab19ef3723fbaa27acff941cf48683a7c25c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548787"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="60751-104">Díjak lekérése a Microsoft Azure-tól</span><span class="sxs-lookup"><span data-stu-id="60751-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="60751-105">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="60751-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="60751-106">Azure-díjkártyák [lekért](azure-rate-card-resources.md) valós idejű árai egy Azure-ajánlathoz.</span><span class="sxs-lookup"><span data-stu-id="60751-106">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="60751-107">Az Azure díjszabása meglehetősen dinamikus, és gyakran változik.</span><span class="sxs-lookup"><span data-stu-id="60751-107">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="60751-108">A használat nyomon követéséhez és a havi számla és az egyes ügyfelek számlái előrejelzéséhez kombinálhatja ezt az Azure Rate Card-lekérdezést az Microsoft Azure árainak lekéréséhez az ügyfél Azure-beli kihasználtsági rekordjainak lekérésére vonatkozó [kéréssel.](get-a-customer-s-utilization-record-for-azure.md)</span><span class="sxs-lookup"><span data-stu-id="60751-108">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="60751-109">Az árak piac és pénznem szerint különböznek, és ez az API figyelembe veszi a helyet.</span><span class="sxs-lookup"><span data-stu-id="60751-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="60751-110">Alapértelmezés szerint az API a partnerprofil beállításait használja a Partnerközpont böngészőnyelven, és ezek a beállítások testre szabhatók.</span><span class="sxs-lookup"><span data-stu-id="60751-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="60751-111">A helytudatosság különösen fontos, ha az értékesítéseket több piacon kezeli egyetlen központi irodából.</span><span class="sxs-lookup"><span data-stu-id="60751-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="60751-112">További információ: [URI-paraméterek.](#uri-parameters)</span><span class="sxs-lookup"><span data-stu-id="60751-112">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="60751-113">C\#</span><span class="sxs-lookup"><span data-stu-id="60751-113">C\#</span></span>

<span data-ttu-id="60751-114">Az Azure Rate Card beszerzéséhez hívja meg az [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) metódust az Azure-árakat tartalmazó [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) erőforrás visszaadása érdekében.</span><span class="sxs-lookup"><span data-stu-id="60751-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="60751-115">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="60751-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="60751-116">**Project:** Partnerközpont SDK **Osztály:** GetAzureRateCard.cs</span><span class="sxs-lookup"><span data-stu-id="60751-116">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="60751-117">Java</span><span class="sxs-lookup"><span data-stu-id="60751-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="60751-118">Az Azure Rate Card beszerzéséhez hívja meg az **IAzureRateCard.get** függvényt az Azure-árakat tartalmazó díjszabási kártya részleteinek visszaadás érdekében.</span><span class="sxs-lookup"><span data-stu-id="60751-118">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="60751-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60751-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="60751-120">Az Azure-kártya beszerzéséhez futtasa le a [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) parancsot az Azure-árakat tartalmazó díjszabási kártya részleteinek visszaadás érdekében.</span><span class="sxs-lookup"><span data-stu-id="60751-120">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="60751-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="60751-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="60751-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="60751-122">Request syntax</span></span>

| <span data-ttu-id="60751-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="60751-123">Method</span></span>  | <span data-ttu-id="60751-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="60751-124">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="60751-125">**Kap**</span><span class="sxs-lookup"><span data-stu-id="60751-125">**GET**</span></span> | <span data-ttu-id="60751-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span><span class="sxs-lookup"><span data-stu-id="60751-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="60751-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="60751-127">URI parameters</span></span>

| <span data-ttu-id="60751-128">Név</span><span class="sxs-lookup"><span data-stu-id="60751-128">Name</span></span>     | <span data-ttu-id="60751-129">Típus</span><span class="sxs-lookup"><span data-stu-id="60751-129">Type</span></span>   | <span data-ttu-id="60751-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="60751-130">Required</span></span> | <span data-ttu-id="60751-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="60751-131">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="60751-132">currency</span><span class="sxs-lookup"><span data-stu-id="60751-132">currency</span></span> | <span data-ttu-id="60751-133">sztring</span><span class="sxs-lookup"><span data-stu-id="60751-133">string</span></span> | <span data-ttu-id="60751-134">No</span><span class="sxs-lookup"><span data-stu-id="60751-134">No</span></span>       | <span data-ttu-id="60751-135">Nem kötelező hárombetűs ISO-kód az erőforrás-díjszabást megszabadtó pénznemhez `EUR` (például).</span><span class="sxs-lookup"><span data-stu-id="60751-135">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="60751-136">A mező alapértelmezett értéke: `USD`.</span><span class="sxs-lookup"><span data-stu-id="60751-136">The default is `USD`.</span></span> |
| <span data-ttu-id="60751-137">régió</span><span class="sxs-lookup"><span data-stu-id="60751-137">region</span></span>   | <span data-ttu-id="60751-138">sztring</span><span class="sxs-lookup"><span data-stu-id="60751-138">string</span></span> | <span data-ttu-id="60751-139">No</span><span class="sxs-lookup"><span data-stu-id="60751-139">No</span></span>       | <span data-ttu-id="60751-140">Választható kétbetűs ISO-ország-/régiókód, amely az ajánlat vásárlásának piacát jelzi `FR` (például).</span><span class="sxs-lookup"><span data-stu-id="60751-140">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="60751-141">A mező alapértelmezett értéke: `US`.</span><span class="sxs-lookup"><span data-stu-id="60751-141">The default is `US`.</span></span>        |

<span data-ttu-id="60751-142">A kérelembe be is [](headers.md#rest-request-headers) foglalhatja az opcionális X-Locale fejlécet.</span><span class="sxs-lookup"><span data-stu-id="60751-142">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="60751-143">Ha nem tartalmazza az X-Locale fejlécet, a rendszer az alapértelmezett értéket ("en-US") használja.</span><span class="sxs-lookup"><span data-stu-id="60751-143">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="60751-144">Ha a kérelemben pénznem- és régióparamétereket ad meg, az X-Locale értéke határozza meg a válasz nyelvét.</span><span class="sxs-lookup"><span data-stu-id="60751-144">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="60751-145">Ha nem ad meg régió- és pénznemparamétereket a kérésben, az X-Locale értéke határozza meg a válasz régióját, pénznemét és nyelvét.</span><span class="sxs-lookup"><span data-stu-id="60751-145">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="60751-146">Kérelem fejléce</span><span class="sxs-lookup"><span data-stu-id="60751-146">Request header</span></span>

<span data-ttu-id="60751-147">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="60751-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="60751-148">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="60751-148">Request body</span></span>

<span data-ttu-id="60751-149">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="60751-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="60751-150">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="60751-150">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="60751-151">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="60751-151">REST response</span></span>

<span data-ttu-id="60751-152">Ha a kérés sikeres, egy [Azure Rate Card-erőforrást ad](azure-rate-card-resources.md) vissza.</span><span class="sxs-lookup"><span data-stu-id="60751-152">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="60751-153">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="60751-153">Response success and error codes</span></span>

<span data-ttu-id="60751-154">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="60751-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="60751-155">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="60751-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="60751-156">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="60751-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="60751-157">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="60751-157">Response example</span></span>

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
