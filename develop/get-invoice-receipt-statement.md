---
title: Számla nyugtakivonatának lekérése
description: A számlaazonosító és a nyugtaazonosító használatával lekéri a számla visszaigazolási kivonatát.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed47eadb377a94363b46cbc5508e5377cee005007698df9077d085705c7b9d08
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990732"
---
# <a name="get-invoice-receipt-statement"></a>Számla nyugtakivonatának lekérése

A számlaazonosító és a nyugtaazonosító használatával lekéri a számla visszaigazolási kivonatát.

> [!IMPORTANT]
> Ez a funkció csak Tajvan adójótátlásai esetében alkalmazható.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy érvényes számlaazonosító és egy megfelelő nyugtaazonosító.

## <a name="c"></a>C\#

Ha azonosító alapján, az Partnerközpont SDK 1.12.0-s és az 1.12.0-stól kezdődően a számlakivonatot  azonosító alapján le kell kapnia, használja az **IPartner.Invoices** gyűjteményt, és hívja meg a **ById()** metódust a számlaazonosító használatával, majd hívja meg a **Documents()** és a **Statement() metódusokat** a számlakivonat eléréséhez.  Végül hívja meg a **Get() vagy** **a GetAsync() metódust.**

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** PartnerSDK.FeatureSample **osztály:** GetInvoiceReceiptStatement.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{számlaazonosító}/receipts/{nyugtaazonosító}/documents/statement HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterrel lekérdezheti a számla visszaigazolási kivonatát.

| Név       | Típus   | Kötelező | Leírás                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| számlaazonosító | sztring | Yes      | Az érték egy számlaazonosító, amely lehetővé teszi, hogy a viszonteladó szűrje egy adott számla eredményeit. |
| nyugta-azonosító | sztring | Yes      | Az érték egy nyugtaazonosító, amely lehetővé teszi, hogy a viszonteladó szűrje egy adott számla nyugtáit. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy PDF-streamet ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
