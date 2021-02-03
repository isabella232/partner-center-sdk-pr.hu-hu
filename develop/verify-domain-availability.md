---
title: Tartomány rendelkezésre állásának ellenőrzése
description: Hogyan állapítható meg, hogy a tartomány használható-e.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 84edb5b7510642ec44dad3d4f92349e40eb10b24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768279"
---
# <a name="verify-domain-availability"></a>Tartomány rendelkezésre állásának ellenőrzése

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Hogyan állapítható meg, hogy a tartomány használható-e.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy tartomány (például `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Annak ellenőrzéséhez, hogy a tartomány elérhető-e, először hívja meg a [**IAggregatePartner. Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) -t, és szerezzen be egy felületet a tartományi műveletekhez. Ezután hívja meg a [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) metódust a tartománnyal. Ez a módszer egy adott tartományhoz elérhető műveletekhez tartozó felületet kérdez le. Végül hívja meg a [**létező**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) metódust, és ellenőrizze, hogy már létezik-e a tartomány.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: CheckDomainAvailability.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                              |
|----------|--------------------------------------------------------------------------|
| **FEJ** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Domains/{domain} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A tartomány rendelkezésre állásának ellenőrzéséhez használja a következő lekérdezési paramétert.

| Név       | Típus       | Kötelező | Leírás                                   |
|------------|------------|----------|-----------------------------------------------|
| **tartományi** | **karakterlánc** | Y        | Egy karakterlánc, amely az ellenőrzési tartományt azonosítja. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincs

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

Ha a tartomány létezik, az nem érhető el, és az 200-es válasz-állapotkód vissza lesz állítva. Ha a tartomány nem található, használható, és a 404-es válasz-állapotkód nem található.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Válasz példa arra, ha a tartomány már használatban van

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Válasz példa arra, ha a tartomány elérhető

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
