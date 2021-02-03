---
title: Annak megerősítése, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződést
description: Megtudhatja, hogyan erősítheti meg a Microsoft-ügyfél szerződését a partner Center API-k használatával.
ms.date: 02/04/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 239ca43c70fb8aa7f0d06e564e6c0726b235ffbe
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/04/2020
ms.locfileid: "97768591"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="27b8b-103">A Microsoft Customer-szerződés ügyfél általi elfogadásának megerősítése a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="27b8b-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="27b8b-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="27b8b-104">**Applies to:**</span></span>

- <span data-ttu-id="27b8b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="27b8b-105">Partner Center</span></span>

<span data-ttu-id="27b8b-106">A partner Center jelenleg csak a Microsoft *nyilvános felhőben* támogatja a Microsoft-ügyfél szerződésének megerősítő jóváhagyását.</span><span class="sxs-lookup"><span data-stu-id="27b8b-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="27b8b-107">Ez a funkció jelenleg nem érvényes a következőkre:</span><span class="sxs-lookup"><span data-stu-id="27b8b-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="27b8b-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="27b8b-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="27b8b-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="27b8b-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="27b8b-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="27b8b-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="27b8b-111">Ez a cikk azt ismerteti, hogyan lehet megerősíteni vagy újból megerősíteni a Microsoft ügyfél-szerződését.</span><span class="sxs-lookup"><span data-stu-id="27b8b-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27b8b-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="27b8b-112">Prerequisites</span></span>

