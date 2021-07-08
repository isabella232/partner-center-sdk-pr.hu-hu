---
title: Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ügyfél alapján)
description: Egy adott termékhez és termékváltozathoz az ügyfél, a termék- és termékváltozat-azonosítók használatával kaphat rendelkezésre állási gyűjteményt az ügyféltől.
ms.assetid: ''
ms.date: 10/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b237bbd17a6108bbcb4e23529cf476a6b8306f68
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874550"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-customer"></a>Egy termékváltozat elérhetőségét tartalmazó lista lekérése (ügyfél alapján)

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A következő módszerekkel kaphat rendelkezésre állási gyűjteményt egy adott termékhez és termékváltozathoz, amelyek egy adott ügyfél számára elérhetők.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

- Egy termékazonosító (**termékazonosító).**

- Egy termékváltozat-azonosító (**sku-id**).

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus | Kérés URI-ja                                                                                                                 |
|--------|-----------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{termékazonosító}/skus/{sku-id} HTTP/1.1 |

### <a name="request-uri-parameters"></a>URI-paraméterek kérése

| Név               | Típus | Kötelező | Leírás                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| ügyfél-bérlő-azonosító | GUID | Igen | Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet. |
| termékazonosító | sztring | Igen | A terméket azonosító sztring. |
| sku-id | sztring | Igen | A termékváltozatot azonosító sztring. |

### <a name="request-header"></a>Kérelem fejléce

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6/skus/0001/availabilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>REST-válasz

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód | Hibakód | Leírás |
|------------------|------------|-------------|
| 404 | 400013 | A szülőtermék nem található. |

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949
{
    "id": "0001",
    "productId": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Microsoft Azure plan (MS-AZR-0017G)",
    "minimumQuantity": 1,
    "maximumQuantity": 1,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "MicrosoftCustomerAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "pilotProgram": "modernazurepilot"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
