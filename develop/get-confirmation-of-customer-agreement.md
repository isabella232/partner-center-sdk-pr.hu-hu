---
title: A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősíteni a Microsoft ügyfél-szerződés elfogadását.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/14/2020
ms.locfileid: "97768167"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="2f5b2-103">A Microsoft Ügyfélszerződés ügyfél általi elfogadási megerősítésének lekérése</span><span class="sxs-lookup"><span data-stu-id="2f5b2-103">Get confirmation of customer acceptance of Microsoft Customer Agreement</span></span>

<span data-ttu-id="2f5b2-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="2f5b2-104">**Applies to:**</span></span>

- <span data-ttu-id="2f5b2-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="2f5b2-105">Partner Center</span></span>

<span data-ttu-id="2f5b2-106">A partner Center jelenleg csak a *Microsoft nyilvános felhőben* támogatja a **szerződési** erőforrást.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-106">The **Agreement** resource is currently supported by Partner Center only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="2f5b2-107">Ez az erőforrás nem vonatkozik a következőkre:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-107">This resource doesn't apply to:</span></span>

- <span data-ttu-id="2f5b2-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="2f5b2-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2f5b2-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2f5b2-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2f5b2-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="2f5b2-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2f5b2-111">Ez a cikk azt ismerteti, hogyan kérhető le a Microsoft ügyfél-szerződés elfogadásának megerősítése (i).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-111">This article explains how you can retrieve confirmation(s) of a customer's acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f5b2-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="2f5b2-112">Prerequisites</span></span>

- <span data-ttu-id="2f5b2-113">Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="2f5b2-114">A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="2f5b2-115">Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-115">This scenario only supports App+User authentication.</span></span>

- <span data-ttu-id="2f5b2-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2f5b2-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2f5b2-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2f5b2-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2f5b2-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2f5b2-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net"></a><span data-ttu-id="2f5b2-122">.NET</span><span class="sxs-lookup"><span data-stu-id="2f5b2-122">.NET</span></span>

<span data-ttu-id="2f5b2-123">A korábban megadott ügyfél-elfogadás megerősítése (i) beolvasása:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="2f5b2-124">Használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="2f5b2-125">A **ByAgreementType** metódus meghívásával olvassa be a **szerződések** tulajdonságot, és szűrje az eredményeket a Microsoft ügyfél-szerződésre.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-125">Fetch the **Agreements** property and filter the results to Microsoft Customer Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="2f5b2-126">A **Get** vagy a **GetAsync** metódus hívása.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="2f5b2-127">Teljes minta a [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="2f5b2-128">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="2f5b2-128">REST request</span></span>

<span data-ttu-id="2f5b2-129">A korábban megadott ügyfél-elfogadás megerősítésének beolvasása:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-129">To retrieve confirmation of customer acceptance that was previously provided:</span></span>

1. <span data-ttu-id="2f5b2-130">Hozzon létre egy REST-kérelmet a [szerződések](./agreement-resources.md) gyűjtésének lekéréséhez az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-130">Create a REST request to retrieve the [Agreements](./agreement-resources.md) collection for the customer.</span></span>

2. <span data-ttu-id="2f5b2-131">A **agreementType** lekérdezési paraméterrel az eredményeket csak a Microsoft ügyfél-szerződésre szűkítheti.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-131">Use the **agreementType** query parameter to scope the results to only the Microsoft Customer Agreement.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f5b2-132">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="2f5b2-132">Request syntax</span></span>

<span data-ttu-id="2f5b2-133">Használja a következő kérelem szintaxisát:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-133">Use the following request syntax:</span></span>

| <span data-ttu-id="2f5b2-134">Metódus</span><span class="sxs-lookup"><span data-stu-id="2f5b2-134">Method</span></span> | <span data-ttu-id="2f5b2-135">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="2f5b2-135">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f5b2-136">GET</span><span class="sxs-lookup"><span data-stu-id="2f5b2-136">GET</span></span>    | <span data-ttu-id="2f5b2-137">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements? agreementType = {egyezmény-típus} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2f5b2-137">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements?agreementType={agreement-type} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2f5b2-138">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="2f5b2-138">URI parameters</span></span>

