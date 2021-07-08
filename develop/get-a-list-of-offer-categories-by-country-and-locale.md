---
title: Ajánlatkategóriák listájának lekérése piac alapján
description: Megtudhatja, hogyan szerez be egy olyan gyűjteményt, amely az összes ajánlatkategóriát tartalmazza egy adott országban/régióban és területi adatokat az összes Microsoft-felhőhöz.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e699355f07dda3941eafed32f5f635d94000abd1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874278"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Ajánlatkategóriák listájának lekérése piac alapján

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ez a cikk azt ismerteti, hogyan lehet egy adott ország/régió és területi terület összes ajánlatkategóriáját tartalmazó gyűjteményt lekért.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Egy adott ország/régió és területi terület ajánlatkategóriái listájának lekért listája:

1. Az [**IAggregatePartner.Operations gyűjtemény**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) használatával hívja meg az [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) metódust egy adott környezetben.

2. Vizsgálja meg az eredményül kapott objektum [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) tulajdonságát.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

Példaként tekintse meg a következőket:

- Minta: [Konzoltesztalkalmazás](console-test-app.md)
- Project: **PartnerSDK.FeatureSample**
- Osztály: **PartnerSDK.FeatureSample**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az ajánlatkategóriák lekérdezhető lekérdezési paramétereit.

| Név           | Típus       | Kötelező | Leírás            |
|----------------|------------|----------|------------------------|
| **country-id (országazonosító)** | **sztring** | Y        | Az ország/régió azonosítója. |

### <a name="request-headers"></a>Kérésfejlécek

Szükség **van egy sztringként** formázott területi azonosítóra.

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha a művelet sikeres, ez a metódus **OfferCategory-erőforrások** gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
