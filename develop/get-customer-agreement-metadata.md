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
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a><span data-ttu-id="e0298-103">A Microsoft Ügyfélszerződés szerződési metaadatainak lekérése</span><span class="sxs-lookup"><span data-stu-id="e0298-103">Get agreement metadata for the Microsoft Customer Agreement</span></span>

<span data-ttu-id="e0298-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e0298-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="e0298-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e0298-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e0298-106">A microsoftos Microsoft Ügyfélszerződés metaadatait jelenleg csak a Microsoft Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="e0298-106">Agreement metadata for Microsoft Customer Agreement is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="e0298-107">A szerződés metaadatait a következő Microsoft Ügyfélszerződés kell lekérnie:</span><span class="sxs-lookup"><span data-stu-id="e0298-107">You must retrieve the agreement metadata for the Microsoft Customer Agreement before you can:</span></span>

- [<span data-ttu-id="e0298-108">Annak megerősítése, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződés</span><span class="sxs-lookup"><span data-stu-id="e0298-108">Confirm a customer's acceptance of the Microsoft Customer Agreement</span></span>](./confirm-customer-consent-customer-agreement.md)
- [<span data-ttu-id="e0298-109">Letöltési hivatkozás lekérése a Microsoft Ügyfélszerződés sablonhoz</span><span class="sxs-lookup"><span data-stu-id="e0298-109">Retrieve a download link for the Microsoft Customer Agreement template</span></span>](./download-customer-agreement-template.md)

## <a name="prerequisites"></a><span data-ttu-id="e0298-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e0298-110">Prerequisites</span></span>

- <span data-ttu-id="e0298-111">Ha az Partnerközpont .NET SDK-t használja, 1.14-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="e0298-111">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="e0298-112">Hitelesítő adatok a Partnerközpont [leírtak szerint.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e0298-112">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="e0298-113">Ez a forgatókönyv csak az App+User hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="e0298-113">This scenario supports App+User authentication only.</span></span>

## <a name="net-version-114-or-newer"></a><span data-ttu-id="e0298-114">.NET (1.14-es vagy újabb verzió)</span><span class="sxs-lookup"><span data-stu-id="e0298-114">.NET (version 1.14 or newer)</span></span>

<span data-ttu-id="e0298-115">A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés:</span><span class="sxs-lookup"><span data-stu-id="e0298-115">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="e0298-116">Először is olvassa be az **IAggregatePartner.AgreementDetails gyűjteményt.**</span><span class="sxs-lookup"><span data-stu-id="e0298-116">First, retrieve the **IAggregatePartner.AgreementDetails** collection.</span></span>

2. <span data-ttu-id="e0298-117">Hívja **meg a ByAgreementType metódust** a gyűjtemény szűréséhez a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="e0298-117">Call **ByAgreementType** method to filter the collection to Microsoft Customer Agreement.</span></span>

3. <span data-ttu-id="e0298-118">Végül hívja meg a **Get** vagy **a GetAsync metódust.**</span><span class="sxs-lookup"><span data-stu-id="e0298-118">Finally, call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

<span data-ttu-id="e0298-119">A teljes minta megtalálható a [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) osztályban a konzol [tesztalkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektjében.</span><span class="sxs-lookup"><span data-stu-id="e0298-119">A complete sample can be found in the [GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e0298-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="e0298-120">REST request</span></span>

<span data-ttu-id="e0298-121">A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés:</span><span class="sxs-lookup"><span data-stu-id="e0298-121">To retrieve the agreement metadata for Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="e0298-122">Hozzon létre egy REST-kérést az [AgreementMetaData gyűjtemény lekéréséhez.](./agreement-metadata-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e0298-122">Create a REST request to retrieve the [AgreementMetaData](./agreement-metadata-resources.md) collection.</span></span>

2. <span data-ttu-id="e0298-123">Az **agreementType lekérdezési** paraméterrel az eredményt csak a lekérdezési Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="e0298-123">Use the **agreementType** query parameter to scope the result to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e0298-124">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e0298-124">Request syntax</span></span>

| <span data-ttu-id="e0298-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="e0298-125">Method</span></span> | <span data-ttu-id="e0298-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e0298-126">Request URI</span></span>                                                         |
|--------|---------------------------------------------------------------------|
| <span data-ttu-id="e0298-127">GET</span><span class="sxs-lookup"><span data-stu-id="e0298-127">GET</span></span>    | <span data-ttu-id="e0298-128">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e0298-128">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="e0298-129">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="e0298-129">URI parameters</span></span>

| <span data-ttu-id="e0298-130">Név</span><span class="sxs-lookup"><span data-stu-id="e0298-130">Name</span></span>                   | <span data-ttu-id="e0298-131">Típus</span><span class="sxs-lookup"><span data-stu-id="e0298-131">Type</span></span>     | <span data-ttu-id="e0298-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e0298-132">Required</span></span> | <span data-ttu-id="e0298-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="e0298-133">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="e0298-134">szerződéstípus</span><span class="sxs-lookup"><span data-stu-id="e0298-134">agreement-type</span></span> | <span data-ttu-id="e0298-135">sztring</span><span class="sxs-lookup"><span data-stu-id="e0298-135">string</span></span> | <span data-ttu-id="e0298-136">No</span><span class="sxs-lookup"><span data-stu-id="e0298-136">No</span></span> | <span data-ttu-id="e0298-137">Ezzel a paraméterrel adott szerződéstípusra lehet hatókört használni a lekérdezési válaszra.</span><span class="sxs-lookup"><span data-stu-id="e0298-137">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="e0298-138">A támogatott értékek a következőek:</span><span class="sxs-lookup"><span data-stu-id="e0298-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="e0298-139">**MicrosoftCloudAgreement,** amely csak *MicrosoftCloudAgreement* típusú szerződési metaadatokat tartalmaz</span><span class="sxs-lookup"><span data-stu-id="e0298-139">**MicrosoftCloudAgreement** that includes agreement metadata only of the type *MicrosoftCloudAgreement*</span></span><br/><br/><span data-ttu-id="e0298-140">**MicrosoftCustomerAgreement,** amely csak *MicrosoftCustomerAgreement* típusú szerződési metaadatokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="e0298-140">**MicrosoftCustomerAgreement** that includes agreement metadata only of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/><span data-ttu-id="e0298-141">**\**_ az összes szerződési metaadatot visszaadja. (Ne használja a _\* \* _ hacsak a kód nem rendelkezik a szükséges futásidejű logikával az ismeretlen szerződéstípusok kezeléshez, mert a Microsoft bármikor bevezethet szerződésmetaadatokat új *szerződéstípusokkal.) <br/> <br/> _* Megjegyzés:*\* Ha az URI paraméter nincs megadva, a lekérdezés alapértelmezés szerint **a MicrosoftCloudAgreement** értéket használja a visszamenőleges kompatibilitás érdekében.</span><span class="sxs-lookup"><span data-stu-id="e0298-141">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary runtime logic to handle unfamiliar agreement types because Microsoft may introduce agreement metadata with new agreement types at any time.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="e0298-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e0298-142">Request headers</span></span>

<span data-ttu-id="e0298-143">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e0298-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e0298-144">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="e0298-144">Request body</span></span>

<span data-ttu-id="e0298-145">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="e0298-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e0298-146">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="e0298-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="e0298-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e0298-147">REST response</span></span>

<span data-ttu-id="e0298-148">Ha a művelet sikeres, ez a metódus [ **agreementMetaData-erőforrások**](./agreement-metadata-resources.md) gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="e0298-148">If successful, this method returns a collection of [**AgreementMetaData** resources](./agreement-metadata-resources.md) in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e0298-149">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e0298-149">Response success and error codes</span></span>

<span data-ttu-id="e0298-150">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="e0298-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="e0298-151">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="e0298-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e0298-152">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e0298-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e0298-153">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="e0298-153">Response example</span></span>

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