<span data-ttu-id="2f5b2-139">A kérelemhez a következő URI-paramétereket használhatja:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-139">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="2f5b2-140">Név</span><span class="sxs-lookup"><span data-stu-id="2f5b2-140">Name</span></span>             | <span data-ttu-id="2f5b2-141">Típus</span><span class="sxs-lookup"><span data-stu-id="2f5b2-141">Type</span></span> | <span data-ttu-id="2f5b2-142">Kötelező</span><span class="sxs-lookup"><span data-stu-id="2f5b2-142">Required</span></span> | <span data-ttu-id="2f5b2-143">Leírás</span><span class="sxs-lookup"><span data-stu-id="2f5b2-143">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="2f5b2-144">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="2f5b2-144">customer-tenant-id</span></span> | <span data-ttu-id="2f5b2-145">GUID</span><span class="sxs-lookup"><span data-stu-id="2f5b2-145">GUID</span></span> | <span data-ttu-id="2f5b2-146">Igen</span><span class="sxs-lookup"><span data-stu-id="2f5b2-146">Yes</span></span> | <span data-ttu-id="2f5b2-147">Az érték egy GUID formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél megadását.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-147">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |
| <span data-ttu-id="2f5b2-148">szerződés típusa</span><span class="sxs-lookup"><span data-stu-id="2f5b2-148">agreement-type</span></span> | <span data-ttu-id="2f5b2-149">sztring</span><span class="sxs-lookup"><span data-stu-id="2f5b2-149">string</span></span> | <span data-ttu-id="2f5b2-150">No</span><span class="sxs-lookup"><span data-stu-id="2f5b2-150">No</span></span> | <span data-ttu-id="2f5b2-151">Ez a paraméter az összes szerződési metaadatot visszaadja.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-151">This parameter returns all agreement metadata.</span></span> <span data-ttu-id="2f5b2-152">Ezzel a paraméterrel a lekérdezési választ adott szerződési típusra szűkítheti.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-152">Use this parameter to scope the query response to specific agreement type.</span></span> <span data-ttu-id="2f5b2-153">A támogatott értékek a következők:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-153">The supported values are:</span></span> <br/><br/> <span data-ttu-id="2f5b2-154">**MicrosoftCloudAgreement** , amely csak a *MicrosoftCloudAgreement* típusú megállapodás-metaadatokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-154">**MicrosoftCloudAgreement** that only includes agreement metadata of the type *MicrosoftCloudAgreement*.</span></span><br/><br/> <span data-ttu-id="2f5b2-155">**MicrosoftCustomerAgreement** , amely csak a *MicrosoftCustomerAgreement* típusú megállapodás-metaadatokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-155">**MicrosoftCustomerAgreement** that only includes agreement metadata of the type *MicrosoftCustomerAgreement*.</span></span><br/><br/> <span data-ttu-id="2f5b2-156">**\*** Ez az összes szerződési metaadatot visszaadja.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-156">**\*** that returns all agreement metadata.</span></span> <span data-ttu-id="2f5b2-157">(Ne használja **\*** , kivéve, ha a kód nem rendelkezik a váratlan szerződések típusának kezeléséhez szükséges logikával.)</span><span class="sxs-lookup"><span data-stu-id="2f5b2-157">(Don't use **\*** unless your code has the necessary logic to handle unexpected agreement types.)</span></span><br/><br/> <span data-ttu-id="2f5b2-158">**Megjegyzés:** Ha nincs megadva az URI paraméter, a lekérdezés alapértelmezés szerint **MicrosoftCloudAgreement** a visszafelé kompatibilitás érdekében.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-158">**Note:** If the URI parameter isn't specified, the query defaults to **MicrosoftCloudAgreement** for backward compatibility.</span></span> <span data-ttu-id="2f5b2-159">A Microsoft bármikor bevezethet szerződési metaadatokat új szerződési típusokkal.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-159">Microsoft may introduce agreement metadata with new agreement types at any time.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="2f5b2-160">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="2f5b2-160">Request headers</span></span>

<span data-ttu-id="2f5b2-161">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f5b2-162">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="2f5b2-162">Request body</span></span>

<span data-ttu-id="2f5b2-163">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-163">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2f5b2-164">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="2f5b2-164">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="2f5b2-165">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="2f5b2-165">REST response</span></span>

<span data-ttu-id="2f5b2-166">Ha ez sikeres, ez a metódus a válasz törzsében a **Szerződés** erőforrásainak gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-166">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f5b2-167">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="2f5b2-167">Response success and error codes</span></span>

<span data-ttu-id="2f5b2-168">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-168">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="2f5b2-169">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-169">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f5b2-170">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-170">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2f5b2-171">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="2f5b2-171">Response example</span></span>

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
