---
title: Termék termék termékterméklistáinak lekért listája (ügyfél szerint)
description: Lekért egy gyűjteményt az adott termék termékhez ügyfél szerint.
ms.assetid: ''
ms.date: 02/16/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e3794dda474a3807a0707f551f01f13eebd58efe
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456018"
---
# <a name="get-a-list-of-skus-for-a-product-by-customer"></a>Termék termék termékterméklistáinak lekért listája (ügyfél szerint)

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekért egy adott terméktermék-gyűjteményét, amely elérhető egy meglévő ügyfél számára.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Egy termékazonosító **(termékazonosító).**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja                                                                                                        |
|--------|--------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products/{termékazonosító}/skus HTTP/1.1 |

### <a name="request-uri-parameter"></a>Kérés URI-paramétere

| Név               | Típus | Kötelező | Leírás                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| ügyfél-bérlő-azonosító | GUID | Yes | Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet. |
| termékazonosító | sztring | Yes | A terméket azonosító sztring. |

### <a name="request-header"></a>Kérelem fejléce

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products/DZH318Z0BPS6 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>REST-válasz

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő [hibakódok Partnerközpont meg:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód | Hibakód | Description |
|------------------|------------|-------------|
| 404 | 400013 | A szülőtermék nem található. |

### <a name="response-example-for-azure-plan"></a>Azure-csomag válasz példája

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "id": "DZH318Z0BPS6",
    "title": "Microsoft Azure plan",
    "description": "Gain access to Azure Services.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "Azure",
            "displayName": "Azure"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BPS6/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BPS6?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "localizedAttributes": [
        {
            "key": "OfferType",
            "value": "OfferType"
        },
        {
            "key": "Standard",
            "value": "Standard"
        },
        {
            "key": "DevTest",
            "value": "Dev/Test"
        }
    ]
}
```

### <a name="response-example-for-new-commerce-license-based-services"></a>Válasz példa az új kereskedelmi licencalapú szolgáltatásokra

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
{
    "id": "0001",
    "productId": "CFQ7TTC0LH18",
    "title": "Microsoft 365 Business Basic",
    "description": "Best for businesses that need professional email, cloud file storage, and online meetings & chat. Desktop versions of Office apps like Excel, Word, and PowerPoint not included. For businesses with up to 300 employees.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "isTrial": false,
    "supportedBillingCycles": [
        "annual",
        "monthly"
    ],
    "purchasePrerequisites": [
        "MicrosoftCloudAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "hasConstraints": true,
        "isAddon": false,
        "prerequisiteSkus": [],
        "isSoftwareAssuranceApplicable": false,
        "upgradeTargetOffers": [
            "CFQ7TTC0LDPB:0001",
            "CFQ7TTC0LF8Q:0001"
…
        ],
        "provisioningId": "3b555118-da6a-4418-894f-7df1e2096870",
        "internal": false
    },
    "links": {
        "availabilities": {
            "uri": "/products/CFQ7TTC0LH18/skus/0001/availabilities?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/CFQ7TTC0LH18/skus/0001?country=US",
            "method": "GET",
            "headers": []
        }
    }
}        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

