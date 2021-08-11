---
title: Partnerközpont – webhookok
description: A webhookokkal a partnerek regisztrálnak az erőforrás-módosítási eseményekre.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: cf063579b447601fa1050d6b03e0c46f6ef64abef9bb500598a047ac40ddaa1d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997549"
---
# <a name="partner-center-webhooks"></a>Partnerközpont – webhookok

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont Webhook API-k lehetővé teszik a partnerek számára az erőforrás-változási eseményekre való regisztrációt. Ezeket az eseményeket HTTP POS-ként kézbesíti a rendszer a partner regisztrált URL-címére. Ha eseményt fogadnak a Partnerközpont, a partnerek visszahívást fognak fogadni, Partnerközpont postán közzétenik az erőforrás-módosítási eseményt. Az esemény digitálisan lesz aláírva, így a partner ellenőrizheti, hogy az esemény el lett-e küldve Partnerközpont.

A partnerek az alábbi példákhoz hasonló webhookesemények közül választhatnak, amelyet a Partnerközpont.

- **Tesztesemény ("test-created")**

    Ez az esemény lehetővé teszi, hogy önkiszolgálóan regisztrálja és tesztelje a regisztrációt egy tesztesemény kérésével, majd a folyamat előrehaladásának nyomon követésével. Láthatja a Microsofttól az esemény kézbesítése közben kapott hibaüzeneteket. Ez a korlátozás csak a "teszt által létrehozott" eseményekre vonatkozik. A hét napnál régebbi adatokat a rendszer kiüríti.

- **Előfizetés-frissített esemény ("subscription-updated")**

    Ez az esemény akkor történik, amikor az előfizetés megváltozik. Ezek az események akkor jönnek létre, ha belső változás történik azon felül, hogy a módosítások a Partnerközpont API-n keresztül történnek.

    >[!NOTE]
    >Akár 48 órás késés is lehet az előfizetések módosulása és az Előfizetés frissítése esemény aktiválása között.

- **Küszöbérték túllépve esemény ("usagerecords-thresholdExceeded")**

    Ez az esemény akkor történik, amikor Microsoft Azure ügyfél használati költségének kihasználtsága meghaladja a használati költségkeretét (a küszöbértékét). További információ: [Azure-költségvetés beállítása az ügyfelek számára/partner-center/set-an-azure-spending-budget-for-your-customers).

- **Ajánlás által létrehozott esemény ("hivatkozás létrehozva")**

    Ez az esemény a hivatkozás létrehozásakor jön létre.

- **A hivatkozás frissített eseménye ("hivatkozás frissítve")**

    Ez az esemény a hivatkozás frissítésekor történik.

- **Számla kész esemény ("számla kész")**

    Ez az esemény akkor történik, amikor az új számla elkészült.

A jövőbeli webhookesemények olyan erőforrásokhoz lesznek hozzáadva, amelyek a partner által nem vezérelt rendszerben változnak, és további frissítések történnek, hogy az események a lehető legközelebb legyenek a "valós időhöz". A partnerektől származó visszajelzések, amelyek alapján az események értéket képviselnek a vállalatuk számára, hasznosak lehetnek annak meghatározásában, hogy milyen új eseményeket kell hozzáadniuk.

A Partnerközpont által támogatott webhookesemények teljes listájáért lásd Partnerközpont [eseményeket.](partner-center-webhook-events.md)

## <a name="prerequisites"></a>Előfeltételek

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="receiving-events-from-partner-center"></a>Események fogadása a Partnerközpont

Ha eseményeket Partnerközpont, egy nyilvánosan elérhető végpontot kell elérhetővé tennie. Mivel ez a végpont elérhető, ellenőriznie kell, hogy a kommunikáció a Partnerközpont. Minden kapott webhook-esemény digitálisan alá van írva egy tanúsítvánnyal, amely a Microsoft-gyökérhez csatlakozik. A szolgáltatás az esemény aláíráshoz használt tanúsítványra mutató hivatkozást is biztosít. Ez lehetővé teszi a tanúsítvány megújítását anélkül, hogy újra üzembe kellene állítania vagy újra kellene konfigurálnia a szolgáltatást. Partnerközpont 10 kísérletet tesz az esemény kézbesítésére. Ha az esemény 10 próbálkozás után sem lesz kézbesítve, akkor az offline üzenetsorba kerül, és a kézbesítéskor nem kísérlünk meg további kísérleteket.

