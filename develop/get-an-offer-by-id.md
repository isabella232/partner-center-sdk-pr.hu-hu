---
title: Ajánlat lekérése azonosító alapján
description: Lekért egy ajánlat-erőforrást, amely megfelel az ajánlat azonosítójának.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: f759cbdeefb4f550c41b41de40e9979e72e4ddeb
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760640"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="6437a-103">Ajánlat lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="6437a-103">Get an offer by ID</span></span>

<span data-ttu-id="6437a-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6437a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6437a-105">Lekért **egy ajánlat-erőforrást,** amely megfelel az ajánlat azonosítójának.</span><span class="sxs-lookup"><span data-stu-id="6437a-105">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6437a-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6437a-106">Prerequisites</span></span>

- <span data-ttu-id="6437a-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6437a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6437a-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="6437a-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6437a-109">Egy ajánlatazonosító.</span><span class="sxs-lookup"><span data-stu-id="6437a-109">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="6437a-110">C\#</span><span class="sxs-lookup"><span data-stu-id="6437a-110">C\#</span></span>

<span data-ttu-id="6437a-111">Ha azonosító alapján keres egy adott ajánlatot, használja az **IAggregatePartner.Offers** gyűjteményt, hozza létre az országot a **ByCountry()** hívásával, majd hívja meg a [**ByID() metódust.**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid)</span><span class="sxs-lookup"><span data-stu-id="6437a-111">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="6437a-112">Ezután hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) [**a Get Async() metódust.**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="6437a-112">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="6437a-113">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="6437a-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6437a-114">**Project**: PartnerSDK.FeatureSample **osztály:** GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="6437a-114">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="6437a-115">Java</span><span class="sxs-lookup"><span data-stu-id="6437a-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="6437a-116">Ha azonosító alapján keres egy adott ajánlatot, használja az **IAggregatePartner.getOffers** függvényt, hozza létre az országot a **byCountry()** függvény hívásával, majd hívja meg a **byID()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="6437a-116">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="6437a-117">Ezután hívja meg a **get()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="6437a-117">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="6437a-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6437a-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="6437a-119">Ha azonosító alapján keres egy adott ajánlatot, hajtsa végre a [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) parancsot, és adja meg a **CountryCode** és **az OfferId paramétereket.**</span><span class="sxs-lookup"><span data-stu-id="6437a-119">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="6437a-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="6437a-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6437a-121">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6437a-121">Request syntax</span></span>

| <span data-ttu-id="6437a-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="6437a-122">Method</span></span>  | <span data-ttu-id="6437a-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6437a-123">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6437a-124">**Kap**</span><span class="sxs-lookup"><span data-stu-id="6437a-124">**GET**</span></span> | <span data-ttu-id="6437a-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{ajánlatazonosító}?country={országazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6437a-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6437a-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="6437a-126">URI parameter</span></span>

| <span data-ttu-id="6437a-127">Név</span><span class="sxs-lookup"><span data-stu-id="6437a-127">Name</span></span>           | <span data-ttu-id="6437a-128">Típus</span><span class="sxs-lookup"><span data-stu-id="6437a-128">Type</span></span>       | <span data-ttu-id="6437a-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6437a-129">Required</span></span> | <span data-ttu-id="6437a-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="6437a-130">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="6437a-131">**ajánlatazonosító**</span><span class="sxs-lookup"><span data-stu-id="6437a-131">**offer-id**</span></span>   | <span data-ttu-id="6437a-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="6437a-132">**guid**</span></span>   | <span data-ttu-id="6437a-133">Y</span><span class="sxs-lookup"><span data-stu-id="6437a-133">Y</span></span>        | <span data-ttu-id="6437a-134">Az ajánlatnak megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="6437a-134">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="6437a-135">**country-id (országazonosító)**</span><span class="sxs-lookup"><span data-stu-id="6437a-135">**country-id**</span></span> | <span data-ttu-id="6437a-136">**sztring**</span><span class="sxs-lookup"><span data-stu-id="6437a-136">**string**</span></span> | <span data-ttu-id="6437a-137">Y</span><span class="sxs-lookup"><span data-stu-id="6437a-137">Y</span></span>        | <span data-ttu-id="6437a-138">Az ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="6437a-138">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="6437a-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6437a-139">Request headers</span></span>

- <span data-ttu-id="6437a-140">Szükség **van egy sztringként** formázott területi azonosítóra.</span><span class="sxs-lookup"><span data-stu-id="6437a-140">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="6437a-141">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6437a-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6437a-142">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6437a-142">Request body</span></span>

<span data-ttu-id="6437a-143">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="6437a-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6437a-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6437a-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="6437a-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6437a-145">REST response</span></span>

<span data-ttu-id="6437a-146">Ha sikeres, ez a metódus egy **Offer (Ajánlat) erőforrást** ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="6437a-146">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6437a-147">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6437a-147">Response success and error codes</span></span>

<span data-ttu-id="6437a-148">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="6437a-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6437a-149">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="6437a-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6437a-150">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6437a-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6437a-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6437a-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    "prerequisiteOffers": [],
    "isAddOn": false,
    "isAvailableForPurchase": true,
    "billing": "license",
    "isAutoRenewable": true,
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
