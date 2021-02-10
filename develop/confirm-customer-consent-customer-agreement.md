---
title: Annak megerősítése, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződést
description: Megtudhatja, hogyan erősítheti meg a Microsoft-ügyfél szerződését a partner Center API-k használatával.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 62a6cebd5d6d093377dd5940dcff6204b7095c70
ms.sourcegitcommit: ebb36208d6e2dea705f62b7d60d471f10c55132e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/09/2021
ms.locfileid: "100006071"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="92890-103">A Microsoft Customer-szerződés ügyfél általi elfogadásának megerősítése a partner Center API-k használatával</span><span class="sxs-lookup"><span data-stu-id="92890-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="92890-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="92890-104">**Applies to:**</span></span>

- <span data-ttu-id="92890-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="92890-105">Partner Center</span></span>

<span data-ttu-id="92890-106">A partner Center jelenleg csak a Microsoft *nyilvános felhőben* támogatja a Microsoft-ügyfél szerződésének megerősítő jóváhagyását.</span><span class="sxs-lookup"><span data-stu-id="92890-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the *Microsoft public cloud*.</span></span> <span data-ttu-id="92890-107">Ez a funkció jelenleg nem érvényes a következőkre:</span><span class="sxs-lookup"><span data-stu-id="92890-107">This functionality doesn't currently apply to:</span></span>

- <span data-ttu-id="92890-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="92890-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="92890-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="92890-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="92890-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="92890-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="92890-111">Ez a cikk azt ismerteti, hogyan lehet megerősíteni vagy újból megerősíteni a Microsoft ügyfél-szerződését.</span><span class="sxs-lookup"><span data-stu-id="92890-111">This article describes how to confirm or re-confirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92890-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="92890-112">Prerequisites</span></span>

