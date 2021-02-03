---
title: Számlakivonat lekérése
description: A számla AZONOSÍTÓjának lekérése a számlázási utasítás alapján.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 42e5201919eea5644da463dfe2584c8d55002083
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767884"
---
# <a name="get-invoice-statement"></a>Számlakivonat lekérése

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A számla AZONOSÍTÓjának lekérése a számlázási utasítás alapján.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Érvényes számla-azonosító.

## <a name="c"></a>C\#

Ha azonosító alapján szeretne számlát kapni, használja a **IPartner. számlákon** gyűjteményt, és hívja meg a **ById ()** METÓDUSt a számla azonosítójának használatával, majd hívja meg a **Documents ()** és a **utasítás ()** metódust a számla-utasítás eléréséhez. Végül hívja meg a **Get ()** vagy a **GetAsync ()** metódust.

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: PartnerSDK. FeatureSample **osztály**: GetInvoiceStatement.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Invoices/{Invoice-ID}/Documents/Statement http/1.1  |

### <a name="uri-parameter"></a>URI-paraméter

A számlakivonat beszerzéséhez használja a következő lekérdezési paramétert.

| Név       | Típus       | Kötelező | Leírás                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| számlázási azonosító | sztring     | Igen      | Az érték egy számlázási azonosító, amely lehetővé teszi, hogy a viszonteladó egy adott számla eredményét szűrje. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincs

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus egy [InvoiceStatement](invoice-resources.md#invoicestatement) -erőforrást ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
