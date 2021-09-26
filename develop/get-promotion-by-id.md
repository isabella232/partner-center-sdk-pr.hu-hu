---
title: Egyetlen előléptetést kap
description: Egyetlen előléptetést kap egy adott előléptetési azonosítóra és országra.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 9ed9171cd7bbe8a6d5202deb7cc6111bb76ec923
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715996"
---
# <a name="get-promotion-by-id"></a>Előléptetés lekért azonosítója alapján

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi módosítások jelenleg csak a Microsoft 365 és a Dynamics 365 új kereskedelmi felhasználói élményének technikai előzetesében található partnerek számára érhetők el.

A partnerek egyetlen előléptetést kaphatnak egy adott előléptetési azonosítóra és országra. Ez a metódus az előléptetési adatokat adja vissza, figyelmen kívül hagyva az előléptetés kezdő és záró dátumát. Ez a módszer elsősorban egyeztetési célokra szolgál az előléptetési adatok lekéréséhez, még az előléptetés lejárta után is.



## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Az előléptetési azonosító egy adott előléptetést képviselő sztringek tagolt készlete.

- Az Ország az ügyfél országának promócióit jelöli, amelyekhez elérhetők. Az országot egy két karakterből áll országkód képviseli.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **KAP**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions/{promotion-id}?country={country-code HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az elérhető promóciók visszaadása érdekében használja az alábbi lekérdezési paramétereket.

| Név                    | Típus     | Kötelező | Leírás                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **promotion-id**  | **sztring** | Y        | A lekérni való előléptetést meghatározó sztring.           |
| **Ország** | **sztring** | Y        | Kétbetűs országkód, amely meghatározza, hogy mely ügyfél országának előléptetései érhetők el. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions/CFQ7TTC0HD33:0003:CFQ7TTC0K59M?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egyetlen előléptetést ad vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely sikeres vagy sikertelen állapotot jelez, valamint további hibakeresési információkat tartalmaz. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 24 Sep 2021 20:42:26 GMT

 
        {
            "id": "39NFJQT1PJQB:0001:39NFJQT1Q5KN",
            "name": "Visio Plan 1",
            "description": "Visio Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Annual"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.05"
                        }
                    ]
                }
            ]
        }
```
