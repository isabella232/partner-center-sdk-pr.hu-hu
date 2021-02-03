---
title: Címformázási szabályok lekérése piac alapján
description: Szerezze be a várt címformátum-formátumot a piac ISO-kódja alapján.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c755a38c11ed9803edb7777a0f661c1fbc5a6107
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767879"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="52d07-103">Címformázási szabályok lekérése piac alapján</span><span class="sxs-lookup"><span data-stu-id="52d07-103">Get address formatting rules by market</span></span>

<span data-ttu-id="52d07-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="52d07-104">**Applies To**</span></span>

- <span data-ttu-id="52d07-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="52d07-105">Partner Center</span></span>
- <span data-ttu-id="52d07-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="52d07-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="52d07-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="52d07-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="52d07-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="52d07-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="52d07-109">Szerezze be a várt címformátum-formátumot a piac ISO-kódja alapján.</span><span class="sxs-lookup"><span data-stu-id="52d07-109">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52d07-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="52d07-110">Prerequisites</span></span>

- <span data-ttu-id="52d07-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="52d07-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="52d07-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="52d07-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="52d07-113">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="52d07-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="52d07-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="52d07-114">Request syntax</span></span>

| <span data-ttu-id="52d07-115">Metódus</span><span class="sxs-lookup"><span data-stu-id="52d07-115">Method</span></span>  | <span data-ttu-id="52d07-116">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="52d07-116">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="52d07-117">**GET**</span><span class="sxs-lookup"><span data-stu-id="52d07-117">**GET**</span></span> | <span data-ttu-id="52d07-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="52d07-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="52d07-119">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="52d07-119">URI parameter</span></span>

| <span data-ttu-id="52d07-120">Név</span><span class="sxs-lookup"><span data-stu-id="52d07-120">Name</span></span>           | <span data-ttu-id="52d07-121">Típus</span><span class="sxs-lookup"><span data-stu-id="52d07-121">Type</span></span>       | <span data-ttu-id="52d07-122">Kötelező</span><span class="sxs-lookup"><span data-stu-id="52d07-122">Required</span></span> | <span data-ttu-id="52d07-123">Leírás</span><span class="sxs-lookup"><span data-stu-id="52d07-123">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="52d07-124">**isocode-azonosító**</span><span class="sxs-lookup"><span data-stu-id="52d07-124">**isocode-id**</span></span> | <span data-ttu-id="52d07-125">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="52d07-125">**string**</span></span> | <span data-ttu-id="52d07-126">Y</span><span class="sxs-lookup"><span data-stu-id="52d07-126">Y</span></span>        | <span data-ttu-id="52d07-127">A két karakterből álló ISO-országkód.</span><span class="sxs-lookup"><span data-stu-id="52d07-127">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="52d07-128">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="52d07-128">Request headers</span></span>

<span data-ttu-id="52d07-129">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="52d07-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="52d07-130">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="52d07-130">Request body</span></span>

<span data-ttu-id="52d07-131">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="52d07-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="52d07-132">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="52d07-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="52d07-133">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="52d07-133">REST response</span></span>

<span data-ttu-id="52d07-134">Ha ez sikeres, ez a metódus egy **CountryInformation** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="52d07-134">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="52d07-135">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="52d07-135">Response success and error codes</span></span>

<span data-ttu-id="52d07-136">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="52d07-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="52d07-137">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="52d07-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="52d07-138">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="52d07-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="52d07-139">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="52d07-139">Response example</span></span>

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
