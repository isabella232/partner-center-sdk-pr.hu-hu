---
title: Címformázási szabályok lekérése piac alapján
description: A piac iso-kódja alapján szerezze be a várt címformátumot.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5233d059ea6e71c28df36b2242659c28c5dd857
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549042"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="65813-103">Címformázási szabályok lekérése piac alapján</span><span class="sxs-lookup"><span data-stu-id="65813-103">Get address formatting rules by market</span></span>

<span data-ttu-id="65813-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="65813-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>


<span data-ttu-id="65813-105">A piac iso-kódja alapján szerezze be a várt címformátumot.</span><span class="sxs-lookup"><span data-stu-id="65813-105">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65813-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="65813-106">Prerequisites</span></span>

- <span data-ttu-id="65813-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="65813-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="65813-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="65813-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="65813-109">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="65813-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="65813-110">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="65813-110">Request syntax</span></span>

| <span data-ttu-id="65813-111">Metódus</span><span class="sxs-lookup"><span data-stu-id="65813-111">Method</span></span>  | <span data-ttu-id="65813-112">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="65813-112">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="65813-113">**Kap**</span><span class="sxs-lookup"><span data-stu-id="65813-113">**GET**</span></span> | <span data-ttu-id="65813-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="65813-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="65813-115">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="65813-115">URI parameter</span></span>

| <span data-ttu-id="65813-116">Név</span><span class="sxs-lookup"><span data-stu-id="65813-116">Name</span></span>           | <span data-ttu-id="65813-117">Típus</span><span class="sxs-lookup"><span data-stu-id="65813-117">Type</span></span>       | <span data-ttu-id="65813-118">Kötelező</span><span class="sxs-lookup"><span data-stu-id="65813-118">Required</span></span> | <span data-ttu-id="65813-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="65813-119">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="65813-120">**isocode-id**</span><span class="sxs-lookup"><span data-stu-id="65813-120">**isocode-id**</span></span> | <span data-ttu-id="65813-121">**sztring**</span><span class="sxs-lookup"><span data-stu-id="65813-121">**string**</span></span> | <span data-ttu-id="65813-122">Y</span><span class="sxs-lookup"><span data-stu-id="65813-122">Y</span></span>        | <span data-ttu-id="65813-123">A két karakterből áll ISO országkód.</span><span class="sxs-lookup"><span data-stu-id="65813-123">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="65813-124">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="65813-124">Request headers</span></span>

<span data-ttu-id="65813-125">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="65813-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="65813-126">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="65813-126">Request body</span></span>

<span data-ttu-id="65813-127">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="65813-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="65813-128">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="65813-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="65813-129">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="65813-129">REST response</span></span>

<span data-ttu-id="65813-130">Ha sikeres, ez a metódus egy **CountryInformation** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="65813-130">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="65813-131">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="65813-131">Response success and error codes</span></span>

<span data-ttu-id="65813-132">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="65813-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="65813-133">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="65813-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="65813-134">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="65813-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="65813-135">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="65813-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1856
Content-Type: application/json
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
Date: Wed, 25 Nov 2015 06:36:47 GMT

{
    "iso2Code": "US",
    "defaultCulture": "en-US",
    "isStateRequired": true,
    "states": {
        "value": ["AK","AL","AR", "AZ","CA","CO","CT","DC","DE","FL","GA","HI","IA","ID","IL","IN",
        "KS","KY","LA","MA","MD","ME","MI","MN","MO","MS","MT","NC","ND","NE","NH","NJ","NM","NV",
        "NY","OH","OK","OR","PA","RI","SC","SD","TN","TX","UT","VA","VT","WA","WI","WV","WY"]
    },
    "supportedLanguages": {
        "value": ["en",
        "es"]
    },
    "supportedCultures": {
        "value": ["en-US",
        "es-US"]
    },
    "isPostalCodeRequired": true,
    "postalCodeRegex": "^\\d{
        5
    }(-\\d{
        4
    })?$",
    "isCityRequired": true,
    "isVatIdSupported": false,
    "taxIdFormat": "US######",
    "taxIdSample": "US999965",
    "phoneNumberRegex": "^(1[\\-\\/\\.]?)?(\((\\d{3})\)|(\\d{3}))[\\-\\/\\.]?(\\d{3})[\\-\\/\\.]?(\\d{4})$",
    "isRegistrationNumberSupported": false,
    "isTaxIdSupported": true,
    "resellerAgreementRegion": "AOC",
    "geographicRegion": "NorthAndLatinAmerica",
    "countryCallingCodes": {
        "value": ["1"]
    },
    "attributes": {
        "objectType": "CountryInformation"
    }
}
```
