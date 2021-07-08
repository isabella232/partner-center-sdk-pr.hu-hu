---
title: Microsoft Cloud szerződés szerződési metaadatainak lekérése
description: Ez a cikk a szerződés metaadatainak lekért Microsoft Cloud szerződés.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 2588327e72a13de75eb9e02675edbd535491adc4
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760793"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a><span data-ttu-id="3ace6-103">Microsoft Cloud szerződés szerződési metaadatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="3ace6-103">Get agreement metadata for Microsoft Cloud Agreement</span></span>

<span data-ttu-id="3ace6-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3ace6-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="3ace6-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3ace6-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3ace6-106">Az **AgreementMetaData** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="3ace6-106">The **AgreementMetaData** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ace6-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3ace6-107">Prerequisites</span></span>

- <span data-ttu-id="3ace6-108">Ha az Partnerközpont .NET SDK-t használja, 1.9-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="3ace6-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="3ace6-109">Ha az Partnerközpont Java SDK-t használja, 1.8-as vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="3ace6-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="3ace6-110">Hitelesítő adatok a Partnerközpont [leírtak szerint.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3ace6-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="3ace6-111">Ez a forgatókönyv támogatja az alkalmazás- és felhasználóhitelesítést.</span><span class="sxs-lookup"><span data-stu-id="3ace6-111">This scenario supports app + user authentication.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="3ace6-112">.NET (1.14-es vagy újabb verzió)</span><span class="sxs-lookup"><span data-stu-id="3ace6-112">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="3ace6-113">A szerződés metaadatainak lekérése Microsoft Cloud szerződés:</span><span class="sxs-lookup"><span data-stu-id="3ace6-113">To retrieve the agreement metadata for Microsoft Cloud Agreement:</span></span>

1. <span data-ttu-id="3ace6-114">Először is olvassa be az **IAggregatePartner.AgreementDetails gyűjteményt.**</span><span class="sxs-lookup"><span data-stu-id="3ace6-114">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="3ace6-115">Hívja **meg a ByAgreementType metódust** a gyűjtemény szűréséhez a Microsoft Cloud szerződés.</span><span class="sxs-lookup"><span data-stu-id="3ace6-115">Call **ByAgreementType** method to filter the collection to Microsoft Cloud Agreement.</span></span>

3. <span data-ttu-id="3ace6-116">Végül hívja meg a **Get** vagy **a GetAsync metódust.**</span><span class="sxs-lookup"><span data-stu-id="3ace6-116">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="3ace6-117">A teljes minta megtalálható a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban a konzol [tesztalkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektjében.</span><span class="sxs-lookup"><span data-stu-id="3ace6-117">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="3ace6-118">.NET (1.9-es és 1.13-as verzió)</span><span class="sxs-lookup"><span data-stu-id="3ace6-118">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="3ace6-119">A szerződés metaadatainak lekérése a Microsoft Cloud szerződés:</span><span class="sxs-lookup"><span data-stu-id="3ace6-119">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="3ace6-120">Először olvassa be az **IAggregatePartner.AgreementDetails** gyűjteményt, majd hívja meg a **Get** vagy **GetAsync metódusokat.**</span><span class="sxs-lookup"><span data-stu-id="3ace6-120">First retrieve the **IAggregatePartner.AgreementDetails** collection and then call the **Get** or **GetAsync** methods.</span></span> <span data-ttu-id="3ace6-121">Ezután keresse meg az elemet a gyűjteményben, amely megfelel a Microsoft Cloud szerződés:</span><span class="sxs-lookup"><span data-stu-id="3ace6-121">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a><span data-ttu-id="3ace6-122">Java</span><span class="sxs-lookup"><span data-stu-id="3ace6-122">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="3ace6-123">A szerződés metaadatainak lekérése a Microsoft Cloud szerződés:</span><span class="sxs-lookup"><span data-stu-id="3ace6-123">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="3ace6-124">Először hívja meg az **IAggregatePartner.getAgreementDetails** függvényt, majd a **get függvényt.**</span><span class="sxs-lookup"><span data-stu-id="3ace6-124">First call the **IAggregatePartner.getAgreementDetails** function and then call the **get** function.</span></span> <span data-ttu-id="3ace6-125">Ezután keresse meg az elemet a gyűjteményben, amely megfelel a Microsoft Cloud szerződés:</span><span class="sxs-lookup"><span data-stu-id="3ace6-125">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

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

<span data-ttu-id="3ace6-126">A teljes minta megtalálható a [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) osztályban a konzol [tesztalkalmazás](https://github.com/Microsoft/Partner-Center-Java-Samples) projektjében.</span><span class="sxs-lookup"><span data-stu-id="3ace6-126">A complete sample can be found in the [GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="3ace6-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ace6-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="3ace6-128">A szerződés metaadatainak lekérése a Microsoft Cloud szerződés:</span><span class="sxs-lookup"><span data-stu-id="3ace6-128">To retrieve agreement metadata for the Microsoft Cloud Agreement:</span></span>

<span data-ttu-id="3ace6-129">Használja a [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) parancsot.</span><span class="sxs-lookup"><span data-stu-id="3ace6-129">Use the [**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) command.</span></span> <span data-ttu-id="3ace6-130">Ezután keresse meg az elemet a gyűjteményben, amely megfelel a Microsoft Cloud szerződés:</span><span class="sxs-lookup"><span data-stu-id="3ace6-130">Then search for the item within the collection, which corresponds to the Microsoft Cloud Agreement:</span></span>

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a><span data-ttu-id="3ace6-131">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="3ace6-131">REST request</span></span>

<span data-ttu-id="3ace6-132">A szerződés metaadatainak lekéréséhez Microsoft Cloud szerződés hozzon létre egy REST-kérést az **AgreementMetaData gyűjtemény lekéréséhez.**</span><span class="sxs-lookup"><span data-stu-id="3ace6-132">To retrieve agreement metadata for Microsoft Cloud Agreement, first create a REST Request to retrieve the **AgreementMetaData** collection.</span></span> <span data-ttu-id="3ace6-133">Ezután keresse meg a gyűjteményben azt az elemet, amely megfelel a Microsoft Cloud szerződés.</span><span class="sxs-lookup"><span data-stu-id="3ace6-133">Then search for the item in the collection that corresponds to the Microsoft Cloud Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3ace6-134">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3ace6-134">Request syntax</span></span>

| <span data-ttu-id="3ace6-135">Metódus</span><span class="sxs-lookup"><span data-stu-id="3ace6-135">Method</span></span> | <span data-ttu-id="3ace6-136">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3ace6-136">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="3ace6-137">GET</span><span class="sxs-lookup"><span data-stu-id="3ace6-137">GET</span></span>    | <span data-ttu-id="3ace6-138">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3ace6-138">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3ace6-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3ace6-139">Request headers</span></span>

<span data-ttu-id="3ace6-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3ace6-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3ace6-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3ace6-141">Request body</span></span>

<span data-ttu-id="3ace6-142">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="3ace6-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3ace6-143">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3ace6-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="3ace6-144">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3ace6-144">REST response</span></span>

<span data-ttu-id="3ace6-145">Ha a művelet sikeres, ez a metódus **agreementMetaData-erőforrások** gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="3ace6-145">If successful, this method returns a collection of **AgreementMetaData** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3ace6-146">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3ace6-146">Response success and error codes</span></span>

<span data-ttu-id="3ace6-147">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="3ace6-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3ace6-148">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="3ace6-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3ace6-149">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3ace6-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3ace6-150">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="3ace6-150">Response example</span></span>

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

<span data-ttu-id="3ace6-151">Az erőforrás azonosításához a válaszban, amely megfelel a Microsoft Cloud szerződés, keresse meg azt az erőforrást, amelynek **agreementType** tulajdonsága a "MicrosoftCloudAgreement" értéket használja.</span><span class="sxs-lookup"><span data-stu-id="3ace6-151">To identify the resource in the response that corresponds to the Microsoft Cloud Agreement, look for the resource whose **agreementType** property has value "MicrosoftCloudAgreement".</span></span>
