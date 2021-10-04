---
title: Egy adott ügyfél túlteljesítményének frissítése
description: Frissíti egy adott ügyfél túlteljesítményét.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 58590a1882cfe94ddd9779f9e9f766f3e62cffd6
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/02/2021
ms.locfileid: "129383446"
---
# <a name="update-overage"></a>Túlóra frissítése

**A következőre vonatkozik:**

- Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi változások jelenleg csak azok a partnerek számára érhetők el, akik a Microsoft 365/Dynamics 365 új kereskedelmi felhasználói élményének technikai előzetesében dolgoznak.

Egy adott ügyfél túlfelhasználási előfizetésre való beállítására használatos. A túl sok idő eltávolításához is használható false (hamis) érték beállításával. A túlhasználat lehetővé teszi, hogy az ügyfél továbbra is használja a szolgáltatásokat, ha a szolgáltatást a korlátozásokon túl használja. A túlóra azért van, mert a használaton túli előfizetési túl használat alapján fizetendő díj fel lesz halmozott.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy előfizetés-azonosító az áttért előfizetéshez.

## <a name="rest-request"></a>REST-kérés
[PUT] /customers/{customer-tenant-id}/subscriptions/overage
### <a name="request-syntax"></a>Kérés szintaxisa

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


| Név                    | Típus     | Description                                       |
|-------------------------|----------|---------------------------------------------------|
| **azureEntitlementId**  | **guid** | Egy GUID, amely meghatározza a használaton túlóra-előfizetést.             |
| **partnerazonosító**  | **guid** | Egy közvetett viszonteladó MPN-azonosítója. Csak kétrétegű modellre (közvetett szolgáltató) vonatkozik.            |

| **overageEnabled (overageEnabled)**   |  **bool** | Meghatározza, hogy a túlóra engedélyezve van-e egy adott használatban van-e.             |


### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "overageEnabled": true
}

```

## <a name="rest-response"></a>REST-válasz

Ha ez a módszer sikeres, a túl sok értéket adja vissza az ügyfélnek.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
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
```
