---
title: Ajánlat lekérése azonosító alapján
description: Lekért egy ajánlat-erőforrást, amely megfelel az ajánlat azonosítójának.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: a57f3715a7c2738e74fc406ed834981b208fb0ab14a228db8756f5c4b1e32281
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990851"
---
# <a name="get-an-offer-by-id"></a>Ajánlat lekérése azonosító alapján

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekért **egy ajánlat-erőforrást,** amely megfelel az ajánlat azonosítójának.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.

- Egy ajánlatazonosító.

## <a name="c"></a>C\#

Ha azonosító alapján keres egy adott ajánlatot, használja az **IAggregatePartner.Offers** gyűjteményt, hozza létre az országot a **ByCountry()** hívásával, majd hívja meg a [**ByID() metódust.**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) Ezután hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) [**a Get Async() metódust.**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync)

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: PartnerSDK.FeatureSample **osztály:** GetOffer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Ha azonosító alapján keres egy adott ajánlatot, használja az **IAggregatePartner.getOffers** függvényt, hozza létre az országot a **byCountry()** függvény hívásával, majd hívja meg a **byID()** függvényt. Ezután hívja meg a **get()** függvényt.

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Ha azonosító alapján keres egy adott ajánlatot, hajtsa végre a [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) parancsot, és adja meg a **CountryCode** és **az OfferId paramétereket.**

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{ajánlatazonosító}?country={országazonosító} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

| Név           | Típus       | Kötelező | Leírás                           |
|----------------|------------|----------|---------------------------------------|
| **ajánlatazonosító**   | **guid**   | Y        | Az ajánlatnak megfelelő GUID. |
| **country-id (országazonosító)** | **sztring** | Y        | Az ország/régió azonosítója.                |

### <a name="request-headers"></a>Kérésfejlécek

- Szükség **van egy sztringként** formázott területi azonosítóra.
További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha a művelet sikeres, ez a metódus egy **Offer (Ajánlat) erőforrást** ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