- <span data-ttu-id="27b8b-113">Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="27b8b-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="27b8b-114">A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="27b8b-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="27b8b-115">*Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.*</span><span class="sxs-lookup"><span data-stu-id="27b8b-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="27b8b-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="27b8b-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="27b8b-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="27b8b-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="27b8b-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="27b8b-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="27b8b-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="27b8b-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="27b8b-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="27b8b-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="27b8b-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="27b8b-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="27b8b-122">A dátum (**dateAgreed**), amikor az ügyfél elfogadta a Microsoft ügyfél-szerződést.</span><span class="sxs-lookup"><span data-stu-id="27b8b-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="27b8b-123">A Microsoft ügyfél-szerződését elfogadó ügyfélről szóló információ.</span><span class="sxs-lookup"><span data-stu-id="27b8b-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="27b8b-124">Ide tartoznak az alábbiak:</span><span class="sxs-lookup"><span data-stu-id="27b8b-124">This includes:</span></span>
  - <span data-ttu-id="27b8b-125">Utónév</span><span class="sxs-lookup"><span data-stu-id="27b8b-125">First name</span></span>
  - <span data-ttu-id="27b8b-126">Vezetéknév</span><span class="sxs-lookup"><span data-stu-id="27b8b-126">Last name</span></span>
  - <span data-ttu-id="27b8b-127">E-mail-cím</span><span class="sxs-lookup"><span data-stu-id="27b8b-127">Email address</span></span>
  - <span data-ttu-id="27b8b-128">Telefonszám (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="27b8b-128">Phone number (optional)</span></span>

## <a name="net"></a><span data-ttu-id="27b8b-129">.NET</span><span class="sxs-lookup"><span data-stu-id="27b8b-129">.NET</span></span>

<span data-ttu-id="27b8b-130">A Microsoft ügyfél-szerződés elfogadásának megerősítése vagy újbóli megerősítése:</span><span class="sxs-lookup"><span data-stu-id="27b8b-130">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="27b8b-131">Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat.</span><span class="sxs-lookup"><span data-stu-id="27b8b-131">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="27b8b-132">Be kell szereznie a Microsoft Customer szerződés **templateId** .</span><span class="sxs-lookup"><span data-stu-id="27b8b-132">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="27b8b-133">További részletekért lásd: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="27b8b-133">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="27b8b-134">Hozzon létre egy új **Szerződés** objektumot, amely tartalmazza a megerősítés részleteit.</span><span class="sxs-lookup"><span data-stu-id="27b8b-134">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="27b8b-135">Használja a **IAgreggatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott **ügyfél-bérlő-azonosítóval**.</span><span class="sxs-lookup"><span data-stu-id="27b8b-135">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="27b8b-136">Használja a **szerződések** tulajdonságot, amelyet a **create** vagy a **CreateAsync** hívása követ.</span><span class="sxs-lookup"><span data-stu-id="27b8b-136">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

   ```csharp
   // string selectedCustomerId;

   var agreementToCreate = new Agreement
   {
       DateAgreed = DateTime.UtcNow,
       TemplateId = microsoftCustomerAgreementDetails.TemplateId,
       PrimaryContact = new Contact
       {
           FirstName = "Tania",
           LastName = "Carr",
           Email = "someone@example.com",
           PhoneNumber = "1234567890"
       }
   };

   Agreement agreement = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Create(agreementToCreate);
   ```

<span data-ttu-id="27b8b-137">Teljes minta a [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="27b8b-137">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="27b8b-138">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="27b8b-138">REST request</span></span>

<span data-ttu-id="27b8b-139">A Microsoft ügyfél-szerződés elfogadásának megerősítése vagy újbóli megerősítése:</span><span class="sxs-lookup"><span data-stu-id="27b8b-139">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="27b8b-140">Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat.</span><span class="sxs-lookup"><span data-stu-id="27b8b-140">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="27b8b-141">Be kell szereznie a Microsoft Customer szerződés **templateId** .</span><span class="sxs-lookup"><span data-stu-id="27b8b-141">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="27b8b-142">További részletekért lásd: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="27b8b-142">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="27b8b-143">Hozzon létre egy új [ **szerződési** erőforrást](agreement-resources.md) annak megerősítéséhez, hogy az ügyfél elfogadta a Microsoft ügyfél-szerződést.</span><span class="sxs-lookup"><span data-stu-id="27b8b-143">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="27b8b-144">Használja az alábbi [Rest-kérelem szintaxisát](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="27b8b-144">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="27b8b-145">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="27b8b-145">Request syntax</span></span>

| <span data-ttu-id="27b8b-146">Metódus</span><span class="sxs-lookup"><span data-stu-id="27b8b-146">Method</span></span> | <span data-ttu-id="27b8b-147">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="27b8b-147">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="27b8b-148">POST</span><span class="sxs-lookup"><span data-stu-id="27b8b-148">POST</span></span>   | <span data-ttu-id="27b8b-149">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="27b8b-149">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="27b8b-150">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="27b8b-150">URI parameter</span></span>

<span data-ttu-id="27b8b-151">A következő lekérdezési paraméterrel adhatja meg a megerősítő ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="27b8b-151">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="27b8b-152">Név</span><span class="sxs-lookup"><span data-stu-id="27b8b-152">Name</span></span>               | <span data-ttu-id="27b8b-153">Típus</span><span class="sxs-lookup"><span data-stu-id="27b8b-153">Type</span></span> | <span data-ttu-id="27b8b-154">Kötelező</span><span class="sxs-lookup"><span data-stu-id="27b8b-154">Required</span></span> | <span data-ttu-id="27b8b-155">Leírás</span><span class="sxs-lookup"><span data-stu-id="27b8b-155">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="27b8b-156">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="27b8b-156">customer-tenant-id</span></span> | <span data-ttu-id="27b8b-157">GUID</span><span class="sxs-lookup"><span data-stu-id="27b8b-157">GUID</span></span> | <span data-ttu-id="27b8b-158">Igen</span><span class="sxs-lookup"><span data-stu-id="27b8b-158">Yes</span></span> | <span data-ttu-id="27b8b-159">Az érték egy GUID-formátumú **ügyfél-bérlői azonosító**, amely egy ügyfél megadását lehetővé tevő azonosító.</span><span class="sxs-lookup"><span data-stu-id="27b8b-159">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="27b8b-160">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="27b8b-160">Request headers</span></span>

<span data-ttu-id="27b8b-161">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="27b8b-161">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="27b8b-162">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="27b8b-162">Request body</span></span>

<span data-ttu-id="27b8b-163">Ez a táblázat a REST-kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="27b8b-163">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="27b8b-164">Név</span><span class="sxs-lookup"><span data-stu-id="27b8b-164">Name</span></span>      | <span data-ttu-id="27b8b-165">Típus</span><span class="sxs-lookup"><span data-stu-id="27b8b-165">Type</span></span>   | <span data-ttu-id="27b8b-166">Leírás</span><span class="sxs-lookup"><span data-stu-id="27b8b-166">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="27b8b-167">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="27b8b-167">Agreement</span></span> | <span data-ttu-id="27b8b-168">object</span><span class="sxs-lookup"><span data-stu-id="27b8b-168">object</span></span> | <span data-ttu-id="27b8b-169">A partner által biztosított részletek a Microsoft ügyfél-szerződésének megerősítő elfogadásának megerősítéséhez.</span><span class="sxs-lookup"><span data-stu-id="27b8b-169">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="27b8b-170">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="27b8b-170">Agreement</span></span>

<span data-ttu-id="27b8b-171">Ez a táblázat a [ **szerződési** erőforrások](agreement-resources.md)létrehozásához szükséges minimális mezőket ismerteti.</span><span class="sxs-lookup"><span data-stu-id="27b8b-171">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="27b8b-172">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="27b8b-172">Property</span></span>       | <span data-ttu-id="27b8b-173">Típus</span><span class="sxs-lookup"><span data-stu-id="27b8b-173">Type</span></span>   | <span data-ttu-id="27b8b-174">Leírás</span><span class="sxs-lookup"><span data-stu-id="27b8b-174">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="27b8b-175">primaryContact</span><span class="sxs-lookup"><span data-stu-id="27b8b-175">primaryContact</span></span> | [<span data-ttu-id="27b8b-176">Kapcsolatfelvétel</span><span class="sxs-lookup"><span data-stu-id="27b8b-176">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="27b8b-177">Információk a Microsoft ügyfél-szerződést elfogadó, a  **firstName**, a **lastName**, az **e-mail** és a **telefonszám** (nem kötelező) felhasználóról</span><span class="sxs-lookup"><span data-stu-id="27b8b-177">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="27b8b-178">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="27b8b-178">dateAgreed</span></span>     | <span data-ttu-id="27b8b-179">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="27b8b-179">string in UTC date time format</span></span> |<span data-ttu-id="27b8b-180">Az a dátum, amikor az ügyfél elfogadta a szerződést.</span><span class="sxs-lookup"><span data-stu-id="27b8b-180">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="27b8b-181">templateId</span><span class="sxs-lookup"><span data-stu-id="27b8b-181">templateId</span></span>     | <span data-ttu-id="27b8b-182">sztring</span><span class="sxs-lookup"><span data-stu-id="27b8b-182">string</span></span> | <span data-ttu-id="27b8b-183">Az ügyfél által elfogadott szerződés típusának egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="27b8b-183">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="27b8b-184">A Microsoft ügyfél-szerződéshez tartozó **templateId** beszerezheti a Microsoft-szerződés metaadatainak beolvasásával.</span><span class="sxs-lookup"><span data-stu-id="27b8b-184">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="27b8b-185">További részletekért lásd: a [Szerződés metaadatainak beszerzése a Microsoft Customer szerződéshez](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="27b8b-185">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="27b8b-186">típus</span><span class="sxs-lookup"><span data-stu-id="27b8b-186">type</span></span>           | <span data-ttu-id="27b8b-187">sztring</span><span class="sxs-lookup"><span data-stu-id="27b8b-187">string</span></span> | <span data-ttu-id="27b8b-188">Az ügyfél által elfogadott szerződés típusa.</span><span class="sxs-lookup"><span data-stu-id="27b8b-188">Agreement type accepted by the customer.</span></span> <span data-ttu-id="27b8b-189">Ha az ügyfél elfogadta a Microsoft Customer szerződést, használja a "MicrosoftCustomerAgreement" lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="27b8b-189">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="27b8b-190">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="27b8b-190">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```

## <a name="rest-response"></a><span data-ttu-id="27b8b-191">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="27b8b-191">REST response</span></span>

<span data-ttu-id="27b8b-192">Ha ez sikeres, ez a metódus egy [ **Szerződés** -erőforrást](./agreement-resources.md)ad vissza.</span><span class="sxs-lookup"><span data-stu-id="27b8b-192">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="27b8b-193">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="27b8b-193">Response success and error codes</span></span>

<span data-ttu-id="27b8b-194">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="27b8b-194">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="27b8b-195">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="27b8b-195">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="27b8b-196">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="27b8b-196">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="27b8b-197">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="27b8b-197">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 261
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "userId": "3d6f2c09-eb40-48ca-a4b3-d24c9c007531",
    "primaryContact": {
        "firstName": "Tania",
        "lastName": "Carr",
        "email": "someone@example.com",
        "phoneNumber": "1234567890"
    },
    "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
    "dateAgreed": "2018-06-14T00:00:00.000Z",
    "type": "MicrosoftCustomerAgreement"
}
```
