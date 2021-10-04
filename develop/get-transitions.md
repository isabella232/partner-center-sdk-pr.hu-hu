---
title: Lekért korábbi váltási előzmények egy korábban áttért új kereskedelmi előfizetéshez
description: Lekérte egy korábban áttért új kereskedelmi előfizetés áttűnéselőzményét.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 65859e0805397efb0c9db2f5bf566ca1b6deba49
ms.sourcegitcommit: 3ee00d9fe9da6b9df0fb7027ae506e2abe722770
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/04/2021
ms.locfileid: "129417270"
---
# <a name="get-transitions"></a>Áttűnések lekért

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi módosítások jelenleg csak az M365/D365 új kereskedelmi felhasználói élmény technikai előzetes kiadásának partnerei számára érhetők el.

Egy adott ügyfél és előfizetés áttérési előzményeinek lekért előzményeit lekértük. Az előzmények tartalmazzák az átváltáshoz feldolgozott összes eseményt. Ez csak az új kereskedelmi licencalapú előfizetés-váltásokat támogatja.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító az áttűnött előfizetéshez.

## <a name="rest-request"></a>REST-kérés
[GET] customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitions
### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **KAP**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/transitions HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterekkel jogosult átmeneteket ad vissza.

| Név                    | Típus     | Kötelező | Leírás                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **guid** | Y        | Az ügyfél bérlőjéhez tartozó GUID.             |
| **subscription-id** | **guid** | Y        | A kezdeti előfizetésnek megfelelő GUID. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/transitions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a megadott előfizetésre vonatkozó váltások előzményeit adja vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "transition": [
        {
        "FromCatalogItemId": "CFQ7TTC0LDPB:0001:CFQ7TTC0LGNT",
        "ToCatalogItemId": "CFQ7TTC0LF8S:0001:CFQ7TTC0K9G9",
        "quantity": 1,
        "transitionType": "transition_with_license_transfer",
        "Events": [
           {
               "name": "Conversion",
               "status": "Started ",
               "timestamp": "2021-01-08T18:01:14.7488618Z",
               "attributes":
                     {
                          "objectType": "TransitionEvent"
                     }
           }, 
           {
               "name": "Conversion",
               "status": "Completed",
               "timestamp": "2021-01-08T18:37:41.591855Z",
               "attributes":
                     {
                          "objectType": "TransitionEvent"
                     }
            }
        ],
        "attributes":
               {
                     "objectType": "Transition"
               }
        }
    ],
    "attributes":
        {
               "objectType": "Collection"
        }
}
```

