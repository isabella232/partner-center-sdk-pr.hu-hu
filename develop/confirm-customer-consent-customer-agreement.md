---
title: Annak megerősítése, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződést
description: Megtudhatja, hogyan erősítheti meg az ügyfelek számára a Microsoft Ügyfélszerződés API Partnerközpont használatával.
ms.date: 02/08/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 002508109191ede53cd06f25efc38286647fd67c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974012"
---
# <a name="confirm-customer-acceptance-of-the-microsoft-customer-agreement-using-partner-center-apis"></a><span data-ttu-id="25e1e-103">Az ügyfél általi elfogadás megerősítése Microsoft Ügyfélszerződés API Partnerközpont használatával</span><span class="sxs-lookup"><span data-stu-id="25e1e-103">Confirm customer acceptance of the Microsoft Customer Agreement using Partner Center APIs</span></span>

<span data-ttu-id="25e1e-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="25e1e-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="25e1e-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="25e1e-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="25e1e-106">Partnerközpont jelenleg csak a Microsoft nyilvános felhőben támogatja a Microsoft Ügyfélszerződés ügyfél általi elfogadásának megerősítését.</span><span class="sxs-lookup"><span data-stu-id="25e1e-106">Partner Center currently supports confirmation of customer acceptance of the Microsoft Customer Agreement only in the Microsoft public cloud.</span></span>

<span data-ttu-id="25e1e-107">Ez a cikk azt ismerteti, hogyan lehet megerősíteni vagy újra megerősíteni az ügyfél általi Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-107">This article describes how to confirm or reconfirm customer acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25e1e-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="25e1e-108">Prerequisites</span></span>

- <span data-ttu-id="25e1e-109">Ha az Partnerközpont .NET SDK-t használja, 1.14-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="25e1e-109">If you are using the Partner Center .NET SDK, version 1.14 or newer is required.</span></span>

