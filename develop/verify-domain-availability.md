---
title: Tartomány rendelkezésre állásának ellenőrzése
description: Annak meghatározása, hogy egy tartomány használható-e.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530276"
---
# <a name="verify-domain-availability"></a>Tartomány rendelkezésre állásának ellenőrzése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Annak meghatározása, hogy egy tartomány használható-e.

## <a name="prerequisites"></a>Előfeltételek

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md) Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy tartomány (például `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Annak ellenőrzéséhez, hogy egy tartomány elérhető-e, először hívja meg az [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) nevet a tartományi műveletek interfészének beszerzéséhez. Ezután hívja meg [**a ByDomain metódust**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) az ellenőrzéshez használt tartománnyal. Ez a metódus lekér egy felületet az adott tartományhoz elérhető műveletekhez. Végül hívja meg az [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) metódust, hogy lássa, létezik-e már a tartomány.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** CheckDomainAvailability.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja                                                              |
|----------|--------------------------------------------------------------------------|
| **Fej** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A tartomány rendelkezésre állásának ellenőrzéséhez használja a következő lekérdezési paramétert.

| Név       | Típus       | Kötelező | Leírás                                   |
|------------|------------|----------|-----------------------------------------------|
| **Tartomány** | **sztring** | Y        | Egy sztring, amely azonosítja az ellenőriznie kell a tartományt. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha a tartomány létezik, nem használható, és a 200 OK válaszállapotkódot ad vissza. Ha a tartomány nem található, használható, és a 404 Not Found válaszállapotkódot ad vissza.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Példa válaszra, ha a tartomány már használatban van

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Példa a tartomány rendelkezésre áll-e válaszra

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
