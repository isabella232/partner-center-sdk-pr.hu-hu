---
title: A Microsoft Partner Network-profil lekérése
description: Lekért egy objektumot, amely a partner MPN-profilját képviseli.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a4972010605f1815382fc92df76842ae5f97ca35cacfcc8428e7b9849c6b0b6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995832"
---
# <a name="get-microsoft-partner-network-profile"></a>A Microsoft Partner Network-profil lekérése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Lekért egy objektumot, amely a partner MPN-profilját képviseli.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

## <a name="c"></a>C\#

A partnerhálózati profil lehívásához használja az **IAggregatePartner.Profiles** gyűjteményt, és hívja meg **az MpnProfile** tulajdonságot. Végül hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**:P centerSDK.FeaturesSamples **osztály:** GetMPNProfile.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

A partnerhálózati profil lehívásához használja az **IAggregatePartner.getProfiles** függvényt, és hívja meg a **getMpnProfile** függvényt. Végül hívja meg a **get()** függvényt.

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A partnerhálózati profil lekért végrehajtásához hajtsa végre a [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) parancsot.

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus  | Kérés URI-ja                                                          |
|---------|----------------------------------------------------------------------|
| **Kap** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST-válasz

Ha sikeres, ez a metódus egy **MPNProfile** objektumot ad vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```
