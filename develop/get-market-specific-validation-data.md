---
title: Címformázási szabályok lekérése piac alapján
description: A piac ISO-kódja alapján szerezze be a várt címformátumot.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1e5c3b0b4a8f57a3731392bfa13d9da22c66699d5dedd4da48aa7f93b5700fd
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995883"
---
# <a name="get-address-formatting-rules-by-market"></a>Címformázási szabályok lekérése piac alapján

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government


A piac ISO-kódja alapján szerezze be a várt címformátumot.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

| Név           | Típus       | Kötelező | Leírás                         |
|----------------|------------|----------|-------------------------------------|
| **isocode-id** | **sztring** | Y        | A két karakterből áll ISO országkód. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy **CountryInformation** objektumot ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

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
