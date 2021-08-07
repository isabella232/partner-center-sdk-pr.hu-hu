---
title: Átvitel létrehozása
description: Előfizetések átvitelének létrehozása egy ügyfél számára.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8414bbcfa0940742339eeba24b3b6a16ddfb6e3424670a4c064cbd995ba50851
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991582"
---
# <a name="create-a-transfer"></a>Átvitel létrehozása

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/transfers HTTP/1.1                    |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél azonosításához használja a következő path paramétert.

| Név            | Típus     | Kötelező | Leírás                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ügyfél-azonosító** | sztring   | Yes      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.             |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a [kérés törzsében található TransferEntity](transfer-entity-resources.md) tulajdonságokat ismerteti.

| Tulajdonság              | Típus          | Kötelező  | Leírás                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | sztring        | No    | A transferEntity sikeres létrehozásakor megadott transferEntity azonosító.                               |
| createdTime (létrehozás ideje)           | DateTime      | No    | A transferEntity létrejöttének dátuma dátum-idő formátumban. Alkalmazva a transferEntity sikeres létrehozásakor.      |
| lastModifiedTime      | DateTime      | No    | A transferEntity utolsó frissítésének dátuma dátum-idő formátumban. Alkalmazva a transferEntity sikeres létrehozásakor. |
| lastModifiedUser      | sztring        | No    | Az a felhasználó, aki utoljára frissítette a transferEntity adatokat. Alkalmazva a transferEntity sikeres létrehozásakor.                          |
| customerName (ügyfél neve)          | sztring        | No    | Választható. Annak az ügyfélnek a neve, akinek az előfizetései átadása folyamatban van.                                              |
| customerTenantId (customerTenantId)      | sztring        | No    | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet. Alkalmazva a transferEntity sikeres létrehozásakor.         |
| partnertenantid       | sztring        | No    | Egy GUID formátumú partnerazonosító, amely azonosítja a partnert.                                                                   |
| sourcePartnerName (forráspartner neve)     | sztring        | No    | Választható. Az átadást kezdeményező partnerszervezet neve.                                           |
| sourcePartnerTenantId (forráspartner-partnerazonosító) | sztring        | Yes   | Egy GUID formátumú partnerazonosító, amely azonosítja az átadást kezdeményező partnert.                                           |
| targetPartnerName     | sztring        | No    | Választható. Annak a partnernek a neve, amely számára az átvitelt megcélozni kell.                                         |
| targetPartnerTenantId | sztring        | Yes   | Egy GUID formátumú partnerazonosító, amely azonosítja azt a partnert, akinek az átadást megcéloznia kell.                                  |
| lineItems (sorsorok)             | Objektumok tömbje | Yes| [TransferLineItem-erőforrások tömbje.](transfer-entity-resources.md#transferlineitem)                                   |
| status                | sztring        | No    | A transferEntity állapota. Lehetséges értékek: "Aktív" (törölhető/elküldve) és "Befejezve" (már befejeződött). Alkalmazva a transferEntity sikeres létrehozásakor.|

Ez a táblázat a [kérés törzsében található TransferLineItem](transfer-entity-resources.md#transferlineitem) tulajdonságokat ismerteti.

|      Tulajdonság       |            Típus             | Kötelező | Leírás                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | sztring                     | No       | Egy átvitelisor-elem egyedi azonosítója. Alkalmazva a transferEntity sikeres létrehozásakor.|
| subscriptionId       | sztring                     | Yes      | Az előfizetés azonosítója.                                                                         |
| quantity             | int                        | No       | A licencek vagy példányok száma.                                                                 |
| billingCycle         | Objektum                     | No       | Az aktuális időszakhoz beállított számlázási ciklus típusa.                                                |
| friendlyName (rövid név)         | sztring                     | No       | Választható. A partner által definiált elem rövid neve, amely segít egyértelműsedni.                |
| partnerIdOnRecord    | sztring                     | No       | PartnerAzonosító a rekordban (MPN-azonosító) a vásárláskor, amikor az átadást elfogadják.              |
| offerId (ajánlatazonosító)              | sztring                     | No       | Az ajánlat azonosítója.                                                                                |
| addonItems (bővítmények)           | **TransferLineItem-objektumok** listája | No | A bővítmények transferEntity sorelemek gyűjteménye, amelyek az átvitt alap előfizetéssel együtt lesznek átadva. Alkalmazva a transferEntity sikeres létrehozásakor.|
| transferError        | sztring                     | No       | A transferEntity után lesz alkalmazva, ha hiba történik.                                        |
| status               | sztring                     | No       | A sortem állapota a transferEntity oszlopban.                                                    |

### <a name="request-example"></a>Példa kérésre

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus visszaadja a válasz törzsében a megadott [TransferEnity](transfer-entity-resources.md) erőforrást.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
