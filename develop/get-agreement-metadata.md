---
title: Microsoft Cloud szerződés szerződési metaadatainak lekérése
description: Ez a cikk a szerződés metaadatainak lekért Microsoft Cloud szerződés.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 55a09752844f74caaf878f1e2dcfe3d8a70a283c5e0e9daefba89c558405690a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994115"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Microsoft Cloud szerződés szerződési metaadatainak lekérése

**A következőkre vonatkozik:** Partnerközpont

**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Az **AgreementMetaData** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.

## <a name="prerequisites"></a>Előfeltételek

- Ha az Partnerközpont .NET SDK-t használja, 1.9-es vagy újabb verzió szükséges.

- Ha az Partnerközpont Java SDK-t használja, 1.8-as vagy újabb verzió szükséges.

- A hitelesítéssel Partnerközpont [hitelesítő adatok.](./partner-center-authentication.md) Ez a forgatókönyv támogatja az alkalmazás- és felhasználóhitelesítést.

## <a name="net-version-114-or-newer"></a>.NET (1.14-es vagy újabb verzió)

A szerződés metaadatainak lekérése Microsoft Cloud szerződés:

1. Először is olvassa be az **IAggregatePartner.AgreementDetails gyűjteményt.**

2. Hívja **meg a ByAgreementType metódust** a gyűjtemény szűréséhez a Microsoft Cloud szerződés.

3. Végül hívja meg a **Get** vagy **a GetAsync metódust.**

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

A teljes minta megtalálható a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban a konzol tesztalkalmazás [projektjében.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)

## <a name="net-version-19---113"></a>.NET (1.9-es és 1.13-as verzió)

A szerződés metaadatainak lekérése a Microsoft Cloud szerződés:

Először olvassa be az **IAggregatePartner.AgreementDetails** gyűjteményt, majd hívja meg a **Get** vagy **GetAsync metódusokat.** Ezután keresse meg az elemet a gyűjteményben, amely megfelel a Microsoft Cloud szerződés:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

A szerződés metaadatainak lekérése a Microsoft Cloud szerződés:

Először hívja meg az **IAggregatePartner.getAgreementDetails** függvényt, majd hívja meg a **get** függvényt. Ezután keresse meg az elemet a gyűjteményben, amely megfelel a Microsoft Cloud szerződés:

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

A teljes minta megtalálható a [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) osztályban a konzol tesztalkalmazás [projektjében.](https://github.com/Microsoft/Partner-Center-Java-Samples)

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

A szerződés metaadatainak lekérése a Microsoft Cloud szerződés:

Használja a [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) parancsot. Ezután keresse meg az elemet a gyűjteményben, amely megfelel a Microsoft Cloud szerződés:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>REST-kérés

A szerződés metaadatainak lekéréséhez Microsoft Cloud szerződés hozzon létre egy REST-kérést az **AgreementMetaData gyűjtemény lekéréséhez.** Ezután keresse meg a gyűjteményben azt az elemet, amely megfelel a Microsoft Cloud szerződés.

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus | Kérés URI-ja                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

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

Sikeres művelet esetén ez a metódus **agreementMetaData-erőforrások** gyűjteményét adja vissza a válasz törzsében.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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

Az erőforrás azonosításához a válaszban, amely megfelel a Microsoft Cloud szerződés, keresse meg azt az erőforrást, amelynek **agreementType** tulajdonsága a "MicrosoftCloudAgreement" értéket használja.
