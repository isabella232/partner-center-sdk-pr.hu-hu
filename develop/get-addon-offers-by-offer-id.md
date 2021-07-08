---
title: Bővítmények lekérése ajánlatazonosító alapján
description: Az ajánlatazonosító bővítményei lekérte.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e3b0ab8007d3affa6912479b960f6dae3bc0bd28
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760334"
---
# <a name="get-add-ons-for-an-offer-id"></a><span data-ttu-id="7af82-103">Bővítmények lekérése ajánlatazonosító alapján</span><span class="sxs-lookup"><span data-stu-id="7af82-103">Get add-ons for an offer ID</span></span>

<span data-ttu-id="7af82-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7af82-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7af82-105">Az ajánlatazonosító bővítményei lekérte.</span><span class="sxs-lookup"><span data-stu-id="7af82-105">How to get the add-ons for an offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7af82-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7af82-106">Prerequisites</span></span>

- <span data-ttu-id="7af82-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7af82-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7af82-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="7af82-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7af82-109">Egy ajánlatazonosító.</span><span class="sxs-lookup"><span data-stu-id="7af82-109">An offer ID.</span></span> <span data-ttu-id="7af82-110">Ha nem tudja az ajánlatazonosítót, tekintse meg a piaci ajánlatok [listájának lekért listáját.](get-a-list-of-offers-for-a-market.md)</span><span class="sxs-lookup"><span data-stu-id="7af82-110">If you don't have the offer ID, see [Get a list of offers for a market](get-a-list-of-offers-for-a-market.md).</span></span>

## <a name="c"></a><span data-ttu-id="7af82-111">C\#</span><span class="sxs-lookup"><span data-stu-id="7af82-111">C\#</span></span>

<span data-ttu-id="7af82-112">Egy ajánlat bővítményei azonosító alapján való lehíváshoz először hívja meg az [**IAggregatePartner.Offers.ByCountry**](/dotnet/api/microsoft.store.partnercenter.genericoperations.icountryselector-1.bycountry) metódust az országkóddal, hogy lekért egy felületet, amely az adott ország alapján kínál műveleteket.</span><span class="sxs-lookup"><span data-stu-id="7af82-112">To get the add-ons for an offer by ID, first call the [**IAggregatePartner.Offers.ByCountry**](/dotnet/api/microsoft.store.partnercenter.genericoperations.icountryselector-1.bycountry) method with the country code to get an interface to offer operations based on the given country.</span></span> <span data-ttu-id="7af82-113">Ezután hívja meg [**a ByID**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) metódust az ajánlat azonosítójával annak az ajánlatnak az azonosításához, amelynek bővítményét le szeretné hívni.</span><span class="sxs-lookup"><span data-stu-id="7af82-113">Then call the [**ByID**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method with the offer ID to identify the offer whose add-ons you want to retrieve.</span></span> <span data-ttu-id="7af82-114">Ezután az [**AddOns**](/dotnet/api/microsoft.store.partnercenter.offers.ioffer.addons) tulajdonság használatával lekért egy interfészt az aktuális ajánlat bővítményműveleteihez.</span><span class="sxs-lookup"><span data-stu-id="7af82-114">Next, use the [**AddOns**](/dotnet/api/microsoft.store.partnercenter.offers.ioffer.addons) property to get an interface to add-on operations for the current offer.</span></span> <span data-ttu-id="7af82-115">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.getasync) metódust a megadott ajánlat összes bővítményének gyűjteményéhez.</span><span class="sxs-lookup"><span data-stu-id="7af82-115">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.offers.iofferaddons.getasync) method to get a collection of all the add-ons for the specified offer.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string offerId;
// string countryCode;

