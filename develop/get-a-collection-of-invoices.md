---
title: Számlák gyűjteményének lekérése
description: A partner számlái gyűjteményének lekérése.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 7698d85df3341ae4cbff0377bd0a1bb47cd36740
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906435"
---
# <a name="get-a-collection-of-invoices"></a>Számlák gyűjteményének lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A partner számlái gyűjteményének lekérése.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

Az összes elérhető számla gyűjteményének lekéréséhez használja az [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) tulajdonságot a számlázási műveletek interfészének lekéréséhez, majd hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) vagy [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) metódust a gyűjtemény lekéréséhez.

A számlák lapozott gyűjteményének lehívásához először hívja meg a [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) metódust, és adja át neki az oldalméretet egy [**IQuery-objektum létrehozásához.**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) Ezután az [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) tulajdonság használatával kérje le a számlaműveletek interfészét, majd adja át az IQuery objektumot a [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) vagy [**a QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) metódusnak a kérés elküldését és az első oldal lekérését.

Ezután az [**Enumerator (Enumerátorok)**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) tulajdonság használatával hozzon létre egy felületet a támogatott erőforrás-gyűjtemény-enumerátorok gyűjteményéhez, majd hívja meg az [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) hívását egy enumerátor létrehozásához a számlák gyűjteményének bejárása számára. Végül az enumerátor használatával lekérheti a számlák minden oldalát, és használhatja őket az alábbi példakódban látható módon. A Next [**metódus**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) minden hívása a számlák következő oldalára vonatkozó kérést küld az oldal mérete alapján.

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

Egy kissé eltérő példáért lásd: **Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** GetPagedInvoices.cs

> [!NOTE] 
> Ugyanazt az API-t használjuk minden modern kereskedelmi vásárláshoz, valamint 145p és Office licenchez. A méret és az eltolás csak az örökölt számlák esetén lesz figyelembe véve. Minden modern kereskedelmi vásárlás esetén a rendszer figyelmen kívül & eltolást.

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1  |

### <a name="uri-parameters"></a>URI-paraméterek

A kérelem létrehozásakor használja a következő lekérdezési paramétereket.

| Név   | Típus | Kötelező | Leírás                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| size   | int  | Nem       | A válaszban visszaadni szükséges számlaerőforrások száma. Ezt a paramétert nem kötelező megadni. |
| offset | int  | Nem       | Az első vissza nem tér számlának nulla alapú indexe.                                   |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a válasz törzse tartalmazza a [számlaerőforrások gyűjteményét.](invoice-resources.md#invoice)

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
