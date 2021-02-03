---
title: A Microsoft Ügyfélszerződés szerződési metaadatainak lekérése
description: Ez a cikk azt ismerteti, hogyan kérheti le a Microsoft ügyfél-szerződéshez tartozó szerződési metaadatokat.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768163"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>A Microsoft Ügyfélszerződés szerződési metaadatainak lekérése

**A következőkre vonatkozik:**

- Partnerközpont

A partner Center jelenleg csak a *Microsoft nyilvános felhőben* támogatja a Microsoft ügyfél-szerződési metaadatokat. A következőkre nem vonatkozik:

- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A Microsoft ügyfél-szerződéshez tartozó szerződési metaadatokat a következő lehetőségekkel kell lekérnie:

- [A Microsoft ügyfél-szerződés elfogadásának megerősítése](./confirm-customer-consent-customer-agreement.md)
- [Letöltési hivatkozás beolvasása a Microsoft ügyfél-szerződési sablonhoz](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Előfeltételek

- Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.

- A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az alkalmazások és a felhasználók hitelesítését támogatja.

## <a name="net-version-114-or-newer"></a>.NET (1,14-es vagy újabb verzió)

A Microsoft ügyfél-szerződéshez tartozó szerződés metaadatainak beolvasása:

1. Először kérje le a **IAggregatePartner. AgreementDetails** gyűjteményt.

2. Hívja meg a **ByAgreementType** metódust a gyűjtemény Microsoft-ügyféli szerződésre való szűréséhez.

3. Végül hívja a **Get** vagy a **GetAsync** metódust.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Teljes minta a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.

## <a name="rest-request"></a>REST-kérelem

A Microsoft ügyfél-szerződéshez tartozó szerződés metaadatainak beolvasása:

1. Hozzon létre egy REST-kérést a [AgreementMetaData](./agreement-metadata-resources.md) -gyűjtemény lekéréséhez.

2. A **agreementType** lekérdezési paraméterrel az eredményeket csak a Microsoft ügyfél-szerződésre szűkítheti.

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Agreements? agreementType = {egyezmény-típus} http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

| Név                   | Típus     | Kötelező | Leírás                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| szerződés típusa | sztring | No | Ezzel a paraméterrel a lekérdezési választ adott szerződési típusra szűkítheti. A támogatott értékek a következők: <br/><br/>**MicrosoftCloudAgreement** , amely csak a *MicrosoftCloudAgreement* típusú szerződési metaadatokat tartalmazza<br/><br/>**MicrosoftCustomerAgreement** , amely csak a *MicrosoftCustomerAgreement* típusú megállapodási metaadatokat tartalmazza.<br/><br/>**\*** Ez az összes szerződési metaadatot visszaadja. (Ne használja **\*** , kivéve, ha a kód a szükséges futtatókörnyezeti logikával rendelkezik a nem ismert megállapodások típusainak kezeléséhez, mivel a Microsoft bármikor bevezetheti a szerződési metaadatokat az új szerződési típusokkal.)<br/><br/> **Megjegyzés:** Ha nincs megadva az URI paraméter, a lekérdezés alapértelmezés szerint **MicrosoftCloudAgreement** a visszafelé kompatibilitás érdekében.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus [ **AgreementMetaData** -erőforrások](./agreement-metadata-resources.md) gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.

A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
