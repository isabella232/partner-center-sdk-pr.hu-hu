---
title: Egy piac ajánlati listájának lekérése
description: Beolvas egy gyűjteményt, amely egy adott piac összes ajánlatát tartalmazza.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 3a004f6f8f8de8cd398d82c300793e4f196efaaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767947"
---
# <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="8364d-103">Egy piac ajánlati listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="8364d-103">Get a list of offers for a market</span></span>

<span data-ttu-id="8364d-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="8364d-104">**Applies To**</span></span>

- <span data-ttu-id="8364d-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8364d-105">Partner Center</span></span>
- <span data-ttu-id="8364d-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="8364d-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8364d-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8364d-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8364d-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8364d-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8364d-109">Beolvas egy gyűjteményt, amely egy adott piac összes ajánlatát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="8364d-109">Gets a collection that contains all the offers for a specific market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8364d-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8364d-110">Prerequisites</span></span>

- <span data-ttu-id="8364d-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="8364d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8364d-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="8364d-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="8364d-113">C\#</span><span class="sxs-lookup"><span data-stu-id="8364d-113">C\#</span></span>

<span data-ttu-id="8364d-114">Egy adott piacon elérhető ajánlatok listájának lekéréséhez használja a **IAggregatePartner. ajánlatok** gyűjteményét, válassza ki a piacot országonként, és hívja meg a **Get ()** vagy a **Get aszinkron ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="8364d-114">To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

<span data-ttu-id="8364d-115">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8364d-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8364d-116">**Projekt**: PartnerSDK. FeatureSample **osztály**: offers.cs</span><span class="sxs-lookup"><span data-stu-id="8364d-116">**Project**: PartnerSDK.FeatureSample **Class**: Offers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8364d-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="8364d-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8364d-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8364d-118">Request syntax</span></span>

| <span data-ttu-id="8364d-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="8364d-119">Method</span></span>  | <span data-ttu-id="8364d-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8364d-120">Request URI</span></span>                                                                          |
|---------|--------------------------------------------------------------------------------------|
| <span data-ttu-id="8364d-121">**GET**</span><span class="sxs-lookup"><span data-stu-id="8364d-121">**GET**</span></span> | <span data-ttu-id="8364d-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers? ország = {ország-azonosító} http/1.1</span><span class="sxs-lookup"><span data-stu-id="8364d-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="8364d-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="8364d-123">URI parameter</span></span>

<span data-ttu-id="8364d-124">Ez a táblázat felsorolja az ajánlatok beszerzéséhez szükséges lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="8364d-124">This table lists the required query parameters to get the offers.</span></span>

| <span data-ttu-id="8364d-125">Név</span><span class="sxs-lookup"><span data-stu-id="8364d-125">Name</span></span>           | <span data-ttu-id="8364d-126">Típus</span><span class="sxs-lookup"><span data-stu-id="8364d-126">Type</span></span>       | <span data-ttu-id="8364d-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8364d-127">Required</span></span> | <span data-ttu-id="8364d-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="8364d-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="8364d-129">**ország azonosítója**</span><span class="sxs-lookup"><span data-stu-id="8364d-129">**country-id**</span></span> | <span data-ttu-id="8364d-130">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="8364d-130">**string**</span></span> | <span data-ttu-id="8364d-131">Y</span><span class="sxs-lookup"><span data-stu-id="8364d-131">Y</span></span>        | <span data-ttu-id="8364d-132">Az ország/régió azonosítója.</span><span class="sxs-lookup"><span data-stu-id="8364d-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8364d-133">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8364d-133">Request headers</span></span>

- <span data-ttu-id="8364d-134">A rendszer karakterláncként formázott **területi beállítás** megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="8364d-134">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="8364d-135">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8364d-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8364d-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8364d-136">Request body</span></span>

<span data-ttu-id="8364d-137">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="8364d-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8364d-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8364d-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <a name="rest-response"></a><span data-ttu-id="8364d-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8364d-139">REST response</span></span>

<span data-ttu-id="8364d-140">Ha ez sikeres, a metódus a válasz törzsében adja vissza az **ajánlati** erőforrások gyűjteményét.</span><span class="sxs-lookup"><span data-stu-id="8364d-140">If successful, this method returns a collection of **Offer** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8364d-141">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8364d-141">Response success and error codes</span></span>

<span data-ttu-id="8364d-142">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="8364d-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8364d-143">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="8364d-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8364d-144">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8364d-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8364d-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8364d-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 26584
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
Date: Mon, 23 Nov 2015 23:20:44 GMT

{
    "totalCount":12,"items":[{
        "id":"E60E0348-1710-484B-992A-32B294D4CDE1",
        "name":"Azure Rights Management Premium (Government Pricing)",
        "description":"Microsoft Azure Rights Management Premium helps you protect confidential documents and email with strong encryption.
                       Control the use of your information by specifying who can view, edit, print, save and share your data.
                       Simple to use and integrated with Microsoft Office, SharePoint and Exchange.",
        "minimumQuantity":1,
        "maximumQuantity":10000000,
        "rank":5,
        "uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/E60E0348-1710-484B-992A-32B294D4CDE1",
        "locale":"EN-US",
        "country":"US",
        "category":{
            "id":"Government_Key",
            "name":"Government",
            "rank":40,
            "locale":"en-us",
            "country":"US",
            "attributes":{
                "objectType":"OfferCategory"
            }
        },
        "prerequisiteOffers":[],
        "isAddOn":false,
        "isAvailableForPurchase":true,
        "billing":"license",
        "isAutoRenewable":true,
        "product":{
            "id":"c52ea49f-fe5d-4e95-93ba-1de91d380f89",
            "name":"Azure Rights Management Premium",
            "unit":"Licenses"
        },
        "unitType":"Licenses",
        "links":{
            "learnMore":{
                "uri":"http://g.microsoftonline.com/0BXPS00en/0000",
                "method":"GET",
                "headers":[]
            },
            "self":{
                "uri":"/offers/E60E0348-1710-484B-992A-32B294D4CDE1",
                "method":"GET",
                "headers":[]
            }
        },
        "attributes":{
            "objectType":"Offer"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        },
        "previous":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
