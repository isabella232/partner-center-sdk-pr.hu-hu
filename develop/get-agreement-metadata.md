---
title: Microsoft Cloud szerződés szerződési metaadatainak lekérése
description: Ez a cikk azt ismerteti, hogyan lehet beolvasni Microsoft Cloud szerződés metaadatait.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6a404eb38c4c31d3e69bb598872b932d8985529
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768048"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Microsoft Cloud szerződés szerződési metaadatainak lekérése

**A következőkre vonatkozik**

- Partnerközpont

> [!NOTE]
> A **AgreementMetaData** -erőforrást jelenleg a Microsoft nyilvános felhőben a partner Center támogatja. Nem alkalmazható a következőre:
> - A 21Vianet által üzemeltetett partneri központ
> - A Microsoft Cloud Germany Partnerközpontja
> - A Microsoft Cloud for US Government Partnerközpontja

## <a name="prerequisites"></a>Előfeltételek

- Ha a partner Center .NET SDK-t használja, a 1,9-es vagy újabb verzió szükséges.

- Ha a partner Center Java SDK-t használja, a 1,8-es vagy újabb verzió szükséges.

- A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja az alkalmazások és a felhasználók hitelesítését.

## <a name="net-version-114-or-newer"></a>.NET (1,14-es vagy újabb verzió)

Microsoft Cloud szerződéshez tartozó szerződés metaadatainak beolvasása:

1. Először kérje le a **IAggregatePartner. AgreementDetails** gyűjteményt.

2. Hívja meg a **ByAgreementType** metódust a gyűjtemény Microsoft Cloud szerződésre való szűréséhez.

3. Végül hívja a **Get** vagy a **GetAsync** metódust.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Teljes minta a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.

## <a name="net-version-19---113"></a>.NET (1,9-1,13-es verzió)

A Microsoft Cloud szerződés metaadatainak beolvasása:

Először kérje le a **IAggregatePartner. AgreementDetails** gyűjteményt, majd hívja meg a **Get** vagy a **GetAsync** metódust. Ezután keresse meg a gyűjteményen belüli tételt, amely megfelel a Microsoft Cloud szerződésnek:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

A Microsoft Cloud szerződés metaadatainak beolvasása:

Először hívja meg a **IAggregatePartner. getAgreementDetails** függvényt, majd hívja meg a **Get** függvényt. Ezután keresse meg a gyűjteményen belüli tételt, amely megfelel a Microsoft Cloud szerződésnek:

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

Teljes minta a [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) osztályban található a [konzol tesztelése alkalmazás](https://github.com/Microsoft/Partner-Center-Java-Samples) projektben.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A Microsoft Cloud szerződés metaadatainak beolvasása:

Használja a [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) parancsot. Ezután keresse meg a gyűjteményen belüli tételt, amely megfelel a Microsoft Cloud szerződésnek:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>REST-kérelem

Microsoft Cloud szerződés metaadatainak lekéréséhez először hozzon létre egy REST-kérelmet a **AgreementMetaData** -gyűjtemény lekéréséhez. Ezután keresse meg a gyűjtemény azon elemét, amely megfelel a Microsoft Cloud szerződésnek.

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Agreements http/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus **AgreementMetaData** -erőforrások gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

A Microsoft Cloud Szerződésnek megfelelő válaszban található erőforrás azonosításához keresse meg azt az erőforrást, amelynek **agreementType** tulajdonságának értéke "MicrosoftCloudAgreement".
