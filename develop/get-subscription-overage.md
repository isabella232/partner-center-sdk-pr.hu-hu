---
title: Lekért egy adott ügyfél túlóraállapotát
description: Lekérte egy adott ügyfél túlóraállapotát.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 8dabd811c61583a38f832eae54ce92402bfb5c29
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/02/2021
ms.locfileid: "129383443"
---
# <a name="get-overage"></a>Túlóra lekért

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi módosítások jelenleg csak azok számára érhetők el, akik a Microsoft 365/Dynamics 365 új kereskedelmi felhasználói élményének technikai előzetes verziója részét képezi.

Egy adott ügyfél túlóra-behozáshoz használatos. A túlhasználat lehetővé teszi az ügyfél számára, hogy továbbra is használja a szolgáltatásokat, ha a szolgáltatás a vonatkozó korlátokon túlra van használva. A túlóra azt a használat alapján határozza meg, hogy az előfizetés használat alapján fizetett túlfelhasználása hogyan fog felmerülni.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, a következő irányítópulton Partnerközpont [ki:](https://partner.microsoft.com/dashboard). Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító az áttűnött előfizetéshez.

## <a name="rest-request"></a>REST-kérés
[GET] /customers/{customer-tenant-id}/subscriptions/overage
### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **KAP**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterekkel használhatja az ügyfél túlhasználatát.

| Név                    | Típus     | Kötelező | Leírás                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **guid** | Y        | Az ügyfél bérlőjéhez tartozó GUID.             |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén ez a módszer a túlóra értéket adja vissza az ügyfélnek.

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
    "totalCount": 1,
    "items": [
        {
            "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
            "partnerId": "1234",
            "type": "PhoneServices",
            "overageEnabled": true,
            "links": {
                "overage": {
                    "uri": "/customers/f62cf10b-8f76-4fc4-9774-c5291f8faf86/subscriptions/overage",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Overage"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
