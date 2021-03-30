---
title: Számlázott kereskedelmi fogyasztási sorok számlázásának beolvasása
description: A partner Center API-k használatával lekérheti a kereskedelmi fogyasztási számla sora (a napi lezárt használati sor) részleteit a megadott számlára vonatkozóan.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1e19792da6a7510bf02dd11b3e77f40a8365be2b
ms.sourcegitcommit: 4ec053c56fd210b174fe657aa7b86faf4e2b5a7c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/29/2021
ms.locfileid: "105730195"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a>Számlázott kereskedelmi fogyasztási sorok számlázásának beolvasása

**A következőkre vonatkozik:**

- Partnerközpont

A következő módszerekkel részletes információkat kaphat a kereskedelmi felhasználású számla sorokról (más néven bezárt napi használati sorokból) egy adott számlához.

Ez az API a Microsoft Azure (MS-AZR-0145P) előfizetésekhez tartozó **Azure** -szolgáltatói típusokat is támogatja. Ez azt jelenti, hogy ez az API egy visszamenőlegesen kompatibilis szolgáltatás.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy fiókazonosító. Ez azonosítja azt a számlát, amelynek a sorát be kell olvasni.

## <a name="c"></a>C\#

A megadott számla kereskedelmi vonali elemeinek lekéréséhez le kell kérnie a számla objektumot:

1. Hívja meg a [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust, hogy lekérje a megadott számla műveleteinek számlázására szolgáló felületet.

2. Hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust a számla objektum lekéréséhez. A számla objektum a megadott számla összes adatát tartalmazza.

A **szolgáltató** azonosítja a számlázott részletes információk forrását (például: **egykori**). A **InvoiceLineItemType** meghatározza a típust (például **UsageLineItem**).

A következő példa egy **foreach** hurok használatával dolgozza fel a line Items gyűjteményt. Az egyes **InvoiceLineItemType** tartozó sorok külön gyűjteménye lesz beolvasva.

Egy **InvoiceDetail** -példánynak megfelelő sorok gyűjteményének beolvasása:

1. Adja át a példány **BillingProvider** és **InvoiceLineItemType** a [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metódusnak.

2. A társított sorok beolvasásához hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust.
3. Hozzon létre egy enumerálást a gyűjtemény átjárásához az alábbi példában látható módon.

``` csharp
// IAggregatePartner partnerOperations;
// string invoiceId;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

Ehhez hasonló példát a következő témakörben talál:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **partner Center SDK-minták**
- Osztály: **GetBilledConsumptionReconLineItemsPaging. cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

Az első szintaxissal adja vissza az adott számla összes sorát tartalmazó teljes listát. Nagyméretű számlák esetén a második szintaxist a megadott mérettel és 0 alapú eltolással adja vissza a sorok lapozható listájának visszaadásához. A harmadik szintaxissal szerezheti be a felderítési sorok következő lapját a használatával: `seekOperation = "Next"` .

| Metódus  | Kérés URI-ja                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {CURRENCYCODE} http/1.1                              |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &mérete = {size} http/1.1  |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &méret = {size} &SeekOperation = Next                               |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelem létrehozásakor használja az alábbi URI-és lekérdezési paramétereket.

| Név                   | Típus   | Kötelező | Leírás                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| számlázási azonosító             | sztring | Yes      | A számlát azonosító karakterlánc.                             |
| Szolgáltató               | sztring | Yes      | A szolgáltató: "egykori".                                  |
| számla-sor-tétel típusa | sztring | Yes      | A számla részleteinek típusa: "UsageLineItems". |
| currencyCode           | sztring | Yes      | A számlázott sorok pénznemkódja.                    |
| period                 | sztring | Yes      | A számlázott felderítés időszaka. Példa: current, Previous.        |
| size                   | szám | No       | A visszaadni kívánt elemek maximális száma. Az alapértelmezett méret 2000       |
| seekOperation          | sztring | No       | Állítsa be a seekOperation = Next (Beolvasás) elemet a felderítési sorok következő oldalának beolvasásához. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz tartalmazza a sor elem részleteinek gyűjteményét.

A sor **ChargeType** a **megvásárolt** érték az **új** elemre van leképezve. Az érték- **visszatérítés** a **megszakításra** van leképezve.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

## <a name="rest-examples"></a>REST-példák

### <a name="request-response-example-1"></a>Kérelem – válasz 1. példa

A példában szereplő REST-kérelem és-válasz részletei a következők:

- **Szolgáltató**: **egykori**
- **InvoiceLineItemType**: **UsageLineItems**
- **Időszak**: **előző**

#### <a name="request-example-1"></a>1. példa kérés

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a>1. válasz – példa

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        },
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Ubuntu 16.04 (WebHost)",
            "productName": "Test Test on Linux",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Linux",
            "meterName": "Test Test on Linux - Test Test on Ubuntu 16.04 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TESTRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/testUbuntuTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209951014286867,
            "quantity": 23.350007,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.490235765325545,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.490235765325545,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1999968000511991808131,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a>Kérelem – válasz 2. példa

A példában szereplő REST-kérelem és-válasz részletei a következők:

- **Szolgáltató**: **egykori**
- **InvoiceLineItemType**: **UsageLineItems**
- **Időszak**: **előző**
- **SeekOperation**: **következő**

#### <a name="request-example-2"></a>2. példa a kérelemre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="response-example-2"></a>2. válasz – példa

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
          {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1835431430074643112595,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
