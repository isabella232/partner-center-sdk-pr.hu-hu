---
title: Támogatási profil lekérése
description: Lekért egy objektumot, amely a felhasználó támogatási profilját képviseli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b112ccbbff731795c21f95845a08be9e9dfb6775
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548634"
---
# <a name="get-support-profile"></a>Támogatási profil lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekért egy objektumot, amely a felhasználó támogatási profilját képviseli.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="c"></a>C\#

A támogatási profilhoz használja az **IAggregatePartner.Profiles gyűjteményt.** Hívja meg [**a SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) tulajdonságot, majd a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync)

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project:** PartnerCenterSDK.FeaturesSamples **osztály:** GetSupportProfile.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus  | Kérés URI-ja                                                              |
|---------|--------------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a metódus egy **SupportProfile** objektumot ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```