- <span data-ttu-id="92890-113">Ha a partner Center .NET SDK-t használja, a 1,14-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="92890-113">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="92890-114">A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="92890-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="92890-115">*Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.*</span><span class="sxs-lookup"><span data-stu-id="92890-115">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="92890-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="92890-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="92890-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="92890-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="92890-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="92890-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="92890-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="92890-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="92890-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="92890-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="92890-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="92890-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="92890-122">A dátum (**dateAgreed**), amikor az ügyfél elfogadta a Microsoft ügyfél-szerződést.</span><span class="sxs-lookup"><span data-stu-id="92890-122">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="92890-123">A Microsoft ügyfél-szerződését elfogadó ügyfélről szóló információ.</span><span class="sxs-lookup"><span data-stu-id="92890-123">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="92890-124">Ide tartoznak az alábbiak:</span><span class="sxs-lookup"><span data-stu-id="92890-124">This includes:</span></span>
  - <span data-ttu-id="92890-125">Utónév</span><span class="sxs-lookup"><span data-stu-id="92890-125">First name</span></span>
  - <span data-ttu-id="92890-126">Vezetéknév</span><span class="sxs-lookup"><span data-stu-id="92890-126">Last name</span></span>
  - <span data-ttu-id="92890-127">E-mail-cím</span><span class="sxs-lookup"><span data-stu-id="92890-127">Email address</span></span>
  - <span data-ttu-id="92890-128">Telefonszám (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="92890-128">Phone number (optional)</span></span>
- <span data-ttu-id="92890-129">Ha az ügyfélen a következő értékek változnak, a partneri központ lehetővé teszi, hogy egy másik szerződést hozzon létre az adott ügyfél számára: Utónév vezetékneve e-mail-cím telefonszáma, máskülönben a partnerek a következő hibakódot kapják meg az ismétlődő ügyfél létrehozása miatt</span><span class="sxs-lookup"><span data-stu-id="92890-129">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


```
{
"code": 600061,
"message": "A partner confirmed agreement already exists for the customer.",
"description": "A partner confirmed agreement already exists for the customer.",
"errorName": "PartnerConfirmedAgreementAlreadyExists",
"isRetryable": false,
"parameters": {},
"errorMessageExtended": "InternalErrorCode=600061"
}
 ```

## <a name="net"></a><span data-ttu-id="92890-130">.NET</span><span class="sxs-lookup"><span data-stu-id="92890-130">.NET</span></span>

<span data-ttu-id="92890-131">A Microsoft ügyfél-szerződés elfogadásának megerősítése vagy újbóli megerősítése:</span><span class="sxs-lookup"><span data-stu-id="92890-131">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="92890-132">Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat.</span><span class="sxs-lookup"><span data-stu-id="92890-132">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="92890-133">Be kell szereznie a Microsoft Customer szerződés **templateId** .</span><span class="sxs-lookup"><span data-stu-id="92890-133">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="92890-134">További részletekért lásd: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="92890-134">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="92890-135">Hozzon létre egy új **Szerződés** objektumot, amely tartalmazza a megerősítés részleteit.</span><span class="sxs-lookup"><span data-stu-id="92890-135">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="92890-136">Használja a **IAgreggatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott **ügyfél-bérlő-azonosítóval**.</span><span class="sxs-lookup"><span data-stu-id="92890-136">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="92890-137">Használja a **szerződések** tulajdonságot, amelyet a **create** vagy a **CreateAsync** hívása követ.</span><span class="sxs-lookup"><span data-stu-id="92890-137">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="92890-138">Teljes minta a [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="92890-138">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="92890-139">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="92890-139">REST request</span></span>

<span data-ttu-id="92890-140">A Microsoft ügyfél-szerződés elfogadásának megerősítése vagy újbóli megerősítése:</span><span class="sxs-lookup"><span data-stu-id="92890-140">To confirm or re-confirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="92890-141">Kérje le a Microsoft Customer szerződéshez tartozó szerződési metaadatokat.</span><span class="sxs-lookup"><span data-stu-id="92890-141">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="92890-142">Be kell szereznie a Microsoft Customer szerződés **templateId** .</span><span class="sxs-lookup"><span data-stu-id="92890-142">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="92890-143">További részletekért lásd: [a szerződés metaadatainak beszerzése a Microsoft ügyfél-szerződéshez](get-customer-agreement-metadata.md).</span><span class="sxs-lookup"><span data-stu-id="92890-143">For more details, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="92890-144">Hozzon létre egy új [ **szerződési** erőforrást](agreement-resources.md) annak megerősítéséhez, hogy az ügyfél elfogadta a Microsoft ügyfél-szerződést.</span><span class="sxs-lookup"><span data-stu-id="92890-144">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="92890-145">Használja az alábbi [Rest-kérelem szintaxisát](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="92890-145">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="92890-146">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="92890-146">Request syntax</span></span>

| <span data-ttu-id="92890-147">Metódus</span><span class="sxs-lookup"><span data-stu-id="92890-147">Method</span></span> | <span data-ttu-id="92890-148">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="92890-148">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="92890-149">POST</span><span class="sxs-lookup"><span data-stu-id="92890-149">POST</span></span>   | <span data-ttu-id="92890-150">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="92890-150">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="92890-151">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="92890-151">URI parameter</span></span>

<span data-ttu-id="92890-152">A következő lekérdezési paraméterrel adhatja meg a megerősítő ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="92890-152">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="92890-153">Név</span><span class="sxs-lookup"><span data-stu-id="92890-153">Name</span></span>               | <span data-ttu-id="92890-154">Típus</span><span class="sxs-lookup"><span data-stu-id="92890-154">Type</span></span> | <span data-ttu-id="92890-155">Kötelező</span><span class="sxs-lookup"><span data-stu-id="92890-155">Required</span></span> | <span data-ttu-id="92890-156">Leírás</span><span class="sxs-lookup"><span data-stu-id="92890-156">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="92890-157">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="92890-157">customer-tenant-id</span></span> | <span data-ttu-id="92890-158">GUID</span><span class="sxs-lookup"><span data-stu-id="92890-158">GUID</span></span> | <span data-ttu-id="92890-159">Igen</span><span class="sxs-lookup"><span data-stu-id="92890-159">Yes</span></span> | <span data-ttu-id="92890-160">Az érték egy GUID-formátumú **ügyfél-bérlői azonosító**, amely egy ügyfél megadását lehetővé tevő azonosító.</span><span class="sxs-lookup"><span data-stu-id="92890-160">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="92890-161">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="92890-161">Request headers</span></span>

<span data-ttu-id="92890-162">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="92890-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="92890-163">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="92890-163">Request body</span></span>

<span data-ttu-id="92890-164">Ez a táblázat a REST-kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="92890-164">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="92890-165">Név</span><span class="sxs-lookup"><span data-stu-id="92890-165">Name</span></span>      | <span data-ttu-id="92890-166">Típus</span><span class="sxs-lookup"><span data-stu-id="92890-166">Type</span></span>   | <span data-ttu-id="92890-167">Description</span><span class="sxs-lookup"><span data-stu-id="92890-167">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="92890-168">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="92890-168">Agreement</span></span> | <span data-ttu-id="92890-169">object</span><span class="sxs-lookup"><span data-stu-id="92890-169">object</span></span> | <span data-ttu-id="92890-170">A partner által biztosított részletek a Microsoft ügyfél-szerződésének megerősítő elfogadásának megerősítéséhez.</span><span class="sxs-lookup"><span data-stu-id="92890-170">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="92890-171">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="92890-171">Agreement</span></span>

<span data-ttu-id="92890-172">Ez a táblázat a [ **szerződési** erőforrások](agreement-resources.md)létrehozásához szükséges minimális mezőket ismerteti.</span><span class="sxs-lookup"><span data-stu-id="92890-172">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="92890-173">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="92890-173">Property</span></span>       | <span data-ttu-id="92890-174">Típus</span><span class="sxs-lookup"><span data-stu-id="92890-174">Type</span></span>   | <span data-ttu-id="92890-175">Description</span><span class="sxs-lookup"><span data-stu-id="92890-175">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="92890-176">primaryContact</span><span class="sxs-lookup"><span data-stu-id="92890-176">primaryContact</span></span> | [<span data-ttu-id="92890-177">Kapcsolatfelvétel</span><span class="sxs-lookup"><span data-stu-id="92890-177">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="92890-178">Információk a Microsoft ügyfél-szerződést elfogadó, a  **firstName**, a **lastName**, az **e-mail** és a **telefonszám** (nem kötelező) felhasználóról</span><span class="sxs-lookup"><span data-stu-id="92890-178">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email** and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="92890-179">dateAgreed</span><span class="sxs-lookup"><span data-stu-id="92890-179">dateAgreed</span></span>     | <span data-ttu-id="92890-180">karakterlánc UTC-dátum időformátuma</span><span class="sxs-lookup"><span data-stu-id="92890-180">string in UTC date time format</span></span> |<span data-ttu-id="92890-181">Az a dátum, amikor az ügyfél elfogadta a szerződést.</span><span class="sxs-lookup"><span data-stu-id="92890-181">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="92890-182">templateId</span><span class="sxs-lookup"><span data-stu-id="92890-182">templateId</span></span>     | <span data-ttu-id="92890-183">sztring</span><span class="sxs-lookup"><span data-stu-id="92890-183">string</span></span> | <span data-ttu-id="92890-184">Az ügyfél által elfogadott szerződés típusának egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="92890-184">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="92890-185">A Microsoft ügyfél-szerződéshez tartozó **templateId** beszerezheti a Microsoft-szerződés metaadatainak beolvasásával.</span><span class="sxs-lookup"><span data-stu-id="92890-185">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="92890-186">További részletekért lásd: a [Szerződés metaadatainak beszerzése a Microsoft Customer szerződéshez](./get-customer-agreement-metadata.md) .</span><span class="sxs-lookup"><span data-stu-id="92890-186">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="92890-187">típus</span><span class="sxs-lookup"><span data-stu-id="92890-187">type</span></span>           | <span data-ttu-id="92890-188">sztring</span><span class="sxs-lookup"><span data-stu-id="92890-188">string</span></span> | <span data-ttu-id="92890-189">Az ügyfél által elfogadott szerződés típusa.</span><span class="sxs-lookup"><span data-stu-id="92890-189">Agreement type accepted by the customer.</span></span> <span data-ttu-id="92890-190">Ha az ügyfél elfogadta a Microsoft Customer szerződést, használja a "MicrosoftCustomerAgreement" lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="92890-190">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="92890-191">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="92890-191">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="92890-192">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="92890-192">REST response</span></span>

<span data-ttu-id="92890-193">Ha ez sikeres, ez a metódus egy [ **Szerződés** -erőforrást](./agreement-resources.md)ad vissza.</span><span class="sxs-lookup"><span data-stu-id="92890-193">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="92890-194">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="92890-194">Response success and error codes</span></span>

<span data-ttu-id="92890-195">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="92890-195">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="92890-196">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="92890-196">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="92890-197">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="92890-197">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="92890-198">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="92890-198">Response example</span></span>

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
