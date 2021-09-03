---
title: Termékek listájának lekérése (ügyfél alapján)
description: Az ügyfélazonosítók segítségével termékek gyűjteményét kaphatja meg ügyfél szerint.
ms.assetid: ''
ms.date: 02/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1f3f38271b97ceba143c819ec03758ad1b9c0d3b
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123455761"
---
# <a name="get-a-list-of-products-by-customer"></a>Termékek listájának lekérése (ügyfél alapján)

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az alábbi módszerekkel lekért termékek gyűjteményét egy meglévő ügyfélhez.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1 |

#### <a name="request-uri-parameters"></a>URI-paraméterek kérése

| Név               | Típus | Kötelező | Leírás                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **ügyfél-bérlő-azonosító** | GUID | Yes | Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet. |
| **targetView** | sztring | Yes | A katalógus célnézetét azonosítja. A támogatott értékek a következőek: <br/><br/>**Azure**, amely az összes Azure-elemet tartalmazza<br/><br/>**AzureReservations**, amely az összes Azure-foglalási elemet tartalmazza<br/><br/>**AzureReservationsVM,** amely az összes virtuálisgép-foglalási elemet tartalmazza<br/><br/>**AzureReservationsSQL,** amely az összes SQL elemet tartalmazza<br/><br/>**AzureReservationsCosmosDb**, amely az összes Cosmos-adatbázis foglalási elemét tartalmazza<br/><br/>**MicrosoftAzure**, amely Microsoft Azure (**MS-AZR-0145P**) és Azure-csomagokhoz<br/><br/>**OnlineServices**, amely az összes online szolgáltatáselemet tartalmazza. Ez a targetView a kereskedelmi piacteret, a hagyományos licencalapú szolgáltatásokat és az új kereskedelmi licencalapú szolgáltatásokat tartalmazza<br/><br/>**Szoftver,** amely az összes szoftverelemet tartalmazza<br/><br/>**SoftwareSUSELinux**, amely az összes szoftveres SUSE Linux-elemet tartalmazza<br/><br/>**SzoftverPerpetual**, amely az összes állandó szoftverelemet tartalmazza<br/><br/>**SoftwareSubscriptions**, amely az összes szoftver-előfizetési elemet tartalmazza  |

### <a name="request-header"></a>Kérelem fejléce

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

Egy adott ügyfél számára elérhető Azure-beli használatalapú termékek listájának lekérése. A nyilvános felhőben Microsoft Azure (MS-AZR-0145P) és Az Azure-csomagokhoz is visszaadunk termékeket:

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```
#### <a name="new-commerce-license-based-services"></a>Új kereskedelmi licencalapú szolgáltatások

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el

Ebben a példában országonként lekért termékek listája érhető el az új kereskedelmi licencalapú szolgáltatásokhoz az új kereskedelmi élmény technikai előzetes kiadásának részeként. Az új kereskedelmi licencalapú szolgáltatások az **OnlineServicesNCE** azonosító és displayNames értéke alapján lesznek azonosítva. Lásd az alábbi példaválaszt.

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=OnlineServices HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-válasz

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő [hibakódok Partnerközpont meg:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód | Hibakód   | Description                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | A kért targetView nézethez való hozzáférés nem engedélyezett. |

### <a name="response-example-for-microsoft-azure-and-azure-plan"></a>Válasz példa a Microsoft Azure Azure-csomagra

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
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
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
### <a name="response-example-for-new-commerce-license-based-services"></a>Válasz példa az új kereskedelmi licencalapú szolgáltatásokra

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesző partnerek számára érhetők el

```http
{
  "totalCount": 19,
  "items": [{
      "id": "CFQ7TTC0LH18",
      "title": "Microsoft 365 Business Basic",
      "description": "Best for businesses that need professional email, cloud file storage, and online meetings & chat. Desktop versions of Office apps like Excel, Word, and PowerPoint not included. For businesses with up to 300 employees.",
      "productType": {
        "id": "OnlineServicesNCE",
        "displayName": "OnlineServicesNCE"
      },
      "isMicrosoftProduct": true,
      "publisherName": "Microsoft Corporation",
      "links": {
        "skus": {
          "uri": "/products/CFQ7TTC0LH18/skus?country=US",
          "method": "GET",
          "headers": []
        },
        "self": {
          "uri": "/products/CFQ7TTC0LH18?country=US",
          "method": "GET",
          "headers": []
        }
      }
    },
    ...
  ],
  "links": {
    "self": {
      "uri": "/products?country=US&targetView=OnlineServices",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
