---
title: Előfizetés ellenőrzése a migráláshoz
description: Annak ellenőrzése, hogy egy előfizetés jogosult-e a migrálásra.
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8d2ae596901a45a794230c79cfb54815963e300
ms.sourcegitcommit: 856b0baa4824960e13ee9672817a2d2e713fdf43
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/05/2021
ms.locfileid: "129528705"
---
# <a name="validate-a-subscription-for-migration"></a>Előfizetés ellenőrzése a migráláshoz

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Előfizetés ellenőrzése az új kereskedelmi felhasználói élménybe való migráláshoz

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy aktuális előfizetés-azonosító

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
|**POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/migrations/newcommerce/validate HTTP/1.1  |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja az előfizetés migráláshoz való érvényesítéséhez szükséges lekérdezési paramétereket.

| Név               | Típus   | Kötelező | Leírás                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| ügyfél-bérlő-azonosító | sztring | Yes      | Egy GUID-formátumú sztring, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem [törzsében](subscription-resources.md) található Előfizetés tulajdonságait ismerteti.

| Tulajdonság              | Típus             | Kötelező        | Leírás |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| currentSubscriptionId (aktuális előíróazonosító) | sztring           | Yes             | Egy előfizetés-azonosító, amely azt jelzi, hogy melyik előfizetést kell érvényesíteni a migráláshoz.            |

### <a name="request-example"></a>Példa kérésre

```http
"currentSubscriptionId" : "9beb6319-6889-4d28-a155-68ca9c783842"
```

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén ez a metódus egy "isEligible" logikai értéket ad vissza a válasz törzsében, amely jelzi, hogy az aktuális előfizetés jogosult-e az új kereskedelembe való migrálásra.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-examples"></a>Példák válaszra

```http
1. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": false,
        "errors": [
            {
                "code": 5,
                "description": "Subscription cannot be migrated to New Commerce because the equivalent offer is not yet available in New Commerce",
            }
        ]
    }

2. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": true,
    "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV",
    }
```
