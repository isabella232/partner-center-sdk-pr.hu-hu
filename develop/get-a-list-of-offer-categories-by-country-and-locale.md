---
title: Ajánlatkategóriák listájának lekérése piac alapján
description: Megtudhatja, hogyan szerezhet be egy olyan gyűjteményt, amely az adott országban/régióban található összes ajánlatot tartalmazza, és az összes Microsoft-felhőre vonatkozó területi beállítással rendelkezik.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 05aad095c6cb8eaee4cbf7ce976ca1b4b7a408c4
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500056"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Ajánlatkategóriák listájának lekérése piac alapján

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett Partnerközpont
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ez a cikk azt ismerteti, hogyan szerezhet be egy olyan gyűjteményt, amely az adott országban/régióban és területi beállításban szereplő összes ajánlati kategóriát tartalmazza.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

## <a name="c"></a>C\#

Az ajánlati kategóriák listájának lekérése egy adott országban/régióban és területi beállításban:

1. A [**IAggregatePartner. Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) gyűjtemény használatával hívja meg a [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) metódust egy adott környezetben.

2. Vizsgálja meg az eredményül kapott objektum [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) tulajdonságát.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

Példaként tekintse meg a következőket:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **PartnerSDK. FeatureSample**
- Osztály: **PartnerSDK. FeatureSample**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories? ország = {ország-azonosító} http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az ajánlati kategóriák beszerzéséhez.

| Név           | Típus       | Kötelező | Leírás            |
|----------------|------------|----------|------------------------|
| **ország azonosítója** | **sztring** | Y        | Az ország/régió azonosítója. |

### <a name="request-headers"></a>Kérésfejlécek

A rendszer karakterláncként formázott **területi beállítás** megadása kötelező.

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus **OfferCategory** -erőforrások gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
