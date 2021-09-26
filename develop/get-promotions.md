---
title: Lekért egy adott szegmensre és piacra vonatkozó aktuális promóciók listáját
description: Lekérte az adott szegmensre és piacra vonatkozó aktuális promóciók listáját.
ms.date: 09/24/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 0b9cc6ccdebbd641ab8b7dcd6cc5932c191d85ad
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/24/2021
ms.locfileid: "128715989"
---
# <a name="get-promotions"></a>Promóciók lekértése

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi változások jelenleg csak a Microsoft 365 és a Dynamics 365 új kereskedelmi felhasználói élményének technikai előzetesében lévő partnerek számára érhetők el.

A partnerek lekértheti egy adott piac (ország) és szegmens aktív új kereskedelmi promócióit. Ez a metódus az elérhető promóciók kezdő és záró dátuma alapján adja vissza az elérhető promóciókat.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- A szegmens azt az ügyféltípust jelöli, aki számára az előléptetések engedélyezve vannak. Jelenleg csak a kereskedelmi használatot támogatja.

- Az Ország az ügyfél országának promócióit jelöli, amelyekhez elérhetők. Az országot egy két karakterből áll országkód képviseli.

## <a name="rest-request"></a>REST-kérés
[GET] /v1/productpromotions?country={country-code}&segment={segment}

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **KAP**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions?country={országkód}&segment={segment} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az elérhető promóciók visszaadása érdekében használja az alábbi lekérdezési paramétereket.

| Név                    | Típus     | Kötelező | Leírás                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Szegmens**  | **sztring** | Y        | Egy sztring, amely meghatározza, hogy mely promóciók érhetők el egy adott szegmenshez.           |
| **Ország** | **sztring** | Y        | Kétbetűs országkód, amely meghatározza, hogy mely ügyfél országának előléptetései érhetők el. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions?country=US&segment=commercial HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén ez a metódus az előléptetések listáját adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely sikeres vagy sikertelen állapotot jelez, valamint további hibakeresési információkat tartalmaz. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT


{
    "totalCount": 2,
    "items": [
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
        },
        {
            "id": "39NFJQT1PJQC:0001:39NFJQT1Q5KM",
            "name": "Vision Plan 1",
            "description": "Vision Plan 1",
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
                        "billingCycle": "Monthly"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.167"
                        }
                    ]
                }
            ]
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
