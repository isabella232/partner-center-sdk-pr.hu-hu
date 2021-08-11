---
title: Számlakivonat lekérése
description: Lekér egy számlakivonatot a számlaazonosítóval.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 97a0ee60b2cb57d3413d341ceea10e267fc1660c83fccbbc20353c3ad6bfc8c2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994489"
---
# <a name="get-invoice-statement"></a>Számlakivonat lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy érvényes számlaazonosító.

## <a name="c"></a>C\#

A számlakivonat azonosító alapján való lehívásához használja az **IPartner.Invoices** gyűjteményt, és hívja meg a **ById()** metódust a számlaazonosítóval, majd hívja meg a **Documents()** és a **Statement() metódusokat** a számlakivonat eléréséhez. Végül hívja meg a **Get() vagy** **a GetAsync() metódust.**

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: PartnerSDK.FeatureSample **osztály:** GetInvoiceStatement.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{számlaazonosító}/documents/statement HTTP/1.1  |

### <a name="uri-parameter"></a>URI-paraméter

Az alábbi lekérdezési paraméterrel lekérdezheti a számlakivonatot.

| Név       | Típus       | Kötelező | Leírás                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| számlaazonosító | sztring     | Yes      | Az érték egy számlaazonosító, amely lehetővé teszi, hogy a viszonteladó szűrje egy adott számla eredményeit. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy [InvoiceStatement erőforrást](invoice-resources.md#invoicestatement) ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

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
