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
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="25bca-103">Microsoft Cloud szerződés szerződési metaadatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="25bca-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="25bca-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="25bca-104">**Applies To**</span></span>

- <span data-ttu-id="25bca-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="25bca-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="25bca-106">A **AgreementMetaData** -erőforrást jelenleg a Microsoft nyilvános felhőben a partner Center támogatja.</span><span class="sxs-lookup"><span data-stu-id="25bca-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="25bca-107">Nem alkalmazható a következőre:</span><span class="sxs-lookup"><span data-stu-id="25bca-107">It isn't applicable to:</span></span>
> - <span data-ttu-id="25bca-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="25bca-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="25bca-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="25bca-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="25bca-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="25bca-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25bca-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="25bca-111">Prerequisites</span></span>

- <span data-ttu-id="25bca-112">Ha a partner Center .NET SDK-t használja, a 1,9-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="25bca-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="25bca-113">Ha a partner Center Java SDK-t használja, a 1,8-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="25bca-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="25bca-114">A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="25bca-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="25bca-115">Ez a forgatókönyv támogatja az alkalmazások és a felhasználók hitelesítését.</span><span class="sxs-lookup"><span data-stu-id="25bca-115">This scenario supports app + user authentication..</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="25bca-116">.NET (1,14-es vagy újabb verzió)</span><span class="sxs-lookup"><span data-stu-id="25bca-116">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="25bca-117">Microsoft Cloud szerződéshez tartozó szerződés metaadatainak beolvasása:</span><span class="sxs-lookup"><span data-stu-id="25bca-117">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="25bca-118">Először kérje le a **IAggregatePartner. AgreementDetails** gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="25bca-118">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="25bca-119">Hívja meg a **ByAgreementType** metódust a gyűjtemény Microsoft Cloud szerződésre való szűréséhez.</span><span class="sxs-lookup"><span data-stu-id="25bca-119">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="25bca-120">Végül hívja a **Get** vagy a **GetAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="25bca-120">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="25bca-121">Teljes minta a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="25bca-121">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="25bca-122">.NET (1,9-1,13-es verzió)</span><span class="sxs-lookup"><span data-stu-id="25bca-122">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="25bca-123">A Microsoft Cloud szerződés metaadatainak beolvasása:</span><span class="sxs-lookup"><span data-stu-id="25bca-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="25bca-124">Először kérje le a **IAggregatePartner. AgreementDetails** gyűjteményt, majd hívja meg a **Get** vagy a **GetAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="25bca-124">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="25bca-125">Ezután keresse meg a gyűjteményen belüli tételt, amely megfelel a Microsoft Cloud szerződésnek:</span><span class="sxs-lookup"><span data-stu-id="25bca-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="25bca-126">Java</span><span class="sxs-lookup"><span data-stu-id="25bca-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="25bca-127">A Microsoft Cloud szerződés metaadatainak beolvasása:</span><span class="sxs-lookup"><span data-stu-id="25bca-127">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="25bca-128">Először hívja meg a **IAggregatePartner. getAgreementDetails** függvényt, majd hívja meg a **Get** függvényt.</span><span class="sxs-lookup"><span data-stu-id="25bca-128">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="25bca-129">Ezután keresse meg a gyűjteményen belüli tételt, amely megfelel a Microsoft Cloud szerződésnek:</span><span class="sxs-lookup"><span data-stu-id="25bca-129">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

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

<span data-ttu-id="25bca-130">Teljes minta a [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) osztályban található a [konzol tesztelése alkalmazás](https://github.com/Microsoft/Partner-Center-Java-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="25bca-130">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="25bca-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25bca-131">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="25bca-132">A Microsoft Cloud szerződés metaadatainak beolvasása:</span><span class="sxs-lookup"><span data-stu-id="25bca-132">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="25bca-133">Használja a [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) parancsot.</span><span class="sxs-lookup"><span data-stu-id="25bca-133">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="25bca-134">Ezután keresse meg a gyűjteményen belüli tételt, amely megfelel a Microsoft Cloud szerződésnek:</span><span class="sxs-lookup"><span data-stu-id="25bca-134">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="25bca-135">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="25bca-135">REST request</span></span>

<span data-ttu-id="25bca-136">Microsoft Cloud szerződés metaadatainak lekéréséhez először hozzon létre egy REST-kérelmet a **AgreementMetaData** -gyűjtemény lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="25bca-136">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="25bca-137">Ezután keresse meg a gyűjtemény azon elemét, amely megfelel a Microsoft Cloud szerződésnek.</span><span class="sxs-lookup"><span data-stu-id="25bca-137">Then search for the item in the collection which corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25bca-138">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="25bca-138">Request syntax</span></span>

| <span data-ttu-id="25bca-139">Metódus</span><span class="sxs-lookup"><span data-stu-id="25bca-139">Method</span></span> | <span data-ttu-id="25bca-140">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="25bca-140">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="25bca-141">GET</span><span class="sxs-lookup"><span data-stu-id="25bca-141">GET</span></span>    | <span data-ttu-id="25bca-142">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="25bca-142">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="25bca-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="25bca-143">Request headers</span></span>

<span data-ttu-id="25bca-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="25bca-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="25bca-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="25bca-145">Request body</span></span>

<span data-ttu-id="25bca-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="25bca-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="25bca-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="25bca-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="25bca-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="25bca-148">REST response</span></span>

<span data-ttu-id="25bca-149">Ha ez sikeres, ez a metódus **AgreementMetaData** -erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="25bca-149">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25bca-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="25bca-150">Response success and error codes</span></span>

<span data-ttu-id="25bca-151">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="25bca-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="25bca-152">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="25bca-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="25bca-153">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="25bca-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="25bca-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="25bca-154">Response example</span></span>

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

<span data-ttu-id="25bca-155">A Microsoft Cloud Szerződésnek megfelelő válaszban található erőforrás azonosításához keresse meg azt az erőforrást, amelynek **agreementType** tulajdonságának értéke "MicrosoftCloudAgreement".</span><span class="sxs-lookup"><span data-stu-id="25bca-155">To identify the resource in the response which corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
