---
title: Tartomány rendelkezésre állásának ellenőrzése
description: Annak meghatározása, hogy egy tartomány használható-e.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3515216127219908aeefb2e070b138e75dc1f0e72b1f57f07f1dbff65ab79558
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989049"
---
# <a name="verify-domain-availability"></a>Tartomány rendelkezésre állásának ellenőrzése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Annak meghatározása, hogy egy tartomány használható-e.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy tartomány (például `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Annak ellenőrzéséhez, hogy egy tartomány elérhető-e, először hívja meg az [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) nevet a tartományi műveletek interfészének beszerzéséhez. Ezután hívja meg [**a ByDomain metódust**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) az ellenőrzéshez a tartománnyal. Ez a metódus lekér egy felületet az adott tartományhoz elérhető műveletekhez. Végül hívja meg az [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) metódust, hogy lássa, létezik-e már a tartomány.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** CheckDomainAvailability.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

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

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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

### <a name="response-example-for-when-the-domain-is-available"></a>Példa válaszra, ha a tartomány elérhető

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
