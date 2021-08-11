---
title: Ellenőrzött tartomány hozzáadása egy ügyfélhez
description: Megtudhatja, hogyan adhat hozzá ellenőrzött tartományt a jóváhagyott tartományok listájához egy ügyfél Partnerközpont. Ezt a Partnerközpont API-k és REST API-k használatával tegye.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 570008c955ce3242b02c1df4c87df52aea3627abb6c86a069cc7c4c0d1d6f799
ms.sourcegitcommit: ac8f5f8bedaddba5110dd4e562fbd9a2b24837df
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/08/2021
ms.locfileid: "116885577"
---
# <a name="add-a-verified-domain-to-the-list-of-approved-domains-for-an-existing-customer"></a>Ellenőrzött tartomány hozzáadása egy meglévő ügyfél jóváhagyott tartományának listájához 

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Ellenőrzött tartomány hozzáadása egy meglévő ügyfél jóváhagyott tartományának listájához.

## <a name="prerequisites"></a>Előfeltételek

- Tartományregisztráló partnernek kell lennie.

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** elemet Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).

## <a name="adding-a-verified-domain"></a>Ellenőrzött tartomány hozzáadása

Ha Ön egy tartományregisztráló partner, az API-val közzétethet egy új tartományerőforrást egy meglévő ügyfél `verifieddomain` tartománylistán. [](#domain) Ehhez azonosítsa az ügyfelet a CustomerTenantId azonosítóját használva. Adjon meg egy értéket a VerifiedDomainName tulajdonsághoz. A [kérelemben adja](#domain) át a szükséges Név, Képesség, Hitelesítési típus, Állapot és VerificationMethod tulajdonságokkal rendelkező tartományerőforrást. Annak megadásához, [](#domain) hogy az új tartomány összevont tartomány, állítsa [](#domain) a Tartomány erőforrás AuthenticationType tulajdonságát a következőre: , és adjon meg egy `Federated` [DomainFederationSettings](#domain-federation-settings) erőforrást a kérelemben. Ha a metódus sikeres, [a](#domain) válasz tartalmazni fog egy tartományi erőforrást az új ellenőrzött tartományhoz.

### <a name="custom-verified-domains"></a>Egyéni ellenőrzött tartományok

Egyéni ellenőrzött tartomány, a **onmicrosoft.com-on** nem regisztrált tartomány hozzáadásakor a [CustomerUser.immutableId](user-resources.md#customeruser) tulajdonságot egyedi azonosítóértékre kell állítania ahhoz az ügyfélhez, akihez hozzáadja a tartományt. Erre az egyedi azonosítóra az ellenőrzési folyamat során van szükség a tartomány ellenőrzésekor. További információ az ügyfél felhasználói fiókjairól: [Felhasználói fiókok létrehozása egy ügyfél számára.](create-user-accounts-for-a-customer.md)

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| POST   | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{CustomerTenantId}/verifieddomain HTTP/1.1 |

#### <a name="uri-parameter"></a>URI-paraméter

A következő lekérdezési paraméterrel adhatja meg azt az ügyfelet, akihez ellenőrzött tartományt ad hozzá.

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| CustomerTenantId | guid | Y        | Az érték egy **CUSTOMERTenantId** formátumú GUID, amely lehetővé teszi egy ügyfél megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név                                                  | Típus   | Kötelező                                      | Leírás                                                |
|-------------------------------------------------------|--------|-----------------------------------------------|--------------------------------------------------------|
| VerifiedDomainName (Ellenőrzött tartománynév)                                    | sztring | Yes                                           | Az ellenőrzött tartománynév. |
| [Tartomány](#domain)                                     | object | Yes                                           | A tartomány adatait tartalmazza. |
| [DomainFederationSettings](#domain-federation-settings) | object | Igen (Ha AuthenticationType = `Federated` )     | A tartomány-összevonási beállításokat akkor kell használni, ha a tartomány `Federated` tartomány, nem `Managed` pedig tartomány. |

### <a name="domain"></a>Tartomány

Ez a táblázat a  kérelem törzsében található kötelező és választható tartománytulajdonságokat ismerteti.

| Név               | Típus                                     | Kötelező | Leírás                                                                                                                                                                                                     |
|--------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AuthenticationType (Hitelesítés típusa)                                    | sztring           | Yes      | Meghatározza, hogy a tartomány `Managed` tartomány vagy `Federated` tartomány. Támogatott értékek: `Managed` , `Federated` .|
| Képesség                                            | sztring           | Yes      | Megadja a tartományi képességet. Például: `Email`.                  |
| IsDefault (Hamis)                                             | nullázható logikai érték | No       | Azt jelzi, hogy a tartomány a bérlő alapértelmezett tartománya-e. Támogatott értékek: `True` , `False` , `Null` .        |
| IsInitial (IsInitial)                                             | nullázható logikai érték | No       | Azt jelzi, hogy a tartomány kezdeti tartomány-e. Támogatott értékek: `True` , `False` , `Null` .                       |
| Name                                                  | sztring           | Yes      | A tartománynév.                                                          |
| RootDomain (Gyökértartomány)                                            | sztring           | No       | A gyökértartomány neve.                                              |
| Állapot                                                | sztring           | Yes      | A tartomány állapota. Például: `Verified`. Támogatott értékek:  `Unverified` , `Verified` , `PendingDeletion` .                               |
| VerificationMethod                                    | sztring           | Yes      | A tartomány-ellenőrzési módszer típusa. Támogatott értékek: `None` , `DnsRecord` , `Email` .                                    |

### <a name="domain-federation-settings"></a>Tartomány-összevonási beállítások

Ez a táblázat a kérés törzsében található kötelező és választható **DomainFederationSettings** tulajdonságokat ismerteti.

| Név   | Típus   | Kötelező | Leírás                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| ActiveLogOnUri                         | sztring           | No      | A gazdag ügyfelek által használt bejelentkezési URI. Ez a tulajdonság a partner STS hitelesítési URL-címe. |
| DefaultInteractiveAuthenticationMethod | sztring           | No      | Azt az alapértelmezett hitelesítési módszert jelöli, amely akkor használatos, ha egy alkalmazás interaktív bejelentkezést igényel a felhasználótól. |
| FederationBrandName (Összevonási név)                    | sztring           | No      | Az összevonási márka neve.        |
| IssuerUri (Kiállítói azonosító)                              | sztring           | Yes     | A tanúsítványok kiállítójának neve.                        |
| LogOffUri                              | sztring           | Yes     | Az kijelentkezés URI-ját. Ez a tulajdonság az összevont tartomány kijelentkező URI-ját írja le.        |
| MetadataExchangeUri                    | sztring           | No      | Az URL-cím, amely megadja a gazdag ügyfélalkalmazások hitelesítéséhez használt metaadatcsere-végpontot. |
| NextSigningCertificate (NextSigningCertificate)                 | sztring           | No      | Az ADFS V2 STS által a jogcímek aláírása érdekében a jövőben használt tanúsítvány. Ez a tulajdonság a tanúsítvány base64 kódolású ábrázolása. |
| OpenIdConnectDiscoveryEndpoint         | sztring           | No      | Az OpenID Csatlakozás az összevont IDP STS felderítési végpontját. |
| PassiveLogOnUri                        | sztring           | Yes     | A régebbi passzív ügyfelek által használt bejelentkezési URI. Ez a tulajdonság az a cím, amely összevont bejelentkezési kérelmeket küld. |
| PreferredAuthenticationProtocol        | sztring           | Yes     | A hitelesítési jogkivonat formátuma. Például: `WsFed`. Támogatott értékek: `WsFed` , `Samlp` |
| PromptLoginBehavior                    | sztring           | Yes     | A bejelentkezési viselkedés típusa.  Például: `TranslateToFreshPasswordAuth`. Támogatott értékek: `TranslateToFreshPasswordAuth` , `NativeSupport` , `Disabled` |
| SigningCertificate (Aláíró tanúsítvány)                     | sztring           | Yes     | Az ADFS V2 STS által a jogcímek aláíráshoz jelenleg használt tanúsítvány. Ez a tulajdonság a tanúsítvány base64 kódolású ábrázolása. |
| SigningCertificateUpdateStatus         | sztring           | No      | Az aláíró tanúsítvány frissítési állapotát jelzi. |
| SigningCertificateUpdateStatus         | nullázható logikai érték | No      | Jelzi, hogy az IDP STS támogatja-e az MFA-t. Támogatott értékek: `True` , `False` , `Null` .|

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

Ha ez az API sikeres, visszaad egy [tartományi](#domain) erőforrást az új ellenőrzött tartományhoz.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
