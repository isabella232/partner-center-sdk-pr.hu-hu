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
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="8e3e3-103">A Microsoft Ügyfélszerződés szerződési metaadatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="8e3e3-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="8e3e3-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="8e3e3-104">**Applies to:**</span></span>

- <span data-ttu-id="8e3e3-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8e3e3-105">Partner Center</span></span>

<span data-ttu-id="8e3e3-106">A partner Center jelenleg csak a *Microsoft nyilvános felhőben* támogatja a Microsoft ügyfél-szerződési metaadatokat.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="8e3e3-107">A következőkre nem vonatkozik:</span><span class="sxs-lookup"><span data-stu-id="8e3e3-107">It doesn't apply to:</span></span>

- <span data-ttu-id="8e3e3-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="8e3e3-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8e3e3-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8e3e3-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8e3e3-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8e3e3-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8e3e3-111">A Microsoft ügyfél-szerződéshez tartozó szerződési metaadatokat a következő lehetőségekkel kell lekérnie:</span><span class="sxs-lookup"><span data-stu-id="8e3e3-111">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="8e3e3-112">A Microsoft ügyfél-szerződés elfogadásának megerősítése</span><span class="sxs-lookup"><span data-stu-id="8e3e3-112">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="8e3e3-113">Letöltési hivatkozás beolvasása a Microsoft ügyfél-szerződési sablonhoz</span><span class="sxs-lookup"><span data-stu-id="8e3e3-113">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="8e3e3-114">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8e3e3-114">Prerequisites</span></span>

- <span data-ttu-id="8e3e3-115">Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-115">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="8e3e3-116">A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-116">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="8e3e3-117">Ez a forgatókönyv csak az alkalmazások és a felhasználók hitelesítését támogatja.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-117">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="8e3e3-118">.NET (1,14-es vagy újabb verzió)</span><span class="sxs-lookup"><span data-stu-id="8e3e3-118">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="8e3e3-119">A Microsoft ügyfél-szerződéshez tartozó szerződés metaadatainak beolvasása:</span><span class="sxs-lookup"><span data-stu-id="8e3e3-119">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="8e3e3-120">Először kérje le a **IAggregatePartner. AgreementDetails** gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-120">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="8e3e3-121">Hívja meg a **ByAgreementType** metódust a gyűjtemény Microsoft-ügyféli szerződésre való szűréséhez.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-121">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="8e3e3-122">Végül hívja a **Get** vagy a **GetAsync** metódust.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-122">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="8e3e3-123">Teljes minta a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-123">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8e3e3-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="8e3e3-124">REST request</span></span>

<span data-ttu-id="8e3e3-125">A Microsoft ügyfél-szerződéshez tartozó szerződés metaadatainak beolvasása:</span><span class="sxs-lookup"><span data-stu-id="8e3e3-125">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="8e3e3-126">Hozzon létre egy REST-kérést a [AgreementMetaData](./agreement-metadata-resources.md) -gyűjtemény lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-126">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="8e3e3-127">A **agreementType** lekérdezési paraméterrel az eredményeket csak a Microsoft ügyfél-szerződésre szűkítheti.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-127">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8e3e3-128">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8e3e3-128">Request syntax</span></span>

| <span data-ttu-id="8e3e3-129">Metódus</span><span class="sxs-lookup"><span data-stu-id="8e3e3-129">Method</span></span> | <span data-ttu-id="8e3e3-130">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8e3e3-130">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="8e3e3-131">GET</span><span class="sxs-lookup"><span data-stu-id="8e3e3-131">GET</span></span>    | <span data-ttu-id="8e3e3-132">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Agreements? agreementType = {egyezmény-típus} http/1.1</span><span class="sxs-lookup"><span data-stu-id="8e3e3-132">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="8e3e3-133">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="8e3e3-133">URI parameters</span></span>

| <span data-ttu-id="8e3e3-134">Név</span><span class="sxs-lookup"><span data-stu-id="8e3e3-134">Name</span></span>                   | <span data-ttu-id="8e3e3-135">Típus</span><span class="sxs-lookup"><span data-stu-id="8e3e3-135">Type</span></span>     | <span data-ttu-id="8e3e3-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8e3e3-136">Required</span></span> | <span data-ttu-id="8e3e3-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="8e3e3-137">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="8e3e3-138">szerződés típusa</span><span class="sxs-lookup"><span data-stu-id="8e3e3-138">agreement-type</span></span> | <span data-ttu-id="8e3e3-139">sztring</span><span class="sxs-lookup"><span data-stu-id="8e3e3-139">string</span></span> | <span data-ttu-id="8e3e3-140">No</span><span class="sxs-lookup"><span data-stu-id="8e3e3-140">No</span></span> | <span data-ttu-id="8e3e3-141">Ezzel a paraméterrel a lekérdezési választ adott szerződési típusra szűkítheti.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-141">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="8e3e3-142">A támogatott értékek a következők:</span><span class="sxs-lookup"><span data-stu-id="8e3e3-142">The supported values are:</span></span> <br/><br/><span data-ttu-id="8e3e3-143">**MicrosoftCloudAgreement** , amely csak a *MicrosoftCloudAgreement* típusú szerződési metaadatokat tartalmazza</span><span class="sxs-lookup"><span data-stu-id="8e3e3-143">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="8e3e3-144">**MicrosoftCustomerAgreement** , amely csak a *MicrosoftCustomerAgreement* típusú megállapodási metaadatokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-144">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="8e3e3-145">**\*** Ez az összes szerződési metaadatot visszaadja.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-145">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="8e3e3-146">(Ne használja **\*** , kivéve, ha a kód a szükséges futtatókörnyezeti logikával rendelkezik a nem ismert megállapodások típusainak kezeléséhez, mivel a Microsoft bármikor bevezetheti a szerződési metaadatokat az új szerződési típusokkal.)</span><span class="sxs-lookup"><span data-stu-id="8e3e3-146">(Don't use **\*** unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)</span></span><br/><br/> <span data-ttu-id="8e3e3-147">**Megjegyzés:** Ha nincs megadva az URI paraméter, a lekérdezés alapértelmezés szerint **MicrosoftCloudAgreement** a visszafelé kompatibilitás érdekében.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-147">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="8e3e3-148">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8e3e3-148">Request headers</span></span>

<span data-ttu-id="8e3e3-149">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8e3e3-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8e3e3-150">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8e3e3-150">Request body</span></span>

<span data-ttu-id="8e3e3-151">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-151">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8e3e3-152">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8e3e3-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="8e3e3-153">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8e3e3-153">REST response</span></span>

<span data-ttu-id="8e3e3-154">Ha ez sikeres, ez a metódus [ **AgreementMetaData** -erőforrások](./agreement-metadata-resources.md) gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-154">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8e3e3-155">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8e3e3-155">Response success and error codes</span></span>

<span data-ttu-id="8e3e3-156">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="8e3e3-157">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8e3e3-158">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="8e3e3-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8e3e3-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8e3e3-159">Response example</span></span>

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
