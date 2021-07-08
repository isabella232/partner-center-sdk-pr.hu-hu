---
title: Díjak lekérése a Microsoft Azure Partner Shared Servicestől
description: Azure-díjkártya lekért díjszabása a partneri Microsoft Azure szolgáltatásainak áraival.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0008d7474f7e57bbbd765afdf2487ee279848ac3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548804"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="64e8f-103">Díjak lekérése a Microsoft Azure Partner Shared Servicestől</span><span class="sxs-lookup"><span data-stu-id="64e8f-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="64e8f-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="64e8f-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="64e8f-105">Azure-díjkártyák [lekért díjszabása](azure-rate-card-resources.md) a partneri Microsoft Azure szolgáltatásokért.</span><span class="sxs-lookup"><span data-stu-id="64e8f-105">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="64e8f-106">Az árak piac és pénznem szerint különböznek, és ez az API figyelembe veszi a helyet.</span><span class="sxs-lookup"><span data-stu-id="64e8f-106">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="64e8f-107">Alapértelmezés szerint az API a partnerprofil beállításait használja a Partnerközpont böngészőnyelven, és ezek a beállítások testre szabhatók.</span><span class="sxs-lookup"><span data-stu-id="64e8f-107">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="64e8f-108">A helytudatosság különösen fontos, ha az értékesítéseket több piacon kezeli egyetlen központi irodából.</span><span class="sxs-lookup"><span data-stu-id="64e8f-108">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="64e8f-109">Példakód</span><span class="sxs-lookup"><span data-stu-id="64e8f-109">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="64e8f-110">C\#</span><span class="sxs-lookup"><span data-stu-id="64e8f-110">C\#</span></span>

<span data-ttu-id="64e8f-111">Az Azure Rate Card beszerzéséhez hívja meg az [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) metódust az Azure-árakat tartalmazó [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) erőforrás visszaadása érdekében.</span><span class="sxs-lookup"><span data-stu-id="64e8f-111">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="64e8f-112">Java</span><span class="sxs-lookup"><span data-stu-id="64e8f-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="64e8f-113">Az Azure Rate Card beszerzéséhez hívja meg az **IAzureRateCard.getShared** függvényt az Azure-árakat tartalmazó díjszabási kártya részleteinek visszaadás érdekében.</span><span class="sxs-lookup"><span data-stu-id="64e8f-113">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="64e8f-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64e8f-114">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="64e8f-115">Az Azure-kártya beszerzéséhez hajtsa végre a [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) parancsot, és adja meg a **SharedServices** paramétert az Azure-árakat tartalmazó díjszabási kártya részleteinek visszaadása érdekében.</span><span class="sxs-lookup"><span data-stu-id="64e8f-115">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="64e8f-116">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="64e8f-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="64e8f-117">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="64e8f-117">Request syntax</span></span>

| <span data-ttu-id="64e8f-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="64e8f-118">Method</span></span>  | <span data-ttu-id="64e8f-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="64e8f-119">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="64e8f-120">**Kap**</span><span class="sxs-lookup"><span data-stu-id="64e8f-120">**GET**</span></span> | <span data-ttu-id="64e8f-121">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&régió={régió}</span><span class="sxs-lookup"><span data-stu-id="64e8f-121">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="64e8f-122">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="64e8f-122">URI parameters</span></span>

| <span data-ttu-id="64e8f-123">Név</span><span class="sxs-lookup"><span data-stu-id="64e8f-123">Name</span></span>     | <span data-ttu-id="64e8f-124">Típus</span><span class="sxs-lookup"><span data-stu-id="64e8f-124">Type</span></span>   | <span data-ttu-id="64e8f-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="64e8f-125">Required</span></span> | <span data-ttu-id="64e8f-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="64e8f-126">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="64e8f-127">currency</span><span class="sxs-lookup"><span data-stu-id="64e8f-127">currency</span></span> | <span data-ttu-id="64e8f-128">sztring</span><span class="sxs-lookup"><span data-stu-id="64e8f-128">string</span></span> | <span data-ttu-id="64e8f-129">No</span><span class="sxs-lookup"><span data-stu-id="64e8f-129">No</span></span>       | <span data-ttu-id="64e8f-130">Nem kötelező hárombetűs ISO-kód az erőforrás-díjszabást megszabadtó pénznemhez `EUR` (például).</span><span class="sxs-lookup"><span data-stu-id="64e8f-130">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="64e8f-131">Az alapértelmezett pénznem a partnerprofilban a piachoz társított pénznem.</span><span class="sxs-lookup"><span data-stu-id="64e8f-131">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="64e8f-132">régió</span><span class="sxs-lookup"><span data-stu-id="64e8f-132">region</span></span>   | <span data-ttu-id="64e8f-133">sztring</span><span class="sxs-lookup"><span data-stu-id="64e8f-133">string</span></span> | <span data-ttu-id="64e8f-134">No</span><span class="sxs-lookup"><span data-stu-id="64e8f-134">No</span></span>       | <span data-ttu-id="64e8f-135">Választható kétbetűs ISO-ország-/régiókód, amely az ajánlat vásárlásának piacát jelzi `FR` (például).</span><span class="sxs-lookup"><span data-stu-id="64e8f-135">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="64e8f-136">Az alapértelmezett érték a partnerprofilban beállított ország-/régiókód.</span><span class="sxs-lookup"><span data-stu-id="64e8f-136">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="64e8f-137">Ha a kérés tartalmazza az opcionális X-Locale fejlécet, az értéke határozza meg a válaszban szereplő részletek nyelvét.</span><span class="sxs-lookup"><span data-stu-id="64e8f-137">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="64e8f-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="64e8f-138">Request headers</span></span>

<span data-ttu-id="64e8f-139">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="64e8f-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="64e8f-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="64e8f-140">Request body</span></span>

<span data-ttu-id="64e8f-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="64e8f-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="64e8f-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="64e8f-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="64e8f-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="64e8f-143">REST response</span></span>

<span data-ttu-id="64e8f-144">Ha a kérés sikeres, egy [Azure Rate Card-erőforrást ad](azure-rate-card-resources.md) vissza.</span><span class="sxs-lookup"><span data-stu-id="64e8f-144">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="64e8f-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="64e8f-145">Response success and error codes</span></span>

<span data-ttu-id="64e8f-146">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="64e8f-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="64e8f-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="64e8f-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="64e8f-148">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="64e8f-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="64e8f-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="64e8f-149">Response example</span></span>

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
    "locale": "en-US",
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
