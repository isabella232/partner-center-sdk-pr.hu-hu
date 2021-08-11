---
title: Partner MPN-azonosítójának ellenőrzése
description: Megtudhatja, hogyan ellenőrizheti egy partner Microsoft Partner Network-azonosítóját (MPN-azonosítóját) a partner MPN-profiljának C-n vagy a \# Partnerközpont REST API.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 223f0da94f5a1c12b4f6de32184296b88ab5f443a69feac89152acc1aa9ccbd6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995917"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Partner MPN-azonosítójának ellenőrzése C-n vagy a \# Partnerközpont REST API

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Egy partner ügyfél-azonosítójának Microsoft Partner Network (MPN-azonosító).

Az itt bemutatott technika úgy ellenőrzi a partner Microsoft Partner Network-azonosítóját, hogy lekérte a partner MPN-profilját a Partnerközpont. Az azonosító akkor minősül érvényesnek, ha a kérés sikeres volt.

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Az ellenőriznie kell a partner MPN-azonosítóját. Ha kihagyja ezt az értéket, a kérelem lekéri a bejelentkezett partner MPN-profilját.

## <a name="c"></a>C\#

A partner MPN-azonosítójának ellenőrzéséhez először az [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) tulajdonságból olvassa be a partnerprofil-gyűjtési műveletek felületét. Ezután szerezze be az MPN-profilműveleteket az [**MpnProfile tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) vagy [**GetAsync metódusokat**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) az MPN-azonosítóval az MPN-profil lekérése előtt. Ha kihagyja az MPN-azonosítót a Get vagy GetAsync hívásból, a kérés megkísérli lekérni a bejelentkezett partner MPN-profilját.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** Partnerközpont SDK **Osztály:** VerifyPartnerMpnId.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Adja meg a következő lekérdezési paramétert a partner azonosításához. Ha kihagyja ezt a lekérdezési paramétert, a kérés visszaadja a bejelentkezett partner MPN-profilját.

| Név   | Típus | Kötelező | Leírás                                                 |
|--------|------|----------|-------------------------------------------------------------|
| mpn-id | int  | No       | Egy Microsoft Partner Network azonosító, amely azonosítja a partnert. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, a válasz törzse tartalmazza a partner [MpnProfile](profile-resources.md#mpnprofile) erőforrását.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example-success"></a>Válasz példa (sikeres)

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a>Válasz példa (hiba)

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
