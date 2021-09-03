---
title: Új kereskedelmi előfizetés váltása
description: Frissíti az ügyfél új commmerce-előfizetését egy megadott cél-előfizetésre.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 2bbf2f63cec416e4d4b4a671d2e2b2914b5f5713
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457306"
---
# <a name="transition-a-new-commerce-subscription"></a>Új kereskedelmi előfizetés váltása

**A következőkre vonatkozik:** Partnerközpont

**Megfelelő szerepkörök**

- Globális rendszergazda
- Rendszergazdai ügynök

> [!Note] 
> Az új kereskedelmi módosítások jelenleg csak az M365/D365 új kereskedelmi felhasználói élmény technikai előzetesének részét képezi partnerek számára érhetők el.

Az ügyfél új commmerce-előfizetésének cél-előfizetésre való frissítéséhez használatos. Először szerezze be a jogosult váltásokat, hogy a SKUs frissíthető legyen. Ezután az átváltás végrehajtásához szükséges váltás után. Ezek a módszerek a hagyományos és az új kereskedelmi forrás-előfizetéseket is támogatják.  

## <a name="get-transition-eligibilities"></a>Áttűnés képességeinek leözése

Egy adott ügyfélre, előfizetésre és kért típusra vonatkozó jogosult váltások listáját adja vissza.

### <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, a következő irányítópulton Partnerközpont [ki:](https://partner.microsoft.com/dashboard). Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- A kezdeti előfizetés egy előfizetés-azonosítója.

### <a name="rest-request"></a>REST-kérés

#### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **KAP**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/transitionEligibilities?eligibilityType={immediate, scheduled} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterekkel jogosult átmeneteket ad vissza.

| Név                    | Típus     | Kötelező | Leírás                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **guid** | Y        | Az ügyfél bérlőjéhez tartozó GUID.             |
| **subscriptoin-Id** | **guid** | Y        | A kezdeti előfizetésnek megfelelő GUID. |
| **jogosultságtípus**       | **sztring** | Y        | Leírja, hogy mikor kell végrehajtani az tranzitást, amely lehet azonnali vagy ütemezett.  |

#### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

#### <a name="request-body"></a>A kérés törzse

None

#### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-Id}/transitionEligibilities?eligibilityType=immediate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

### <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus a válasz törzsében található jogosult átmenetek listáját adja vissza.

#### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

#### <a name="eligibility-errors"></a>Jogosultsági hibák

Hibaleírások és jelentés.

| Hibaleírás | Értelmezés  |
|-------------------------|----------|
|Az előfizetés nem lehet átváltva – a forrás-előfizetés nem aktív. | Az eredeti alállapot nem Aktív |
|Az előfizetés nem lehet átváltva – a forrás-előfizetés még nincs kiépítve. | Az eredeti al FulfillmentState nem sikeres |
|Az átváltás típusa nem kompatibilis – AzureAD-előfizetés-leképezés szükséges. | LegacyCannotConvertSubscriptionId hiba a GetSubscriptionUpgradeConflicts hívhatósága során |
|Az átváltás típusa nem kompatibilis – a licencátvitelhez ütköző előfizetések léteznek. | Ha bármely AAD-szolgáltatás eltérő előfizetéshez tartozik előfizetés-azonosítóval, adja hozzá azt az ütközések listájához (beleértve a régi vagy a modern vásárlási folyamat vásárlását is) |

#### <a name="response-example"></a>Példa válaszra

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
            "catalogItemId": "CFQ7TTC0KZCR:0001:CFQ7TTC0K71H",
            "title": "Microsoft 365 E5 Test Sku Title",
            "description": "Microsoft 365 E5 Test Sku Description",
            "quantity": 1,
            "eligibilities": [
{
                    "isEligible": true,
                    "transitionType": "transition_only",
                    "errors": []
                },
                
{
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        },
        {
            "catalogItemId": "CFQ7TTC0L4M3:0001:CFQ7TTC0K78T",
            "title": "Business Premium Test Sku Title",
            "description": "Business Premium Test Sku Description",
            "quantity": 1,
            "eligibilities": [
                {
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="post-transition"></a>Váltás utáni

Egy adott ügyfélre és előfizetésre vonatkozó átmeneti kérést ad közzé. Intial állapotú átmenetet ad vissza.

### <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, a következő irányítópulton Partnerközpont [ki:](https://partner.microsoft.com/dashboard). Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- A kezdeti előfizetés egy előfizetés-azonosítója.

### <a name="rest-request"></a>REST-kérés

#### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **POST**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscriptoin-Id}/transitions HTTP/1.1 |


#### <a name="uri-parameter"></a>URI-paraméter

Az átváltás végrehajtásához használja az alábbi lekérdezési paramétereket.

| Név                    | Típus     | Kötelező | Leírás                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **ügyfél-bérlő-azonosító**  | **guid** | Y        | Az ügyfél bérlőjéhez tartozó GUID.             |
| **subscriptoin-Id** | **guid** | Y        | A kezdeti előfizetésnek megfelelő GUID. |

#### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

#### <a name="request-body"></a>A kérés törzse

A kérelem **törzsében** teljes átváltási erőforrásra van szükség.

#### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customerId}/subscriptions/{subscriptionId}/transitions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "toCatalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
    "quantity": 5,
    "transitionType": "transition_with_license_transfer",
    "events": []
}
```

### <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy Transition (Átváltás) erőforrást ad vissza a kezdeti eseményekkel.

#### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

#### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

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
        }
    ],
    "attributes":
    {
        "objectType": "Transition"
    }
}
```
