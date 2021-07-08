---
title: A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősítést kapni az ügyfelek általi Microsoft Ügyfélszerződés.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3668a5e510effb533cade311f52513b9a81d40af
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760538"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="f455d-103">A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése</span><span class="sxs-lookup"><span data-stu-id="f455d-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="f455d-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f455d-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="f455d-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f455d-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f455d-106">A **Szerződés** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="f455d-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="f455d-107">Ez a cikk bemutatja, hogyan kérhető(k) le a jóváhagyás(ak) arról, hogy az ügyfél elfogadta-e Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="f455d-107">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f455d-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f455d-108">Prerequisites</span></span>

- <span data-ttu-id="f455d-109">Ha az Partnerközpont .NET SDK-t használja, 1.14-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="f455d-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="f455d-110">Hitelesítő adatok a Partnerközpont [leírtak szerint.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f455d-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="f455d-111">Ez a forgatókönyv csak az App+User hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="f455d-111">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="f455d-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f455d-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f455d-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="f455d-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f455d-114">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f455d-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f455d-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="f455d-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f455d-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="f455d-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f455d-117">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f455d-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="f455d-118">.NET</span><span class="sxs-lookup"><span data-stu-id="f455d-118">.NET</span></span>

<span data-ttu-id="f455d-119">A korábban megadott ügyfél-elfogadás megerősítésének(i) lekérése:</span><span class="sxs-lookup"><span data-stu-id="f455d-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="f455d-120">Használja az **IAggregatePartner.Customers gyűjteményt,** és hívja meg a **ById** metódust a megadott ügyfélazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="f455d-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="f455d-121">A **ByAgreementType** metódus hívásával lekérheti a **Agreements** Microsoft Ügyfélszerződés és szűrheti az eredményeket.</span><span class="sxs-lookup"><span data-stu-id="f455d-121">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="f455d-122">Hívja meg **a Get** vagy **a GetAsync metódust.**</span><span class="sxs-lookup"><span data-stu-id="f455d-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="f455d-123">A teljes minta megtalálható a [GetCustomerAgreements osztályban](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) a konzol tesztalkalmazás [projektjében.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="f455d-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="f455d-124">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="f455d-124">REST request</span></span>

<span data-ttu-id="f455d-125">A korábban megadott ügyfél-elfogadás megerősítésének lekérése:</span><span class="sxs-lookup"><span data-stu-id="f455d-125">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="f455d-126">Hozzon létre egy REST-kérést az ügyfél [szerződésgyűjteményének](./agreement-resources.md) lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="f455d-126">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="f455d-127">Az **agreementType lekérdezési** paraméterrel az eredményeket csak a lekérdezési Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="f455d-127">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f455d-128">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f455d-128">Request syntax</span></span>

<span data-ttu-id="f455d-129">Használja a következő kérésszintaxist:</span><span class="sxs-lookup"><span data-stu-id="f455d-129">Use the following request syntax:</span></span>

| <span data-ttu-id="f455d-130">Metódus</span><span class="sxs-lookup"><span data-stu-id="f455d-130">Method</span></span> | <span data-ttu-id="f455d-131">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f455d-131">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f455d-132">GET</span><span class="sxs-lookup"><span data-stu-id="f455d-132">GET</span></span>    | <span data-ttu-id="f455d-133">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f455d-133">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="f455d-134">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="f455d-134">URI parameters</span></span>

<span data-ttu-id="f455d-135">A kérelemhez a következő URI-paramétereket használhatja:</span><span class="sxs-lookup"><span data-stu-id="f455d-135">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="f455d-136">Név</span><span class="sxs-lookup"><span data-stu-id="f455d-136">Name</span></span>             | <span data-ttu-id="f455d-137">Típus</span><span class="sxs-lookup"><span data-stu-id="f455d-137">Type</span></span> | <span data-ttu-id="f455d-138">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f455d-138">Required</span></span> | <span data-ttu-id="f455d-139">Leírás</span><span class="sxs-lookup"><span data-stu-id="f455d-139">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="f455d-140">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="f455d-140">customer-tenant-id</span></span> | <span data-ttu-id="f455d-141">GUID</span><span class="sxs-lookup"><span data-stu-id="f455d-141">GUID</span></span> | <span data-ttu-id="f455d-142">Igen</span><span class="sxs-lookup"><span data-stu-id="f455d-142">Yes</span></span> | <span data-ttu-id="f455d-143">Az érték egy **CustomerTenantId** formátumú GUID, amely lehetővé teszi egy ügyfél megadását.</span><span class="sxs-lookup"><span data-stu-id="f455d-143">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="f455d-144">szerződéstípus</span><span class="sxs-lookup"><span data-stu-id="f455d-144">agreement-type</span></span> | <span data-ttu-id="f455d-145">sztring</span><span class="sxs-lookup"><span data-stu-id="f455d-145">string</span></span> | <span data-ttu-id="f455d-146">No</span><span class="sxs-lookup"><span data-stu-id="f455d-146">No</span></span> | <span data-ttu-id="f455d-147">Ez a paraméter az összes szerződési metaadatot visszaadja.</span><span class="sxs-lookup"><span data-stu-id="f455d-147">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="f455d-148">Ezzel a paraméterrel adott szerződéstípusra lehet hatókört használni a lekérdezési válaszra.</span><span class="sxs-lookup"><span data-stu-id="f455d-148">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="f455d-149">A támogatott értékek a következőek:</span><span class="sxs-lookup"><span data-stu-id="f455d-149">The supported values are:</span></span> <br/><br/> <span data-ttu-id="f455d-150">**MicrosoftCloudAgreement,** amely csak *MicrosoftCloudAgreement* típusú szerződési metaadatokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="f455d-150">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="f455d-151">**MicrosoftCustomerAgreement,** amely csak *MicrosoftCustomerAgreement* típusú szerződési metaadatokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="f455d-151">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="f455d-152">**\**_ az összes szerződési metaadatot visszaadja. (Ne használja a _\* \* _ hacsak a kód nem rendelkezik a váratlan szerződéstípusok *kezeléshez szükséges logikával.) <br/> <br/> _* Megjegyzés:*\* Ha az URI paraméter nincs megadva, a lekérdezés alapértelmezés szerint **a MicrosoftCloudAgreement** értéket használja a visszamenőleges kompatibilitás érdekében.</span><span class="sxs-lookup"><span data-stu-id="f455d-152">**\**_ that returns all agreement metadata. (Don't use _*\**_ unless your code has the necessary logic to handle unexpected agreement types.)<br/><br/> _\* Note:*\* If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="f455d-153">A Microsoft bármikor bevezetheti a szerződés metaadatait az új szerződéstípusokkal.</span><span class="sxs-lookup"><span data-stu-id="f455d-153">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="f455d-154">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f455d-154">Request headers</span></span>

<span data-ttu-id="f455d-155">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f455d-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f455d-156">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f455d-156">Request body</span></span>

<span data-ttu-id="f455d-157">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f455d-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f455d-158">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f455d-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="f455d-159">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f455d-159">REST response</span></span>

<span data-ttu-id="f455d-160">Ha a művelet sikeres, ez a metódus **szerződéserőforrások** gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="f455d-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f455d-161">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f455d-161">Response success and error codes</span></span>

<span data-ttu-id="f455d-162">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="f455d-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="f455d-163">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="f455d-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f455d-164">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f455d-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f455d-165">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f455d-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
