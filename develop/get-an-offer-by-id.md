---
title: Ajánlat lekérése azonosító alapján
description: Az ajánlat-AZONOSÍTÓnak megfelelő ajánlat-erőforrás beolvasása.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: 9448276e817affb823eddabbcab8757c79615fbd
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768480"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="b9cb8-103">Ajánlat lekérése azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="b9cb8-103">Get an offer by ID</span></span>

<span data-ttu-id="b9cb8-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="b9cb8-104">**Applies To**</span></span>

- <span data-ttu-id="b9cb8-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b9cb8-105">Partner Center</span></span>
- <span data-ttu-id="b9cb8-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="b9cb8-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b9cb8-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b9cb8-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b9cb8-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b9cb8-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b9cb8-109">Beolvas egy **ajánlat** -erőforrást, amely megfelel az ajánlat azonosítójának.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-109">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9cb8-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b9cb8-110">Prerequisites</span></span>

- <span data-ttu-id="b9cb8-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b9cb8-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b9cb8-113">Egy ajánlat azonosítója.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-113">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="b9cb8-114">C\#</span><span class="sxs-lookup"><span data-stu-id="b9cb8-114">C\#</span></span>

<span data-ttu-id="b9cb8-115">Ha azonosító alapján szeretne megkeresni egy adott ajánlatot, használja a **IAggregatePartner. ajánlatok** gyűjteményét, hozza létre az országot a **ByCountry ()** hívásával, majd hívja meg a [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) metódust.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-115">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="b9cb8-116">Ezután hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) vagy a [**Get aszinkron ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-116">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="b9cb8-117">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b9cb8-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b9cb8-118">**Projekt**: PartnerSDK. FeatureSample **osztály**: GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="b9cb8-118">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="b9cb8-119">Java</span><span class="sxs-lookup"><span data-stu-id="b9cb8-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="b9cb8-120">Ha azonosító alapján szeretne megkeresni egy adott ajánlatot, használja a **IAggregatePartner. getOffers** függvényt, és hozza létre az országot a **byCountry ()** függvény hívásával, majd hívja meg a **byID ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-120">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="b9cb8-121">Ezután hívja meg a **Get ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-121">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="b9cb8-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9cb8-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="b9cb8-123">Ha azonosító alapján szeretne megkeresni egy adott ajánlatot, hajtsa végre a [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) parancsot, és határozza meg a **országhívószám** és a **OfferID** paramétert.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-123">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="b9cb8-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b9cb8-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b9cb8-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b9cb8-125">Request syntax</span></span>

| <span data-ttu-id="b9cb8-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="b9cb8-126">Method</span></span>  | <span data-ttu-id="b9cb8-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b9cb8-127">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b9cb8-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="b9cb8-128">**GET**</span></span> | <span data-ttu-id="b9cb8-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{Offer-ID}? ország = {ország-azonosító} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b9cb8-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b9cb8-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b9cb8-130">URI parameter</span></span>

| <span data-ttu-id="b9cb8-131">Név</span><span class="sxs-lookup"><span data-stu-id="b9cb8-131">Name</span></span>           | <span data-ttu-id="b9cb8-132">Típus</span><span class="sxs-lookup"><span data-stu-id="b9cb8-132">Type</span></span>       | <span data-ttu-id="b9cb8-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b9cb8-133">Required</span></span> | <span data-ttu-id="b9cb8-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="b9cb8-134">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="b9cb8-135">**ajánlat azonosítója**</span><span class="sxs-lookup"><span data-stu-id="b9cb8-135">**offer-id**</span></span>   | <span data-ttu-id="b9cb8-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="b9cb8-136">**guid**</span></span>   | <span data-ttu-id="b9cb8-137">Y</span><span class="sxs-lookup"><span data-stu-id="b9cb8-137">Y</span></span>        | <span data-ttu-id="b9cb8-138">Az ajánlatnak megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-138">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="b9cb8-139">**ország azonosítója**</span><span class="sxs-lookup"><span data-stu-id="b9cb8-139">**country-id**</span></span> | <span data-ttu-id="b9cb8-140">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="b9cb8-140">**string**</span></span> | <span data-ttu-id="b9cb8-141">Y</span><span class="sxs-lookup"><span data-stu-id="b9cb8-141">Y</span></span>        | <span data-ttu-id="b9cb8-142">Az ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-142">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="b9cb8-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b9cb8-143">Request headers</span></span>

- <span data-ttu-id="b9cb8-144">A rendszer karakterláncként formázott **területi beállítás** megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-144">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="b9cb8-145">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b9cb8-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b9cb8-146">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b9cb8-146">Request body</span></span>

<span data-ttu-id="b9cb8-147">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b9cb8-148">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b9cb8-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="b9cb8-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b9cb8-149">REST response</span></span>

<span data-ttu-id="b9cb8-150">Ha ez sikeres, ez a metódus egy **ajánlat** -erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-150">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b9cb8-151">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b9cb8-151">Response success and error codes</span></span>

<span data-ttu-id="b9cb8-152">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b9cb8-153">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b9cb8-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b9cb8-154">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b9cb8-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b9cb8-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b9cb8-155">Response example</span></span>

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
