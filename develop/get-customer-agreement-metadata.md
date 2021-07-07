---
title: A Microsoft Ügyfélszerződés szerződési metaadatainak lekérése
description: Ez a cikk a szerződés metaadatainak lekért Microsoft Ügyfélszerződés.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 5c20b317edf16b159050884070683880cf7e45bb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025718"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>A Microsoft Ügyfélszerződés szerződési metaadatainak lekérése

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A microsoftos Microsoft Ügyfélszerződés metaadatait jelenleg csak a Microsoft Partnerközpont támogatja.

A szerződés metaadatait a következő Microsoft Ügyfélszerződés kell lekérnie:

- [Annak megerősítése, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződés](./confirm-customer-consent-customer-agreement.md)
- [Letöltési hivatkozás lekérése a Microsoft Ügyfélszerződés sablonhoz](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Előfeltételek

- Ha az Partnerközpont .NET SDK-t használja, 1.14-es vagy újabb verzió szükséges.

- Hitelesítő adatok a Partnerközpont [leírtak szerint.](./partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítést támogatja.

## <a name="net-version-114-or-newer"></a>.NET (1.14-es vagy újabb verzió)

A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés:

1. Először is olvassa be az **IAggregatePartner.AgreementDetails gyűjteményt.**

2. Hívja **meg a ByAgreementType metódust** a gyűjtemény szűréséhez a Microsoft Ügyfélszerződés.

3. Végül hívja meg a **Get** vagy **a GetAsync metódust.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

A teljes minta megtalálható a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban a konzol [tesztalkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektjében.

## <a name="rest-request"></a>REST-kérés

A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés:

1. Hozzon létre egy REST-kérést az [AgreementMetaData gyűjtemény lekéréséhez.](./agreement-metadata-resources.md)

2. Az **agreementType lekérdezési** paraméterrel az eredményt csak a lekérdezési Microsoft Ügyfélszerződés.

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus | Kérés URI-ja                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

| Név                   | Típus     | Kötelező | Leírás                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| szerződéstípus | sztring | No | Ezzel a paraméterrel adott szerződéstípusra lehet hatókört használni a lekérdezési válaszra. A támogatott értékek a következőek: <br/><br/>**MicrosoftCloudAgreement,** amely csak *MicrosoftCloudAgreement* típusú szerződési metaadatokat tartalmaz<br/><br/>**MicrosoftCustomerAgreement,** amely csak *MicrosoftCustomerAgreement* típusú szerződési metaadatokat tartalmaz.<br/><br/>**\**_ az összes szerződési metaadatot visszaadja. (Ne használja a _* \* _ hacsak a kód nem rendelkezik a szükséges futásidejű logikával az ismeretlen szerződéstípusok kezeléshez, mert a Microsoft bármikor bevezethet szerződésmetaadatokat új *szerződéstípusokkal.) <br/> <br/> _* Megjegyzés:** Ha az URI paraméter nincs megadva, a lekérdezés alapértelmezés szerint **a MicrosoftCloudAgreement** értéket használja a visszamenőleges kompatibilitás érdekében.  |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Ha a művelet sikeres, ez a metódus [ **agreementMetaData-erőforrások**](./agreement-metadata-resources.md) gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.

Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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