- <span data-ttu-id="25e1e-110">Az Partnerközpont [ismertetett hitelesítő adatok.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="25e1e-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="25e1e-111">*Ez a forgatókönyv csak az alkalmazás- és felhasználóhitelesítést támogatja.*</span><span class="sxs-lookup"><span data-stu-id="25e1e-111">*This scenario only supports App+User authentication.*</span></span>

- <span data-ttu-id="25e1e-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25e1e-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="25e1e-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="25e1e-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="25e1e-114">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="25e1e-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="25e1e-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="25e1e-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="25e1e-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="25e1e-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="25e1e-117">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="25e1e-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="25e1e-118">Az a **dátum (dateAgreed**), amikor az ügyfél elfogadta a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-118">The date (**dateAgreed**) when the customer accepted the Microsoft Customer Agreement.</span></span>

- <span data-ttu-id="25e1e-119">Információ az ügyfélszervezettől származó felhasználóról, amely elfogadta a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-119">Information about the user from the customer organization that accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="25e1e-120">Ide tartoznak az alábbiak:</span><span class="sxs-lookup"><span data-stu-id="25e1e-120">This includes:</span></span>
  - <span data-ttu-id="25e1e-121">Utónév</span><span class="sxs-lookup"><span data-stu-id="25e1e-121">First name</span></span>
  - <span data-ttu-id="25e1e-122">Vezetéknév</span><span class="sxs-lookup"><span data-stu-id="25e1e-122">Last name</span></span>
  - <span data-ttu-id="25e1e-123">E-mail-cím</span><span class="sxs-lookup"><span data-stu-id="25e1e-123">Email address</span></span>
  - <span data-ttu-id="25e1e-124">Telefon száma (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="25e1e-124">Phone number (optional)</span></span>
- <span data-ttu-id="25e1e-125">Ha egy ügyfélnél az alábbi értékek változnak, a Partnerközpont lehetővé teszi egy másik szerződés létrejöttét az ügyfél számára: Vezetéknév vezetéknév e-mail-címe Telefon szám. Ellenkező esetben a partnerek a következő hibakódot kapják meg egy duplikált ügyfél létrehozása miatt</span><span class="sxs-lookup"><span data-stu-id="25e1e-125">If the following values change for a customer, Partner Center  will allow for another agreement to be created for that customer:       First Name       Last Name       Email address       Phone number Otherwise partners will receive the following error code, due to a duplicate customer being created</span></span>


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

## <a name="net"></a><span data-ttu-id="25e1e-126">.NET</span><span class="sxs-lookup"><span data-stu-id="25e1e-126">.NET</span></span>

<span data-ttu-id="25e1e-127">A következő feltételek ügyfél általi elfogadásának megerősítése vagy Microsoft Ügyfélszerződés:</span><span class="sxs-lookup"><span data-stu-id="25e1e-127">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="25e1e-128">A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-128">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="25e1e-129">Be kell szereznie a **sablonazonosítót** a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-129">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="25e1e-130">További információkért lásd a [szerződés metaadatainak lekért Microsoft Ügyfélszerződés.](get-customer-agreement-metadata.md)</span><span class="sxs-lookup"><span data-stu-id="25e1e-130">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
   ```

2. <span data-ttu-id="25e1e-131">Hozzon létre egy új **Szerződés** objektumot, amely a megerősítés részleteit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="25e1e-131">Create a new **Agreement** object containing details of the confirmation.</span></span>

3. <span data-ttu-id="25e1e-132">Használja az **IAgreggatePartner.Customers** gyűjteményt, és hívja meg a **ById** metódust a megadott **ügyfél-bérlő-azonosítóval.**</span><span class="sxs-lookup"><span data-stu-id="25e1e-132">Use the **IAgreggatePartner.Customers** collection and call the **ById** method with the specified **customer-tenant-id**.</span></span>

4. <span data-ttu-id="25e1e-133">Használja a **Agreements tulajdonságot,** majd hívja meg a **Create** vagy **a CreateAsync metódust.**</span><span class="sxs-lookup"><span data-stu-id="25e1e-133">Use the **Agreements** property, followed by calling **Create** or **CreateAsync**.</span></span>

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

<span data-ttu-id="25e1e-134">A teljes minta a [CreateCustomerAgreement osztályban](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) található a konzol [tesztalkalmazás-projektből.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="25e1e-134">A complete sample can be found in the [CreateCustomerAgreement](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/CreateCustomerAgreement.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="rest-request"></a><span data-ttu-id="25e1e-135">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="25e1e-135">REST request</span></span>

<span data-ttu-id="25e1e-136">A következő feltételek ügyfél általi elfogadásának megerősítése vagy Microsoft Ügyfélszerződés:</span><span class="sxs-lookup"><span data-stu-id="25e1e-136">To confirm or reconfirm customer acceptance of the Microsoft Customer Agreement:</span></span>

1. <span data-ttu-id="25e1e-137">A szerződés metaadatainak lekérése a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-137">Retrieve the agreement metadata for the Microsoft Customer Agreement.</span></span> <span data-ttu-id="25e1e-138">Be kell szereznie a **sablonazonosítót** a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-138">You must obtain the **templateId** of the Microsoft Customer Agreement.</span></span> <span data-ttu-id="25e1e-139">További információkért lásd a [szerződés metaadatainak lekért Microsoft Ügyfélszerződés.](get-customer-agreement-metadata.md)</span><span class="sxs-lookup"><span data-stu-id="25e1e-139">For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).</span></span>

2. <span data-ttu-id="25e1e-140">Hozzon létre egy új [ **Szerződés** erőforrást](agreement-resources.md) annak megerősítéséhez, hogy az ügyfél elfogadta a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-140">Create a new [**Agreement** resource](agreement-resources.md) to confirm that a customer has accepted the Microsoft Customer Agreement.</span></span> <span data-ttu-id="25e1e-141">Használja a [következő REST-kérési szintaxist:](#request-syntax).</span><span class="sxs-lookup"><span data-stu-id="25e1e-141">Use the following [REST request syntax](#request-syntax).</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25e1e-142">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="25e1e-142">Request syntax</span></span>

| <span data-ttu-id="25e1e-143">Metódus</span><span class="sxs-lookup"><span data-stu-id="25e1e-143">Method</span></span> | <span data-ttu-id="25e1e-144">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="25e1e-144">Request URI</span></span>                                                                                        |
|--------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25e1e-145">POST</span><span class="sxs-lookup"><span data-stu-id="25e1e-145">POST</span></span>   | <span data-ttu-id="25e1e-146">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="25e1e-146">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="25e1e-147">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="25e1e-147">URI parameter</span></span>

<span data-ttu-id="25e1e-148">A következő lekérdezési paraméterrel adhatja meg azt az ügyfelet, akiről megerősítést ad.</span><span class="sxs-lookup"><span data-stu-id="25e1e-148">Use the following query parameter to specify the customer that you're confirming.</span></span>

| <span data-ttu-id="25e1e-149">Név</span><span class="sxs-lookup"><span data-stu-id="25e1e-149">Name</span></span>               | <span data-ttu-id="25e1e-150">Típus</span><span class="sxs-lookup"><span data-stu-id="25e1e-150">Type</span></span> | <span data-ttu-id="25e1e-151">Kötelező</span><span class="sxs-lookup"><span data-stu-id="25e1e-151">Required</span></span> | <span data-ttu-id="25e1e-152">Leírás</span><span class="sxs-lookup"><span data-stu-id="25e1e-152">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="25e1e-153">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="25e1e-153">customer-tenant-id</span></span> | <span data-ttu-id="25e1e-154">GUID</span><span class="sxs-lookup"><span data-stu-id="25e1e-154">GUID</span></span> | <span data-ttu-id="25e1e-155">Igen</span><span class="sxs-lookup"><span data-stu-id="25e1e-155">Yes</span></span> | <span data-ttu-id="25e1e-156">Az érték egy GUID-formátumú **ügyfél-bérlő-azonosító,** amely egy olyan azonosító, amellyel megadhatja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="25e1e-156">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="25e1e-157">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="25e1e-157">Request headers</span></span>

<span data-ttu-id="25e1e-158">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="25e1e-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="25e1e-159">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="25e1e-159">Request body</span></span>

<span data-ttu-id="25e1e-160">Ez a táblázat a REST-kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="25e1e-160">This table describes the required properties in the REST request body.</span></span>

| <span data-ttu-id="25e1e-161">Név</span><span class="sxs-lookup"><span data-stu-id="25e1e-161">Name</span></span>      | <span data-ttu-id="25e1e-162">Típus</span><span class="sxs-lookup"><span data-stu-id="25e1e-162">Type</span></span>   | <span data-ttu-id="25e1e-163">Leírás</span><span class="sxs-lookup"><span data-stu-id="25e1e-163">Description</span></span>                                                                                  |
|-----------|--------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="25e1e-164">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="25e1e-164">Agreement</span></span> | <span data-ttu-id="25e1e-165">object</span><span class="sxs-lookup"><span data-stu-id="25e1e-165">object</span></span> | <span data-ttu-id="25e1e-166">A partner által a feltételek ügyfél általi elfogadásának megerősítéséhez megadott Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-166">Details provided by partner to confirm customer acceptance of the Microsoft Customer Agreement.</span></span> |

#### <a name="agreement"></a><span data-ttu-id="25e1e-167">Megállapodás</span><span class="sxs-lookup"><span data-stu-id="25e1e-167">Agreement</span></span>

<span data-ttu-id="25e1e-168">Ez a táblázat a szerződéserőforrás létrehozásához minimálisan szükséges [ **mezőket** ismerteti.](agreement-resources.md)</span><span class="sxs-lookup"><span data-stu-id="25e1e-168">This table describes the minimum required fields to create an [**Agreement** resource](agreement-resources.md).</span></span>

| <span data-ttu-id="25e1e-169">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="25e1e-169">Property</span></span>       | <span data-ttu-id="25e1e-170">Típus</span><span class="sxs-lookup"><span data-stu-id="25e1e-170">Type</span></span>   | <span data-ttu-id="25e1e-171">Leírás</span><span class="sxs-lookup"><span data-stu-id="25e1e-171">Description</span></span>                              |
|----------------|--------|------------------------------------------|
| <span data-ttu-id="25e1e-172">primaryContact (elsődleges tranzakció)</span><span class="sxs-lookup"><span data-stu-id="25e1e-172">primaryContact</span></span> | [<span data-ttu-id="25e1e-173">Kapcsolatfelvétel</span><span class="sxs-lookup"><span data-stu-id="25e1e-173">Contact</span></span>](./utility-resources.md#contact) | <span data-ttu-id="25e1e-174">A felhasználóval kapcsolatos információk az ügyfélszervezettől, amely elfogadta a Microsoft Ügyfélszerződés, beleértve a  **következőket: firstName,** **lastName,** **e-mail,** és **phoneNumber** (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="25e1e-174">Information about the user from the customer organization who accepted the Microsoft Customer Agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional)</span></span> |
| <span data-ttu-id="25e1e-175">dateAgreed (dátum dátuma)</span><span class="sxs-lookup"><span data-stu-id="25e1e-175">dateAgreed</span></span>     | <span data-ttu-id="25e1e-176">sztring UTC dátum-idő formátumban</span><span class="sxs-lookup"><span data-stu-id="25e1e-176">string in UTC date time format</span></span> |<span data-ttu-id="25e1e-177">Az a dátum, amikor az ügyfél elfogadta a szerződést.</span><span class="sxs-lookup"><span data-stu-id="25e1e-177">The date when the customer accepted the agreement.</span></span> |
| <span data-ttu-id="25e1e-178">templateId (sablonazonosító)</span><span class="sxs-lookup"><span data-stu-id="25e1e-178">templateId</span></span>     | <span data-ttu-id="25e1e-179">sztring</span><span class="sxs-lookup"><span data-stu-id="25e1e-179">string</span></span> | <span data-ttu-id="25e1e-180">Az ügyfél által elfogadott szerződéstípus egyedi azonosítója.</span><span class="sxs-lookup"><span data-stu-id="25e1e-180">Unique identifier of the agreement type accepted by the customer.</span></span> <span data-ttu-id="25e1e-181">A sablon  sablonazonosítóját úgy szerezheti be Microsoft Ügyfélszerződés hogy lekérte a szerződés metaadatait a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-181">You can obtain the **templateId** for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement.</span></span> <span data-ttu-id="25e1e-182">A részletekért tekintse meg a szerződés [metaadatainak le Microsoft Ügyfélszerződés](./get-customer-agreement-metadata.md) kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="25e1e-182">See [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md) for details.</span></span> |
| <span data-ttu-id="25e1e-183">típus</span><span class="sxs-lookup"><span data-stu-id="25e1e-183">type</span></span>           | <span data-ttu-id="25e1e-184">sztring</span><span class="sxs-lookup"><span data-stu-id="25e1e-184">string</span></span> | <span data-ttu-id="25e1e-185">Az ügyfél által elfogadott szerződéstípus.</span><span class="sxs-lookup"><span data-stu-id="25e1e-185">Agreement type accepted by the customer.</span></span> <span data-ttu-id="25e1e-186">Ha az ügyfél elfogadta a Microsoft Ügyfélszerződés, használja a "MicrosoftCustomerAgreement" Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="25e1e-186">Use "MicrosoftCustomerAgreement" if customer accepted the Microsoft Customer Agreement.</span></span> |

#### <a name="request-example"></a><span data-ttu-id="25e1e-187">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="25e1e-187">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="25e1e-188">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="25e1e-188">REST response</span></span>

<span data-ttu-id="25e1e-189">Ha a művelet sikeres, ez a metódus egy [ **szerződéserőforrást ad** vissza.](./agreement-resources.md)</span><span class="sxs-lookup"><span data-stu-id="25e1e-189">If successful, this method returns an [**Agreement** resource](./agreement-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25e1e-190">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="25e1e-190">Response success and error codes</span></span>

<span data-ttu-id="25e1e-191">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="25e1e-191">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="25e1e-192">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="25e1e-192">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="25e1e-193">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="25e1e-193">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="25e1e-194">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="25e1e-194">Response example</span></span>

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
