---
title: Átvitel létrehozása
description: Előfizetések átvitelének létrehozása az ügyfelek számára.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767760"
---
# <a name="create-a-transfer"></a>Átvitel létrehozása

**A következőkre vonatkozik:**

- Partnerközpont

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers http/1.1                    |

### <a name="uri-parameter"></a>URI-paraméter

Az ügyfél azonosításához használja a következő Path paramétert.

| Név            | Típus     | Kötelező | Leírás                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **ügyfél-azonosító** | sztring   | Igen      | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.             |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsének [TransferEntity](transfer-entity-resources.md) tulajdonságait ismerteti.

| Tulajdonság              | Típus          | Kötelező  | Leírás                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | sztring        | No    | A transferEntity sikeres létrehozásakor megadott transferEntity-azonosító.                               |
| createdTime           | DateTime      | Nem    | A transferEntity létrehozásának dátuma dátum és idő formátumban. A transferEntity sikeres létrehozása után alkalmazható.      |
| lastModifiedTime      | DateTime      | Nem    | A transferEntity utolsó frissítésének dátuma, dátum-idő formátumban. A transferEntity sikeres létrehozása után alkalmazható. |
| lastModifiedUser      | sztring        | No    | Az a felhasználó, aki utoljára frissítette a transferEntity. A transferEntity sikeres létrehozásakor lett alkalmazva.                          |
| Customername (          | sztring        | No    | Választható. Annak az ügyfélnek a neve, amelynek előfizetéseit át kell vinni.                                              |
| customerTenantId      | sztring        | No    | Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet. A transferEntity sikeres létrehozása után alkalmazható.         |
| partnertenantid       | sztring        | No    | Egy GUID formátumú partner-azonosító, amely azonosítja a partnert.                                                                   |
| sourcePartnerName     | sztring        | No    | Választható. A partner azon szervezetének neve, aki kezdeményezi az átvitelt.                                           |
| sourcePartnerTenantId | sztring        | Igen   | Egy GUID formátumú partner-azonosító, amely azonosítja az átvitelt kezdeményező partnert.                                           |
| targetPartnerName     | sztring        | No    | Választható. A partner azon szervezetének neve, amelyhez az átvitel irányul.                                         |
| targetPartnerTenantId | sztring        | Igen   | Egy GUID formátumú partner-azonosító, amely azonosítja azt a partnert, akire az átvitel irányul.                                  |
| Listaelemek             | Objektumok tömbje | Igen| [TransferLineItem](transfer-entity-resources.md#transferlineitem) -erőforrások tömbje.                                   |
| status                | sztring        | No    | A transferEntity állapota. A lehetséges értékek: "Active" (törölhető/elküldhető) és "befejezett" (már befejeződött). A transferEntity sikeres létrehozása után alkalmazható.|

Ez a táblázat a kérelem törzsének [TransferLineItem](transfer-entity-resources.md#transferlineitem) tulajdonságait ismerteti.

|      Tulajdonság       |            Típus             | Kötelező | Leírás                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | sztring                     | No       | Egy adatátviteli sorhoz tartozó egyedi azonosító. A transferEntity sikeres létrehozása után alkalmazható.|
| subscriptionId       | sztring                     | Igen      | Az előfizetés azonosítója.                                                                         |
| quantity             | int                        | Nem       | A licencek vagy példányok száma.                                                                 |
| billingCycle         | Objektum                     | Nem       | Az aktuális időszakban beállított számlázási ciklus típusa.                                                |
| friendlyName         | sztring                     | No       | Választható. A partner által a egyértelműsítse segítségére meghatározott rövid név.                |
| partnerIdOnRecord    | sztring                     | No       | A PartnerId on Record (MPNID) azon a vásárláson, amely az átvitel elfogadásakor történik.              |
| offerId              | sztring                     | No       | Az ajánlat azonosítója.                                                                                |
| addonItems           | **TransferLineItem** -objektumok listája | Nem | Olyan transferEntity-elemek gyűjteménye, amelyek az átvitt alap előfizetéssel együtt lesznek átadva. A transferEntity sikeres létrehozása után alkalmazható.|
| transferError        | sztring                     | No       | A transferEntity elfogadását követően alkalmazva hiba esetén.                                        |
| status               | sztring                     | No       | A lineitem állapota a transferEntity.                                                    |

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

Ha ez sikeres, ez a metódus a válasz törzsében lévő [TransferEnity](transfer-entity-resources.md) -erőforrást adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

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
