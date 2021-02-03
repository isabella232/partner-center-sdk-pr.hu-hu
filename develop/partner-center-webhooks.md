---
title: Partnerközpont – webhookok
description: A webhookok lehetővé teszik a partnerek számára az Erőforrás-változási események regisztrálását.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8225623ade7e922ac23ebf0ed9215686b0601244
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768024"
---
# <a name="partner-center-webhooks"></a>Partnerközpont – webhookok

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partner Center webhook API-k lehetővé teszik a partnerek számára az Erőforrás-változási események regisztrálását. Ezeket az eseményeket a rendszer HTTP-bejegyzések formájában továbbítja a partner regisztrált URL-címére. A partneri központból érkező események fogadásához a partnerek visszahívást kapnak, ahol a partner Center közzéteheti az erőforrás-módosítási eseményt. Az esemény digitálisan alá lesz írva, hogy a partner ellenőrizze, hogy a partner központból küldték-e el.

A partnerek a partner Center által támogatott webhook-eseményekről választhatnak, például a következő példákkal.

- **Tesztelési esemény ("test-created")**

    Ez az esemény lehetővé teszi, hogy saját bevezetést kérjen, és tesztelje a regisztrációt egy tesztelési esemény megadásával, majd a folyamat nyomon követésével. Megtekintheti a Microsofttól érkező hibaüzeneteket, amikor az eseményt próbálja kézbesíteni. Ez a korlátozás csak a "test-created" eseményekre vonatkozik. A hét napnál régebbi adatértékek törlődnek.

- **Előfizetés frissített eseménye ("előfizetés-frissítve")**

    Ez az esemény az előfizetés változásakor következik be. Ezek az események akkor jönnek létre, ha a partner Center API-n keresztül végzett módosítások mellett belső módosítás is történik.

    >[!NOTE]
    >Az előfizetés változásai és az előfizetés frissített eseményének megváltozása közötti időtartam 48 óra.

- **Túllépte a küszöbértéket ("usagerecords-thresholdExceeded")**

    Ez az esemény akkor következik be, ha az ügyfél Microsoft Azure használatának mennyisége meghaladja a használati költségekkel kapcsolatos költségvetést (a küszöbértéket). További információ: [Azure-beli kiadások költségvetésének beállítása ügyfeleinek/partner-központ/set-an-Azure-költőpénzt-Budget-for-your-Customs).

- **Hivatkozó létrehozott esemény ("hivatkozó-létrehozva")**

    Ez az esemény az átirányítás létrehozásakor következik be.

- **Hivatkozó frissített esemény ("referral-frissítve")**

    Ez az esemény az átirányítás frissítésekor következik be.

- **Számla üzemkész eseménye ("számla kész")**

    Ez az esemény akkor következik be, amikor az új számla elkészült.

A jövőbeli webhook-események hozzáadódnak a rendszeren megjelenő olyan erőforrásokhoz, amelyek a partner által nem vezéreltek, és további frissítésekre kerül majd, hogy a lehető legrövidebb idő alatt megkapják ezeket az eseményeket. A partnerek visszajelzései hasznosak lehetnek a felvenni kívánt új események meghatározásához.

A partner Center által támogatott webhook-események teljes listáját a következő témakörben talál: a [partner Center webhook eseményei](partner-center-webhook-events.md).

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

## <a name="receiving-events-from-partner-center"></a>Események fogadása a partner központtól

A partner Centertől érkező események fogadásához közzé kell tenni egy nyilvánosan elérhető végpontot. Mivel ez a végpont elérhető, ellenőriznie kell, hogy a kommunikáció a partner központból származik-e. A kapott webhook-események digitális aláírása a Microsoft gyökeréhez tartozó tanúsítvánnyal történik. A rendszer az esemény aláírásához használt tanúsítványra mutató hivatkozást is biztosít. Ez lehetővé teszi a tanúsítvány megújítását anélkül, hogy újból üzembe kellene helyeznie vagy konfigurálnia kell a szolgáltatást. A partner Center 10 kísérletet tesz az esemény kézbesítésére. Ha az esemény még nem érkezik meg 10 próbálkozás után, akkor a rendszer egy offline várólistába helyezi, és nem hajt végre további kísérleteket a kézbesítéskor.

Az alábbi példa egy, a partner Centerből közzétett eseményt mutat be.

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

>[!NOTE]
>Az engedélyezési fejléc "Signature" sémával rendelkezik. Ez a tartalom Base64 kódolású aláírása.

## <a name="how-to-authenticate-the-callback"></a>A visszahívás hitelesítése

A partner Centertől kapott visszahívási esemény hitelesítéséhez kövesse az alábbi lépéseket:

1. Ellenőrizze, hogy jelen vannak-e a szükséges fejlécek (Engedélyezés, x-MS-Certificate-URL, x-MS-Signature-algoritmus).

