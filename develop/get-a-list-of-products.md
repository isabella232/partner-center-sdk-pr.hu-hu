---
title: Termékek listájának lekérése (ország alapján)
description: A Product erőforrással termékek gyűjteményét kaphatja meg az ügyfél országa szerint.
ms.date: 02/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 601fc2c8012d92d6964f0aaa29a3a46d732df300
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456052"
---
# <a name="get-a-list-of-products-by-country"></a>Termékek listájának lekérése (ország alapján)

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az alábbi módszerekkel egy adott országban elérhető termékek gyűjteményét kaphatja meg.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ország.

## <a name="c"></a>C\#

A termékek listájának lekért listája:

1. Az **IAggregatePartner.Products** gyűjtemény használatával válassza ki az országot a **ByCountry() metódussal.**

2. Válassza ki a katalógusnézetet a **ByTargetView() metódussal.**

3. (Nem kötelező) Válassza ki a foglalás hatókörét a **ByReservationScope() metódussal.**

4. (Nem kötelező) Válassza ki a célszegmenst a **ByTargetSegment() metódussal.**

5. A **gyűjtemény visszaadáshoz hívja** meg a Get() vagy **a GetAsync()** metódust.

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

A termékek listájának lekért listája:

1. Az **IAggregatePartner.getProducts** függvény használatával válassza ki az országot a **byCountry() függvény** használatával.

2. Válassza ki a katalógusnézetet a **byTargetView() függvény** használatával.
3. (Nem kötelező) Válassza ki a **célszegmenst a byTargetSegment() függvény** használatával.

4. A gyűjtemény visszaadáshoz hívja meg a **get()** függvényt.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A termékek listájának lekért listája:

1. Hajtsa végre [**a Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) parancsot.

2. Válassza ki a katalógust a Catalog paraméter **megadásával.**
3. (Nem kötelező) Válassza ki a célszegmenst a Szegmens paraméter **megadásával.**

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **KAP** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az alábbi elérési út és lekérdezési paraméterek használatával lekérdezheti a termékek listáját.

| Név                   | Típus     | Kötelező | Leírás                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| ország                | sztring   | Yes      | Az ország/régió azonosítója.                                                  |
| targetView             | sztring   | Yes      | A katalógus célnézetét azonosítja. A támogatott értékek a következőek: <br/><br/>**Azure**, amely az összes Azure-elemet tartalmazza<br/><br/>**AzureReservations**, amely az összes Azure-foglalási elemet tartalmazza<br/><br/>**AzureReservationsVM,** amely az összes virtuálisgép-foglalási elemet tartalmazza<br/><br/>**AzureReservationsSQL,** amely az összes SQL elemet tartalmazza<br/><br/>**AzureReservationsCosmosDb,** amely a Cosmos-adatbázis összes foglalási elemét tartalmazza<br/><br/>**MicrosoftAzure**, amely a Microsoft Azure **(MS-AZR-0145P)** és az Azure-csomagokhoz tartalmaz elemeket<br/><br/>**OnlineServices**, amely az összes online szolgáltatáselemet tartalmazza. Ez a targetView a kereskedelmi piacteret, a hagyományos licencalapú szolgáltatásokat és az új kereskedelmi licencalapú szolgáltatásokat tartalmazza<br/><br/>**Szoftver,** amely az összes szoftverelemet tartalmazza<br/><br/>**SoftwareSUSELinux**, amely az összes szoftveres SUSE Linux-elemet tartalmazza<br/><br/>**SzoftverPerpetual**, amely az összes állandó szoftverelemet tartalmazza<br/><br/>**SoftwareSubscriptions**, amely az összes szoftver-előfizetési elemet tartalmazza    |
| targetSegment (célszegmentálás)          | sztring   | No       | Azonosítja a célszegmenst. A különböző célközönségek nézete. A támogatott értékek a következőek: <br/><br/>**Kereskedelmi**<br/>**Oktatás**<br/>**Kormány**<br/>**Nonprofit**  |
| reservationScope | sztring   | No | Az Azure Reservationshez használható termékek listájának lekérdezésekor adja meg, hogy lekérdezi az Azure-csomagokra vonatkozó `reservationScope=AzurePlan` termékek listáját. Zárja ki ezt a paramétert, hogy lekérte a termékek listáját az Azure Reservationshez, amelyek az Microsoft Azure (**MS-AZR-0145P**) előfizetések esetében alkalmazhatók.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-examples"></a>Példák kérésre

#### <a name="products-by-country"></a>Termékek ország szerint

Ebben a példában országonként lekért termékek listáját Microsoft Azure (MS-AZR-0145P) előfizetések és Azure-csomagok esetében.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Azure-beli virtuális gépek foglalása (Azure-csomag)

Kövesse ezt a példát az Azure-csomagokra vonatkozó Azure-beli virtuálisgép-foglalások termékek országonkénti listájának lekért listájához.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Azure-beli virtuális gépek foglalása Microsoft Azure (MS-AZR-0145P) előfizetéshez

Kövesse ezt a példát a termékek országok szerinti listáját az Azure-beli virtuális gépek foglalásához, amelyek az Microsoft Azure -előfizetések (MS-AZR-0145P) esetében alkalmazhatók.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="new-commerce-license-based-services"></a>Új kereskedelmi licencalapú szolgáltatások

> [!Note] 
> Az új kereskedelmi változások jelenleg csak az M365/D365 új kereskedelmi felhasználói élményének technikai előzetesében részt vesz partnerek számára érhetők el

Az alábbi példa alapján országonként lekért termékek listája érhető el az új kereskedelmi licencalapú szolgáltatásokhoz az új kereskedelmi felhasználói élmény technikai előzetes kiadásának részeként. Az új kereskedelmi licencalapú szolgáltatásokat az **OnlineServicesNCE** azonosító és displayNames értéke azonosítja. Lásd az alábbi példaválaszt.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=OnlineServices HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse termékerőforrások [**gyűjteményét**](product-resources.md#product) tartalmazza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát a következő [hibakódok Partnerközpont meg:](error-codes.md).

Ez a metódus a következő hibakódokat adja vissza:

| HTTP-állapotkód     | Hibakód   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | A kért targetSegment szolgáltatáshoz való hozzáférés nem engedélyezett.                                                     |
| 403                  | 400036       | A kért targetView nézethez való hozzáférés nem engedélyezett.                                                        |

### <a name="response-example-for-azure-vm-reservations-azure-plan"></a>Azure-beli virtuális gépek foglalási példái (Azure-csomag)

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

