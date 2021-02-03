---
title: Díjak lekérése a Microsoft Azure Partner Shared Servicestől
description: Azure Rate-kártya beszerzése Microsoft Azure partner megosztott szolgáltatások díjszabásával.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cd396c35b6b89de4d0f092ba4da738a2ed0ac633
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768479"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="5b349-103">Díjak lekérése a Microsoft Azure Partner Shared Servicestől</span><span class="sxs-lookup"><span data-stu-id="5b349-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="5b349-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="5b349-104">**Applies To**</span></span>

- <span data-ttu-id="5b349-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5b349-105">Partner Center</span></span>
- <span data-ttu-id="5b349-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5b349-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5b349-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5b349-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5b349-108">[Azure Rate-kártya](azure-rate-card-resources.md) beszerzése Microsoft Azure partner megosztott szolgáltatások díjszabásával.</span><span class="sxs-lookup"><span data-stu-id="5b349-108">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="5b349-109">Az árak a piac és a pénznem alapján eltérnek, és ez az API figyelembe veszi a helyet.</span><span class="sxs-lookup"><span data-stu-id="5b349-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="5b349-110">Alapértelmezés szerint az API a partner-profil beállításait a partner Centerben és a böngésző nyelvén használja, és ezek a beállítások testreszabhatók.</span><span class="sxs-lookup"><span data-stu-id="5b349-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="5b349-111">A hely ismertsége különösen akkor fontos, ha egyetlen, központosított irodában több piacon kezel értékesítéseket.</span><span class="sxs-lookup"><span data-stu-id="5b349-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="5b349-112">Példa kódja</span><span class="sxs-lookup"><span data-stu-id="5b349-112">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="5b349-113">C\#</span><span class="sxs-lookup"><span data-stu-id="5b349-113">C\#</span></span>

<span data-ttu-id="5b349-114">Az Azure Rate kártya beszerzéséhez hívja meg a [**IAzureRateCard. GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) metódust egy olyan [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) -erőforrás visszaadásához, amely tartalmazza az Azure-árakat.</span><span class="sxs-lookup"><span data-stu-id="5b349-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="5b349-115">Java</span><span class="sxs-lookup"><span data-stu-id="5b349-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="5b349-116">Az Azure Rate kártya beszerzéséhez hívja meg a **IAzureRateCard. getShared** függvényt, hogy visszaállítsa az árfolyam-kártya adatait, amelyek tartalmazzák az Azure-árakat.</span><span class="sxs-lookup"><span data-stu-id="5b349-116">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="5b349-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b349-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="5b349-118">Az Azure-kártya beszerzéséhez hajtsa végre a [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) parancsot, és a **SharedServices** paramétert megadhatja az Azure-árakat tartalmazó kártya adatainak visszaadásához.</span><span class="sxs-lookup"><span data-stu-id="5b349-118">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="5b349-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5b349-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5b349-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5b349-120">Request syntax</span></span>

| <span data-ttu-id="5b349-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="5b349-121">Method</span></span>  | <span data-ttu-id="5b349-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5b349-122">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="5b349-123">**GET**</span><span class="sxs-lookup"><span data-stu-id="5b349-123">**GET**</span></span> | <span data-ttu-id="5b349-124">*{baseURL}*/v1/ratecards/Azure-Shared? pénznem = {pénznem} &régió = {régió}</span><span class="sxs-lookup"><span data-stu-id="5b349-124">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="5b349-125">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="5b349-125">URI parameters</span></span>

| <span data-ttu-id="5b349-126">Név</span><span class="sxs-lookup"><span data-stu-id="5b349-126">Name</span></span>     | <span data-ttu-id="5b349-127">Típus</span><span class="sxs-lookup"><span data-stu-id="5b349-127">Type</span></span>   | <span data-ttu-id="5b349-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5b349-128">Required</span></span> | <span data-ttu-id="5b349-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="5b349-129">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5b349-130">currency</span><span class="sxs-lookup"><span data-stu-id="5b349-130">currency</span></span> | <span data-ttu-id="5b349-131">sztring</span><span class="sxs-lookup"><span data-stu-id="5b349-131">string</span></span> | <span data-ttu-id="5b349-132">No</span><span class="sxs-lookup"><span data-stu-id="5b349-132">No</span></span>       | <span data-ttu-id="5b349-133">Nem kötelező három betűs ISO-kódot megadni ahhoz a pénznemhez, amelyben az erőforrás-díjszabást megadja (például `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="5b349-133">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="5b349-134">Az alapértelmezett érték a partneri profil piacához társított pénznem.</span><span class="sxs-lookup"><span data-stu-id="5b349-134">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="5b349-135">régió</span><span class="sxs-lookup"><span data-stu-id="5b349-135">region</span></span>   | <span data-ttu-id="5b349-136">sztring</span><span class="sxs-lookup"><span data-stu-id="5b349-136">string</span></span> | <span data-ttu-id="5b349-137">No</span><span class="sxs-lookup"><span data-stu-id="5b349-137">No</span></span>       | <span data-ttu-id="5b349-138">Opcionális kétbetűs ISO ország-vagy régiókód, amely azt jelzi, hogy az ajánlat melyik piacon vásárolható meg (például `FR` ).</span><span class="sxs-lookup"><span data-stu-id="5b349-138">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="5b349-139">Az alapértelmezett érték a partner profiljában beállított ország/régió kódja.</span><span class="sxs-lookup"><span data-stu-id="5b349-139">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="5b349-140">Ha az opcionális X-locale fejléc szerepel a kérelemben, annak értéke határozza meg a válaszban szereplő adatokhoz használt nyelvet.</span><span class="sxs-lookup"><span data-stu-id="5b349-140">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="5b349-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5b349-141">Request headers</span></span>

<span data-ttu-id="5b349-142">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5b349-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5b349-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5b349-143">Request body</span></span>

<span data-ttu-id="5b349-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="5b349-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5b349-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5b349-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5b349-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5b349-146">REST response</span></span>

<span data-ttu-id="5b349-147">Ha a kérelem sikeres, egy [Azure Rate Card](azure-rate-card-resources.md) -erőforrást ad vissza.</span><span class="sxs-lookup"><span data-stu-id="5b349-147">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5b349-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5b349-148">Response success and error codes</span></span>

<span data-ttu-id="5b349-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5b349-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5b349-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5b349-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5b349-151">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="5b349-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5b349-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5b349-152">Response example</span></span>

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