2. Töltse le a tartalom aláírásához használt tanúsítványt (x-MS-Certificate-URL).

3. Ellenőrizze a tanúsítványlánc utasításait.

4. Ellenőrizze a tanúsítvány "szervezetét".

5. Az UTF8 kódolású tartalom beolvasása pufferbe.

6. Hozzon létre egy RSA titkosítási szolgáltatót.

7. Győződjön meg arról, hogy a megadott kivonatoló algoritmussal (például SHA256) aláírt adatértékek megfelelnek-e.

8. Ha az ellenőrzés sikeres, dolgozza fel az üzenetet.

> [!NOTE]
> Alapértelmezés szerint az aláírási jogkivonat egy engedélyezési fejlécben lesz elküldve. Ha a **SignatureTokenToMsSignatureHeader** értéke TRUE (igaz) értékre van állítva a regisztrációban, az aláírási tokent az x-MS-Signature fejlécben küldi el a rendszer.

## <a name="event-model"></a>Eseményvezérelt modell

A következő táblázat a partneri központ eseményeinek tulajdonságait ismerteti.

### <a name="properties"></a>Tulajdonságok

| Név                      | Leírás                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | Az esemény neve. A (z) {Resource} – {Action} formátumban. Például: "test-created".  |
| **ResourceUri**           | A módosult erőforrás URI-ja.                                                 |
| **ResourceName**          | A módosult erőforrás neve.                                                |
| **AuditUrl**              | Választható. A naplózási rekord URI-ja.                                                |
| **ResourceChangeUtcDate** | A dátum és az idő UTC formátumban, amikor az erőforrás megváltozása megtörtént.                  |

### <a name="sample"></a>Sample

Az alábbi példa egy partner Center-esemény szerkezetét mutatja be.

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a>Webhook API-k

### <a name="authentication"></a>Hitelesítés

A webhook API-kon lévő összes hívást az engedélyezési fejléc tulajdonosi jogkivonatának használatával hitelesíti a rendszer. Hozzáférési jogkivonat beszerzése a hozzáféréshez `https://api.partnercenter.microsoft.com` . Ez a jogkivonat ugyanaz a jogkivonat, amely a partner Center API-k további részeinek elérésére szolgál.

### <a name="get-a-list-of-events"></a>Események listájának beolvasása

A webhook API-k által jelenleg támogatott események listáját adja vissza.

### <a name="resource-url"></a>Erőforrás URL-címe

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a>Példa kérésre

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US

[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```

### <a name="register-to-receive-events"></a>Regisztrálás az események fogadására

Regisztrálja a bérlőt a megadott események fogadásához.

#### <a name="resource-url"></a>Erőforrás URL-címe

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Példa kérésre

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="view-a-registration"></a>Regisztráció megtekintése

Egy bérlő webhookok eseményének regisztrációját adja vissza.

#### <a name="resource-url"></a>Erőforrás URL-címe

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Példa kérésre

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="update-an-event-registration"></a>Esemény-regisztráció frissítése

Egy meglévő esemény regisztrációjának frissítése.

#### <a name="resource-url"></a>Erőforrás URL-címe

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a>Példa kérésre

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="send-a-test-event-to-validate-your-registration"></a>Tesztelési esemény küldése a regisztráció érvényesítéséhez

Tesztelési eseményt hoz létre a webhookok regisztrálásának ellenőrzéséhez. Ez a teszt arra szolgál, hogy ellenőrizze, hogy tud-e eseményeket fogadni a partner központból. Az események adatai a kezdeti esemény létrehozása után hét nappal törlődnek. Az érvényesítési esemény elküldése előtt regisztrálnia kell a "test-created" eseményhez a regisztrációs API használatával.

>[!NOTE]
>Egy érvényesítési esemény közzétételekor percenként 2 kérelem van.

#### <a name="resource-url"></a>Erőforrás URL-címe

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a>Példa kérésre

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```

### <a name="verify-that-the-event-was-delivered"></a>Az esemény kézbesítésének ellenőrzése

Az érvényesítési esemény aktuális állapotát adja vissza. Ez az ellenőrzés hasznos lehet az esemény-kézbesítési problémák elhárításához. A válasz az esemény továbbítására tett összes kísérlet eredményét tartalmazza.

#### <a name="resource-url"></a>Erőforrás URL-címe

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a>Példa kérésre

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```

## <a name="example-for-signature-validation"></a>Példa aláírás-ellenőrzésre

### <a name="sample-callback-controller-signature-aspnet"></a>Minta visszahívási vezérlő aláírása (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>Aláírás ellenőrzése

Az alábbi példa bemutatja, hogyan adhat hozzá olyan engedélyezési attribútumot a vezérlőhöz, amely fogadja a webhook eseményeinek visszahívásait.

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // for example RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
