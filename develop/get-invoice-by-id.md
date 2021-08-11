---
title: Számla lekért azonosítója alapján
description: Lekér egy adott számlát a számlaazonosítóval.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 79327879614de521224606b69a5b6d1e8e4192f0df085f5fce61230c91e774e5
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994506"
---
# <a name="get-invoice-by-id"></a>Számla lekért azonosítója alapján

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekér egy adott számlát a számlaazonosítóval.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy érvényes számlaazonosító.

## <a name="c"></a>C\#

Számla lekért száma azonosító alapján:

1. Használja az **IPartner.Invoices gyűjteményt,** és hívja meg a **ById() metódust.**

2. Hívja meg **a Get() vagy** **a GetAsync() metódust.**

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** PartnerSDK.FeatureSample **osztály:** GetInvoice.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{számlaazonosító} HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A számla lekérdezhető a következő lekérdezési paraméterrel.

| Név           | Típus       | Kötelező | Leírás                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| **számlaazonosító** | **sztring** | Yes      | Az érték egy **számlaazonosító,** amely lehetővé teszi, hogy a viszonteladó szűrje egy adott számla eredményeit. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy [invoice erőforrást](invoice-resources.md#invoice) ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 676
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
Date: Thu, 24 Mar 2016 05:22:14 GMT

{
    "id": "G000024135",
    "invoiceDate": "2018-02-08T22:40:37.5897767Z",
    "billingPeriodStartDate": "2018-02-01T22:40:37.5897767Z",
    "billingPeriodEndDate": "2018-02-28T22:40:37.5897767Z",
    "totalCharges": 2076.63,
    "paidAmount": 0,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "pdfDownloadLink": "/invoices/G000024135/documents/statement",
    "taxReceipts": [
        {
            "id": "123456",
            "taxReceiptPdfDownloadLink": "/invoices/G000024135/receipts/123456/documents/statement"
        }
    ],
    "invoiceDetails": [
        {
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024135/lineitems/OneTime/BillingLineItems",
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
    "invoiceType": "OneTime",
    "links": {
        "self": {
            "uri": "/invoices/OneTime-G000024135",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Invoice"
    }
}
```
