---
title: Számlázott kereskedelmi fogyasztási sorok beolvasása
description: A partner Center API-k használatával beszerezhet egy adott számlára vonatkozó, nem számlázott kereskedelmi fogyasztási sor részleteit tartalmazó gyűjteményt.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b0ce9d4c8d310243d8b799445e5a64975f2d05d
ms.sourcegitcommit: 4ec053c56fd210b174fe657aa7b86faf4e2b5a7c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/29/2021
ms.locfileid: "105730246"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a>Számlázott kereskedelmi fogyasztási sorok beolvasása

**A következőkre vonatkozik:**

- Partnerközpont

A nem számlázott kereskedelmi fogyasztási sorokra vonatkozó részletek gyűjteményének beolvasása.

A következő módszerekkel lekérheti a nem számlázott kereskedelmi fogyasztási sorok (más néven nyitott használati sorok) részletes gyűjteményét programozott módon.

>[!NOTE]
>A napi névleges használat általában 24 órát vesz igénybe a partner Centerben, vagy az API-n keresztül érhető el.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy fiókazonosító. Ez azonosítja azt a számlát, amelynek a sorát be kell olvasni.

## <a name="c"></a>C\#

A megadott számla vonali elemeinek beolvasása:

1. Hívja meg a [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) metódust, hogy lekérje a megadott számla műveleteinek számlázására szolgáló felületet.

2. Hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust a számla objektum lekéréséhez.

A **számla objektum** a megadott számla összes adatát tartalmazza. A **szolgáltató** azonosítja a nem számlázott részletes információk forrását (például **egykori**). A **InvoiceLineItemType** meghatározza a típust (például **UsageLineItem**).

Az alábbi mintakód egy **foreach** hurkot használ a **InvoiceLineItems** -gyűjtemény feldolgozásához. Az egyes **InvoiceLineItemType** tartozó sorok külön gyűjteménye lesz beolvasva.

Egy **InvoiceDetail** -példánynak megfelelő sorok gyűjteményének beolvasása:

1. Adja át a példány **BillingProvider** és **InvoiceLineItemType** a [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metódusnak.

2. A társított sorok beolvasásához hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) metódust.
3. Hozzon létre egy enumerálást a gyűjtemény átjárásához az alábbi példában látható módon.

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

Ehhez hasonló példát a következő témakörben talál:

- Minta: [konzol tesztelési alkalmazás](console-test-app.md)
- Projekt: **partner Center SDK-minták**
- Osztály: **GetUnBilledConsumptionReconLineItemsPaging. cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

A REST-kérelemhez a használati esettől függően a következő szintaxist használhatja. További információkért tekintse meg az egyes szintaxisok leírását.

 | Metódus  | Kérés URI-ja         | Szintaxis használati esetének leírása |                                                                                                                                            |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/UNBILLED/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &időszak = {period} http/1.1                              | Ezzel a szintaxissal teljes listát adhat vissza az adott számlához tartozó összes sor tételről. |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/UNBILLED/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &időszak = {period} &mérete = {size} http/1.1  | Használja ezt a szintaxist nagyméretű számlákhoz. Ezt a szintaxist egy megadott mérettel és 0-alapú eltolással használhatja a sorok lapozható listájának visszaadásához. |
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/UNBILLED/lineitems? Provider = egykori&invoicelineitemtype = usagelineitems&CurrencyCode = {currencycode} &időszak = {period} &mérete = {size} &SeekOperation = tovább                               | Ezzel a szintaxissal beolvashatja az egyeztetési sorok következő oldalát a használatával `seekOperation = "Next"` . |

#### <a name="uri-parameters"></a>URI-paraméterek

A kérelem létrehozásakor használja az alábbi URI-és lekérdezési paramétereket.

| Név                   | Típus   | Kötelező | Leírás                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| Szolgáltató               | sztring | Yes      | A szolgáltató: "**egykori**".                                                |
| számla-sor-tétel típusa | sztring | Yes      | A számla részleteinek típusa: "**UsageLineItems**", "**UsageLineItems**".               |
| currencyCode           | sztring | Yes      | A nem számlázott sorok pénznemkódja.                                  |
| period                 | sztring | Yes      | A nem számlázott felderítés időtartama (például: **current**, **Previous**). Tegyük fel, hogy a számlázási ciklus (01/01/2020 – 01/31/2020) nem számlázott használati adatait kell lekérdezni januárban, válassza a **"jelenlegi",** "else **" (előző) lehetőséget.** |
| size                   | szám | No       | A visszaadni kívánt elemek maximális száma. Az alapértelmezett méret 2000.                    |
| seekOperation          | sztring | No       | Állítsa be `seekOperation=Next` az egyeztetési sorok következő oldalának beolvasásához.                |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz tartalmazza a sor elem részleteinek gyűjteményét.

*A sor **ChargeType** az érték **megvásárlása** **újra** van leképezve, és az érték- **visszatérítés** a **megszakításra** van leképezve.*

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

## <a name="request-response-examples"></a>Kérelem – válasz példák

### <a name="request-response-example-1"></a>Kérelem – válasz 1. példa

A következő részletek a példára vonatkoznak:

- **Szolgáltató**: **egykori**
- **InvoiceLineItemType**: **UsageLineItems**
- **Időszak**: **előző**

#### <a name="request-example-1"></a>1. példa kérés

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a>1. válasz – példa

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 0,
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemTypce": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

A következő részletek a példára vonatkoznak:

- **Szolgáltató**: **egykori**
- **InvoiceLineItemType**: **UsageLineItems**
- **Időszak**: **előző**
- **SeekOperation**: **következő**

#### <a name="request-example-2"></a>2. példa a kérelemre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a>2. válasz – példa

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
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