var offerAddOns = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).AddOns.Get();
```

<span data-ttu-id="7af82-116">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7af82-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7af82-117">**Project**: Partnerközpont SDK **Osztály:** GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="7af82-117">**Project**: Partner Center SDK Samples **Class**: GetOffer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7af82-118">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="7af82-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7af82-119">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="7af82-119">Request syntax</span></span>

| <span data-ttu-id="7af82-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="7af82-120">Method</span></span>  | <span data-ttu-id="7af82-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7af82-121">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7af82-122">**Kap**</span><span class="sxs-lookup"><span data-stu-id="7af82-122">**GET**</span></span> | <span data-ttu-id="7af82-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{ajánlatazonosító}/addons?country={országkód} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7af82-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}/addons?country={country-code} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="7af82-124">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7af82-124">URI parameters</span></span>

<span data-ttu-id="7af82-125">A következő paraméterekkel használhatja az ajánlat azonosítóját és országkódját.</span><span class="sxs-lookup"><span data-stu-id="7af82-125">Use the following parameters to provide the offer ID and country code.</span></span>

| <span data-ttu-id="7af82-126">Név</span><span class="sxs-lookup"><span data-stu-id="7af82-126">Name</span></span>         | <span data-ttu-id="7af82-127">Típus</span><span class="sxs-lookup"><span data-stu-id="7af82-127">Type</span></span>       | <span data-ttu-id="7af82-128">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7af82-128">Required</span></span> | <span data-ttu-id="7af82-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="7af82-129">Description</span></span>                       |
|--------------|------------|----------|-----------------------------------|
| <span data-ttu-id="7af82-130">**ajánlatazonosító**</span><span class="sxs-lookup"><span data-stu-id="7af82-130">**offer-id**</span></span> | <span data-ttu-id="7af82-131">**guid**</span><span class="sxs-lookup"><span data-stu-id="7af82-131">**guid**</span></span>   | <span data-ttu-id="7af82-132">Y</span><span class="sxs-lookup"><span data-stu-id="7af82-132">Y</span></span>        | <span data-ttu-id="7af82-133">Az ajánlatot azonosító GUID.</span><span class="sxs-lookup"><span data-stu-id="7af82-133">A GUID that identifies the offer.</span></span> |
| <span data-ttu-id="7af82-134">**Ország**</span><span class="sxs-lookup"><span data-stu-id="7af82-134">**country**</span></span>  | <span data-ttu-id="7af82-135">**sztring**</span><span class="sxs-lookup"><span data-stu-id="7af82-135">**string**</span></span> | <span data-ttu-id="7af82-136">Y</span><span class="sxs-lookup"><span data-stu-id="7af82-136">Y</span></span>        | <span data-ttu-id="7af82-137">Az országkód (például `US` ).</span><span class="sxs-lookup"><span data-stu-id="7af82-137">The country code (for example `US`).</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="7af82-138">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7af82-138">Request headers</span></span>

<span data-ttu-id="7af82-139">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7af82-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7af82-140">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7af82-140">Request body</span></span>

<span data-ttu-id="7af82-141">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7af82-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7af82-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7af82-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/195416C1-3447-423A-B37B-EE59A99A19C4/addons?country=us HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c15e829e-ecc7-42c2-8a4b-5e6961f4e3f8
MS-CorrelationId: 26d2b3b1-c76a-4aeb-8298-1654c91d9eb8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7af82-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7af82-143">REST response</span></span>

<span data-ttu-id="7af82-144">Ha a művelet sikeres, ez a metódus ajánlatobjektumok [gyűjteményét](offer-resources.md) adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="7af82-144">If successful, this method returns a collection of [Offer](offer-resources.md) objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7af82-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7af82-145">Response success and error codes</span></span>

<span data-ttu-id="7af82-146">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="7af82-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7af82-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="7af82-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7af82-148">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7af82-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7af82-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7af82-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3137
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 26d2b3b1-c76a-4aeb-8298-1654c91d9eb8
MS-RequestId: c15e829e-ecc7-42c2-8a4b-5e6961f4e3f8
MS-CV: P8xjUcSeY0ithZ9S.0
MS-ServerId: 202010406
Date: Wed, 01 Feb 2017 22:37:58 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "name": "Exchange Online Archiving for Exchange Online",
            "description": "A personal e-mail archive for users who have mailboxes on Exchange Server 2010 or later.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 200,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "locale": "en-US",
            "country": "US",
            "category": {
                "id": "",
                "name": "",
                "rank": 0,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": ["35A36B80-270A-44BF-9290-00545D350866", "6FBAD345-B7DE-42A6-B6AB-79B363D0B371", "91FD106F-4B2C-4938-95AC-F54F74E9A239", "195416C1-3447-423A-B37B-EE59A99A19C4", "22A70120-4078-4926-9592-39ED91CB9C01", "2A727AE4-F201-497D-A9D6-C6A892DF4A87", "BD938F12-058F-4927-BBA3-AE36B1D2501C", "031C9E47-4802-4248-838E-778FB1D2CC05", "B2016E73-D9AD-4758-B8B8-D5C001BDF411", "AA98032C-5403-472F-B24F-F6654846B15D"],
            "isAddOn": true,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "salesGroupId": "1",
            "product": {
                "id": "EE02FD1B-340E-4A4B-B355-4A514E4C8943",
                "name": "Exchange Online Archiving for Exchange Online",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "uri": "http://g.microsoftonline.com/0BXPS00en-us/1302",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/2828BE95-46BA-4F91-B2FD-0BEF192ECF60?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        }, {
            "id": "45320EC9-9B8E-49D0-B900-F14141A0ABD1",
            "name": "Microsoft MyAnalytics",
            "description": "Microsoft MyAnalytics provides insights about time and relationships to help individuals and teams achieve more at work.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 232,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/45320EC9-9B8E-49D0-B900-F14141A0ABD1",
            "locale": "en-US",
            "country": "US",
            "category": {
                "id": "",
                "name": "",
                "rank": 0,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": ["195416C1-3447-423A-B37B-EE59A99A19C4", "2F707C7C-2433-49A5-A437-9CA7CF40D3EB", "91FD106F-4B2C-4938-95AC-F54F74E9A239", "796B6B5F-613C-4E24-A17C-EBA730D49C02", "8909E28E-5832-42F4-9886-B0A5545F3645", "2B3B8D2D-10AA-4BE4-B5FD-7F2FEB0C3091"],
            "isAddOn": true,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "salesGroupId": "1",
            "product": {
                "id": "90A8F363-DA30-4ECD-90A7-D3A6B203486D",
                "name": "Microsoft MyAnalytics",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/45320EC9-9B8E-49D0-B900-F14141A0ABD1?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
