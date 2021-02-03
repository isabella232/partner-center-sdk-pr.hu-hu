---
title: Számla nyugtakivonatának lekérése
description: A számla-azonosító és a bevételezési azonosító használatával kérdezi le a számlázási bevételezési utasítást.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767683"
---
# <a name="get-invoice-receipt-statement"></a>Számla nyugtakivonatának lekérése

**A következőkre vonatkozik**

- Partnerközpont

A számla-azonosító és a bevételezési azonosító használatával kérdezi le a számlázási bevételezési utasítást.

> [!IMPORTANT]
> Ez a funkció csak a tajvani adóbevallásokra vonatkozik.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Egy érvényes számla-azonosító és egy megfelelő nyugta-azonosító.

## <a name="c"></a>C\#

Ha azonosító alapján szeretné beolvasni a számla bevételezési utasítását, a partner Center SDK v 1.12.0 kezdődően, használja a **IPartner. számlák** gyűjteményt, és hívja meg a **ById ()** METÓDUSt a számla azonosítójának használatával, majd hívja meg a **beérkezési** gyűjteményt, hívja meg a **ById ()** , majd hívja meg a **Documents ()** és a **utasítás ()** metódust a számla Végül hívja meg a **Get ()** vagy a **GetAsync ()** metódust.

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample **osztály**: GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/receipts/{Receipt-ID}/Documents/Statement http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Használja a következő lekérdezési paramétert a számla bevételezési utasításának beolvasásához.

| Név       | Típus   | Kötelező | Leírás                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| számlázási azonosító | sztring | Igen      | Az érték egy számlázási azonosító, amely lehetővé teszi, hogy a viszonteladó egy adott számla eredményét szűrje. |
| nyugta – azonosító | sztring | Igen      | Az érték egy nyugtát azonosító, amely lehetővé teszi, hogy a viszonteladó szűrni lehessen egy adott számla nyugtáit. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincs

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a metódus egy PDF-streamet ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
