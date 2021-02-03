---
title: Ellenőrzött tartomány hozzáadása egy ügyfélhez
description: Megtudhatja, hogyan adhat hozzá ellenőrzött tartományt a partner Centerben lévő ügyfél jóváhagyott tartományának listájához. Ezt a partner Center API-k és a REST API-k használatával teheti meg.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d0ea9998324e99c7986645dc90fdfba0a2a71571
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768519"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Ellenőrzött tartomány hozzáadása egy meglévő ügyfél jóváhagyott tartományának listájához 

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

Ellenőrzött tartomány hozzáadása egy meglévő ügyfél jóváhagyott tartományának listájához.

## <a name="prerequisites"></a>Előfeltételek

- Olyan partnernek kell lennie, aki egy tartományregisztráló.

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="adding-a-verified-domain"></a>Ellenőrzött tartomány hozzáadása

Ha Ön olyan partner, aki egy tartományregisztráló, az `verifieddomain` API-val új [tartományi](#domain) erőforrást küldhet egy meglévő ügyfél tartományának listájára. Ehhez azonosítsa az ügyfelet a CustomerTenantId használatával. A VerifiedDomainName tulajdonság értékének megadása. Adjon át egy [tartományi](#domain) erőforrást a kérelemben a szükséges névvel, képességgel, AuthenticationType, állapottal és VerificationMethod tulajdonságokkal. Annak megadásához, hogy az új [tartomány](#domain) összevont tartomány legyen, állítsa a AuthenticationType tulajdonságot a [tartományba](#domain) , `Federated` és vegyen fel egy [DomainFederationSettings](#domain-federation-settings) -erőforrást a kérelembe. Ha a metódus sikeres, a válasz tartalmazni fog egy [tartományi](#domain) erőforrást az új ellenőrzött tartományhoz.

### <a name="custom-verified-domains"></a>Egyéni ellenőrzött tartományok

Egyéni ellenőrzött tartomány hozzáadásakor egy olyan tartomány, amely nincs regisztrálva a **onmicrosoft.com**-on, a [CustomerUser. immutableId](user-resources.md#customeruser) tulajdonságot egy egyedi azonosító értékre kell állítani ahhoz az ügyfélhez, amelyhez a tartományt hozzá kívánja adni. Ez az egyedi azonosító szükséges az érvényesítési folyamat során a tartomány ellenőrzésekor. További információ az ügyfél felhasználói fiókjairól: [felhasználói fiókok létrehozása az ügyfélhez](create-user-accounts-for-a-customer.md).

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{CustomerTenantId}/verifieddomain http/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméter használatával adja meg azt az ügyfelet, amelyhez ellenőrzött tartományt ad hozzá.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Az érték egy GUID formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.

| Név                                                  | Típus   | Kötelező                                      | Leírás                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName                                    | sztring | Igen                                           | Az ellenőrzött tartomány neve. |
| [Tartomány](#domain)                                     | object | Igen                                           | A tartományi információkat tartalmazza. |
| [DomainFederationSettings](#domain-federation-settings) | object | Igen (IF AuthenticationType = `Federated` )     | A tartományi összevonási beállítások, amelyeket akkor kell használni, ha a tartomány `Federated` tartomány, és nem `Managed` tartomány. |

### <a name="domain"></a>Tartomány

Ez a táblázat a kérés törzsének kötelező és választható **tartomány** -tulajdonságait ismerteti.

| Név               | Típus                                     | Kötelező | Leírás                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType                                    | sztring           | Igen      | Meghatározza, hogy a tartomány `Managed` tartomány vagy tartomány-e `Federated` . Támogatott értékek: `Managed` , `Federated` .|
| Képesség                                            | sztring           | Igen      | Megadja a tartományi képességet. Például: `Email`.                  |
| IsDefault                                             | NULL értékű logikai érték | Nem       | Azt jelzi, hogy a tartomány a bérlő alapértelmezett tartománya-e. Támogatott értékek: `True` , `False` , `Null` .        |
| IsInitial                                             | NULL értékű logikai érték | Nem       | Azt jelzi, hogy a tartomány kezdeti tartomány-e. Támogatott értékek: `True` , `False` , `Null` .                       |
| Name                                                  | sztring           | Igen      | A tartománynév.                                                          |
| RootDomain                                            | sztring           | No       | A gyökértartomány neve.                                              |
| Állapot                                                | sztring           | Igen      | A tartomány állapota. Például: `Verified`. Támogatott értékek:  `Unverified` , `Verified` , `PendingDeletion` .                               |
| VerificationMethod                                    | sztring           | Igen      | A tartomány-ellenőrzési módszer típusa. Támogatott értékek: `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Tartományi összevonási beállítások

Ez a táblázat a kérés törzsének kötelező és választható **DomainFederationSettings** tulajdonságait ismerteti.

| Név   | Típus   | Kötelező | Leírás                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | sztring           | No      | A gazdag ügyfelek által használt bejelentkezési URI. Ez a tulajdonság a partner STS-hitelesítésének URL-címe. |
| DefaultInteractiveAuthenticationMethod | sztring           | No      | Megadja az alapértelmezett hitelesítési módszert, amelyet akkor kell használni, ha egy alkalmazásnak interaktív bejelentkezésre van szüksége a felhasználónak. |
| FederationBrandName                    | sztring           | No      | Az összevonási márka neve.        |
| IssuerUri                              | sztring           | Igen     | A tanúsítványok kiállítójának neve.                        |
| LogOffUri                              | sztring           | Igen     | A kijelentkezés URI-ja. Ez a tulajdonság az összevont tartomány kijelentkezési URI-JÁT ismerteti.        |
| MetadataExchangeUri                    | sztring           | No      | Az URL-cím, amely a gazdag ügyfélalkalmazások általi hitelesítéshez használt metaadat-Exchange-végpontot határozza meg. |
| NextSigningCertificate                 | sztring           | No      | Az ADFS v2 STS által a jogcímek aláírásához használt tanúsítvány. Ez a tulajdonság a tanúsítvány Base64 kódolású ábrázolása. |
| OpenIdConnectDiscoveryEndpoint         | sztring           | No      | Az összevont IDENTITÁSSZOLGÁLTATÓ STS-kapcsolatának az OpenID Connect-felderítési végpontja. |
| PassiveLogOnUri                        | sztring           | Igen     | A régebbi passzív ügyfelek által használt bejelentkezési URI. Ez a tulajdonság az összevont bejelentkezési kérelmek küldésének címe. |
| PreferredAuthenticationProtocol        | sztring           | Igen     | A hitelesítési jogkivonat formátuma. Például: `WsFed`. Támogatott értékek: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | sztring           | Igen     | A bejelentkezés kérésének viselkedési típusa.  Például: `TranslateToFreshPasswordAuth`. Támogatott értékek: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate                     | sztring           | Igen     | Az ADFS v2 STS által a jogcímek aláírására jelenleg használt tanúsítvány. Ez a tulajdonság a tanúsítvány Base64 kódolású ábrázolása. |
| SigningCertificateUpdateStatus         | sztring           | No      | Az aláíró tanúsítvány frissítési állapotát jelzi. |
| SigningCertificateUpdateStatus         | NULL értékű logikai érték | Nem      | Azt jelzi, hogy a IDENTITÁSSZOLGÁLTATÓ STS támogatja-e az MFA-t. Támogatott értékek: `True` , `False` , `Null` .|

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
    "VerifiedDomainName": "Example.com",
    "Domain": {
        "AuthenticationType": "Federated",
        "Capability": "Email",
        "IsDefault": Null,
        "IsInitial": Null,
        "Name": "Example.com",
        "RootDomain": null,
        "Status": "Verified",
        "VerificationMethod": "None"
    },
    "DomainFederationSettings": {
        "ActiveLogOnUri": "https://sts.microsoftonline.com/FederationPassive/",
        "DefaultInteractiveAuthenticationMethod": "http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password",
        "FederationBrandName": "FederationBrandName",
        "IssuerUri": "Example.com",
        "LogOffUri": "https://sts.microsoftonline.com/FederationPassive/",
        "MetadataExchangeUri": null,
        "NextSigningCertificate": null,
        "OpenIdConnectDiscoveryEndpoint": "https://sts.contoso.com/adfs/.well-known/openid-configuration",
        "PassiveLogOnUri": "https://sts.microsoftonline.com/Trust/2005/UsernameMixed",
        "PreferredAuthenticationProtocol": "WsFed",
        "PromptLoginBehavior": "TranslateToFreshPasswordAuth",
        "SigningCertificate": <Certificate Signature goes here>,
        "SigningCertificateUpdateStatus": null,
        "SupportsMfa": true
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, az API egy [tartományi](#domain) erőforrást ad vissza az új ellenőrzött tartományhoz.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 Created
Content-Length: 206
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "authenticationType": "federated",
    "capability": "email",
    "isDefault": false,
    "isInitial": false,
    "name": "Example.com",
    "status": "verified",
    "verificationMethod": "dns_record"
}
```
