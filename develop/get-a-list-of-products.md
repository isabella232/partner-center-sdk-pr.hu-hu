---
title: Termékek listájának lekérése (ország alapján)
description: A Product (termék) erőforrás használatával a termékek gyűjteményét az ügyfél országa veheti igénybe.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768172"
---
# <a name="get-a-list-of-products-by-country"></a>Termékek listájának lekérése (ország alapján)

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A következő módszerekkel kérheti le egy adott országban elérhető termékek gyűjteményét.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy ország.

## <a name="c"></a>C\#

A termékek listájának lekérése:

1. A **IAggregatePartner. Products** gyűjtemény használatával válassza ki az országot a **ByCountry ()** metódus használatával.

2. Válassza ki a katalógus nézetet a **ByTargetView ()** metódus használatával.

3. Választható Válassza ki a foglalási hatókört a **ByReservationScope ()** metódus használatával.

4. Választható A **ByTargetSegment ()** metódus használatával válassza ki a célként megadott szegmenst.

5. A gyűjtemény visszaadásához hívja meg a **Get ()** vagy a **GetAsync ()** metódust.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

A termékek listájának lekérése:

1. Használja az **IAggregatePartner. getProducts** függvényt az ország kiválasztásához a **byCountry ()** függvény használatával.

2. Válassza ki a katalógus nézetet a **byTargetView ()** függvény használatával.
3. Választható Válassza ki a cél szegmenst a **byTargetSegment ()** függvény használatával.

4. A gyűjtemény visszaküldéséhez hívja meg a **Get ()** függvényt.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A termékek listájának lekérése:

1. Futtassa a [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) parancsot.

2. Válassza ki a katalógust a **katalógus** paraméter megadásával.
3. Választható Válassza ki a cél szegmenst a **szegmens** paraméter megadásával.

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Products? ország = {ország} &targetView = {targetView} &targetSegment = {TARGETSEGMENT} http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

A termékek listájának megjelenítéséhez használja a következő elérési utat és a lekérdezési paramétereket.

| Név                   | Típus     | Kötelező | Leírás                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| ország                | sztring   | Igen      | Az ország/régió azonosítója.                                                  |
| targetView             | sztring   | Igen      | Meghatározza a katalógus céljának nézetét. A támogatott értékek a következők: <br/><br/>**Azure**, amely tartalmazza az összes Azure-elemet<br/><br/>**AzureReservations**, amely tartalmazza az összes Azure foglalási elemet<br/><br/>**AzureReservationsVM**, amely tartalmazza az összes virtuális gép (VM) foglalási elemét<br/><br/>**AzureReservationsSQL**, amely az összes SQL-foglalási elemet tartalmazza<br/><br/>**AzureReservationsCosmosDb**, amely tartalmazza az összes Cosmos-adatbázis foglalási elemét.<br/><br/>**MicrosoftAzure**, amely Microsoft Azure előfizetések (**MS-AZR-0145P**) és az Azure-csomagok elemeit tartalmazza<br/><br/>**OnlineServices**, amely tartalmazza az összes online szolgáltatási elemet (beleértve a kereskedelmi piactér termékeit is)<br/><br/>**Szoftver**, amely tartalmazza az összes szoftver elemet<br/><br/>**SoftwareSUSELinux**, amely tartalmazza az összes szoftver SUSE Linux-elemet<br/><br/>**SoftwarePerpetual**, amely tartalmazza az összes örökös szoftver elemet.<br/><br/>**SoftwareSubscriptions**, amely tartalmazza az összes szoftver-előfizetési elemet    |
| targetSegment          | sztring   | No       | A célként megadott szegmenst azonosítja. A különböző célközönségek nézete. A támogatott értékek a következők: <br/><br/>**kereskedelmi**<br/>**oktatás**<br/>**kormány**<br/>**nonprofit**  |
| reservationScope | sztring   | No | A Azure Reservations termékek listájának lekérdezésekor az `reservationScope=AzurePlan` Azure-csomagokra érvényes termékek listájának lekéréséhez. Zárja be ezt a paramétert, hogy lekérje a Microsoft Azure (**MS-AZR-0145P**) előfizetésekre vonatkozó termékek listáját az Azure-foglalásokhoz.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-examples"></a>Példák kérése

#### <a name="products-by-country"></a>Termékek országonként

Ezt a példát követve beolvashatja a termékek ország szerinti listáját Microsoft Azure (MS-AZR-0145P) előfizetések és az Azure-csomagok alapján.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Azure VM-foglalások (Azure-csomag)

Ezt a példát követve az Azure-csomagokra érvényes Azure-beli virtuális gépekhez tartozó termékek országonkénti listáját kaphatja meg.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Azure-beli virtuális gépek foglalása Microsoft Azure (MS-AZR-0145P) előfizetésekhez

Ezt a példát követve megtekintheti az ország által a Microsoft Azure (MS-AZR-0145P) előfizetésekre alkalmazható Azure-beli virtuálisgép-foglalások listáját.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse tartalmazza a [**termék**](product-resources.md#product) erőforrásainak gyűjteményét.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Leírás                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | A kért targetSegment való hozzáférés nem engedélyezett.                                                     |
| 403                  | 400036       | A kért targetView való hozzáférés nem engedélyezett.                                                        |

### <a name="response-example"></a>Példa válaszra

```http
{
    "totalCount": 19,
    "items": [
        {
            "id": "DZH318Z0BQ3Q",
            "title": "Virtual Machines DSv2 Series",
            "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
            "productType": {
                "id": "Azure",
                "displayName": "Azure",
                "subType": {
                "id": "VirtualMachines",
                "displayName": "VirtualMachines"
                }
            },
            "isMicrosoftProduct": true,
            "publisherName": "Microsoft",
            "links": {
                "skus": {
                    "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ3Q?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
