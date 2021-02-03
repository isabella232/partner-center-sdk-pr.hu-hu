---
title: Partner MPN-azonosítójának ellenőrzése
description: Megtudhatja, hogyan ellenőrizheti egy partner Microsoft Partner Network-azonosítóját (MPN-AZONOSÍTÓját) a partner MPN-profiljának C \# -n vagy a partner Center-REST API keresztül történő kérelmezésével.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768500"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>Partner MPN-azonosító ellenőrzése C \# vagy a partner Center REST API használatával

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Partner Microsoft Partner Network-azonosítójának (MPN-azonosító) ellenőrzése

Az itt bemutatott módszer ellenőrzi a partner Microsoft Partner Network azonosítóját, ha a partneri MPN-profilt kéri a partner Centertől. Az azonosító akkor minősül érvényesnek, ha a kérelem sikeres.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- A partner MPN-AZONOSÍTÓjának ellenőrzése. Ha kihagyja ezt az értéket, a kérelem lekéri a bejelentkezett partner MPN-profilját.

## <a name="c"></a>C\#

A partner MPN-AZONOSÍTÓjának ellenőrzéséhez először kérjen le egy felületet a [**IAggregatePartner. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) tulajdonságból a partneri profil gyűjtési műveleteihez. Ezután szerezzen be egy felületet az MPN-profil műveleteihez a [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) tulajdonságból. Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) metódust az MPN-azonosítóval az MPN-profil lekéréséhez. Ha kihagyja az MPN-azonosítót a Get vagy a GetAsync hívásból, a kérelem megkísérli a bejelentkezett partner MPN-profiljának beolvasását.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: VerifyPartnerMpnId.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN? mpnId = {MPN-ID} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Adja meg a következő lekérdezési paramétert a partner azonosításához. Ha kihagyja ezt a lekérdezési paramétert, a kérelem a bejelentkezett partner MPN-profilját adja vissza.

| Név   | Típus | Kötelező | Leírás                                                 |
|--------|------|----------|-------------------------------------------------------------|
| MPN-azonosító | int  | Nem       | A partnert azonosító Microsoft Partner Network-azonosító. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

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

Ha a művelet sikeres, a válasz törzse tartalmazza a partner [MpnProfile](profile-resources.md#mpnprofile) -erőforrását.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
