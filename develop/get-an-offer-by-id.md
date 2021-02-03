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
# <a name="get-an-offer-by-id"></a>Ajánlat lekérése azonosító alapján

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Beolvas egy **ajánlat** -erőforrást, amely megfelel az ajánlat azonosítójának.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy ajánlat azonosítója.

## <a name="c"></a>C\#

Ha azonosító alapján szeretne megkeresni egy adott ajánlatot, használja a **IAggregatePartner. ajánlatok** gyűjteményét, hozza létre az országot a **ByCountry ()** hívásával, majd hívja meg a [**ByID ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) metódust. Ezután hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) vagy a [**Get aszinkron ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) metódust.

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample **osztály**: GetOffer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Ha azonosító alapján szeretne megkeresni egy adott ajánlatot, használja a **IAggregatePartner. getOffers** függvényt, és hozza létre az országot a **byCountry ()** függvény hívásával, majd hívja meg a **byID ()** függvényt. Ezután hívja meg a **Get ()** függvényt.

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Ha azonosító alapján szeretne megkeresni egy adott ajánlatot, hajtsa végre a [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) parancsot, és határozza meg a **országhívószám** és a **OfferID** paramétert.

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{Offer-ID}? ország = {ország-azonosító} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

| Név           | Típus       | Kötelező | Leírás                           |
|----------------|------------|----------|---------------------------------------|
| **ajánlat azonosítója**   | **guid**   | Y        | Az ajánlatnak megfelelő GUID. |
| **ország azonosítója** | **karakterlánc** | Y        | Az ország/régió azonosítója.                |

### <a name="request-headers"></a>Kérésfejlécek

- A rendszer karakterláncként formázott **területi beállítás** megadása kötelező.
További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus egy **ajánlat** -erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

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