Az alábbi minta egy, a Partnerközpont.

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
>Az Authorization fejléc "Signature" sémával rendelkezik. Ez a tartalom base64 kódolású aláírása.

## <a name="how-to-authenticate-the-callback"></a>A visszahívás hitelesítése

Az eseménytől kapott visszahívási esemény hitelesítéséhez Partnerközpont alábbi lépéseket:

1. Ellenőrizze, hogy a szükséges fejlécek jelen vannak-e (Engedélyezés, x-ms-certificate-url, x-ms-signature-algorithm).

2. Töltse le a tartalom aláíráshoz használt tanúsítványt (x-ms-certificate-url).

3. Ellenőrizze a tanúsítványláncot.

4. Ellenőrizze a tanúsítvány "Szervezet" tanúsítványát.

5. Olvassa be a tartalmat UTF8-kódolással egy pufferbe.

6. RSA titkosítási szolgáltató létrehozása.

7. Ellenőrizze, hogy az adatok megegyeznek-e a megadott kivonatolási algoritmussal aláírt adatokkal (például SHA256).

8. Ha az ellenőrzés sikeres, feldolgozta az üzenetet.

> [!NOTE]
> Alapértelmezés szerint az aláírási jogkivonat egy Authorization fejlécben lesz elküldve. Ha a regisztrációban a **SignatureTokenToMsSignatureHeader** true (igaz) értékre van állítva, az aláírási jogkivonat ehelyett az x-ms-signature fejlécben lesz elküldve.

## <a name="event-model"></a>Eseménymodell

Az alábbi táblázat a Partnerközpont tulajdonságait ismerteti.

### <a name="properties"></a>Tulajdonságok

| Név                      | Leírás                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | Az esemény neve. A következő formában: {resource}-{action}. Például: "test-created".  |
| **ResourceUri (Erőforrás-azonosító)**           | A módosított erőforrás URI-ját.                                                 |
| **ResourceName (Erőforrásnév)**          | A módosított erőforrás neve.                                                |
| **AuditUrl (Naplózásiurl)**              | Választható. A naplórekord URI-ját.                                                |
| **ResourceChangeUtcDate (Erőforrás-felcserélési csomópont)** | Az erőforrás változásának dátuma és időpontja (UTC formátumban).                  |

### <a name="sample"></a>Sample

Az alábbi minta egy esemény Partnerközpont mutatja be.

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

A webhook API-k hívásait az engedélyezési fejlécben található Bearer token hitelesíti. Hozzáférési jogkivonat beszerzése a `https://api.partnercenter.microsoft.com` eléréséhez. Ez a jogkivonat ugyanaz a jogkivonat, amely a többi api-hoz való Partnerközpont használ.

### <a name="get-a-list-of-events"></a>Események listájának lekért listája

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

### <a name="register-to-receive-events"></a>Regisztrálás események fogadására

Regisztrál egy bérlőt a megadott események fogadására.

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

Egy bérlő webhook-eseményregisztrációját adja vissza.

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

### <a name="update-an-event-registration"></a>Eseményregisztráció frissítése

Frissíti a meglévő eseményregisztrációt.

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

### <a name="send-a-test-event-to-validate-your-registration"></a>Tesztesemény küldése a regisztráció ellenőrzéshez

Létrehoz egy teszteseményt a webhookok regisztrációja érvényesítéséhez. A teszt célja annak ellenőrzése, hogy fogadhat-e eseményeket a Partnerközpont. Ezeknek az eseményeknek az adatai hét nappal a kezdeti esemény létrehozása után törlődnek. Érvényesítési esemény küldése előtt regisztrálnia kell a "test-created" eseményre a regisztrációs API-val.

>[!NOTE]
>Érvényesítési esemény közzétételével percenként 2 kérelemre van korlátozva.

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

Az érvényesítési esemény aktuális állapotát adja vissza. Ez az ellenőrzés hasznos lehet az események kézbesítésével kapcsolatos problémák elhárításában. A Válasz az esemény kézbesítésére tett minden egyes kísérlet eredményét tartalmazza.

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

## <a name="example-for-signature-validation"></a>Példa az aláírás-ellenőrzésre

### <a name="sample-callback-controller-signature-aspnet"></a>Minta visszahívási vezérlő aláírása (ASP.NET)

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a>Aláírás-ellenőrzés

Az alábbi példa bemutatja, hogyan adhat hozzá engedélyezési attribútumot a webhookesemények visszahívásait fogadó vezérlőhöz.

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
