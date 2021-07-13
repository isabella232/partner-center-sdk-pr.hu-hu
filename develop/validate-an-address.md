---
title: Cím ellenőrzése
description: Cím ellenőrzése a címérvényesítési API-val.
ms.date: 05/17/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30f5cd526ab038dce400e79822d89b8086ba3799
ms.sourcegitcommit: 41bf9dca55f4c96d382b327a75b2d2418edfc9bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/13/2021
ms.locfileid: "113655609"
---
# <a name="validate-an-address"></a><span data-ttu-id="476b7-103">Cím ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="476b7-103">Validate an address</span></span>

<span data-ttu-id="476b7-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="476b7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="476b7-105">Cím ellenőrzése a címérvényesítési API-val.</span><span class="sxs-lookup"><span data-stu-id="476b7-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="476b7-106">A címérvényesítési API csak az ügyfélprofilok frissítésének előzetes érvényesítéséhez használható.</span><span class="sxs-lookup"><span data-stu-id="476b7-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="476b7-107">Használja annak tudatában, hogy ha az ország az Egyesült Államok, Kanada, Kína vagy Mexikó, akkor az állam mező az adott ország érvényes államlistával lesz ellenőrizve.</span><span class="sxs-lookup"><span data-stu-id="476b7-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="476b7-108">Az összes többi országban ez a teszt nem történik meg, és az API csak azt ellenőrzi, hogy az állam érvényes sztring-e.</span><span class="sxs-lookup"><span data-stu-id="476b7-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="476b7-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="476b7-109">Prerequisites</span></span>

<span data-ttu-id="476b7-110">A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="476b7-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="476b7-111">Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="476b7-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="476b7-112">C\#</span><span class="sxs-lookup"><span data-stu-id="476b7-112">C\#</span></span>

<span data-ttu-id="476b7-113">A cím érvényesítéséhez először példányosítenie kell egy új **Cím** objektumot, és ki kell feltöltenie a címet az ellenőrzéshez.</span><span class="sxs-lookup"><span data-stu-id="476b7-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="476b7-114">Ezután az **IAggregatePartner.Validations** tulajdonságból olvassa be az Ellenőrzési műveletek felületét, és hívja meg az **IsAddressValid** metódust a címobjektummal. </span><span class="sxs-lookup"><span data-stu-id="476b7-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",
    Country = "US"
};

// Validate the address.
AddressValidationResponse result = partnerOperations.Validations.IsAddressValid(address);

// If the request completes successfully, you can inspect the response object.

// See the status of the validation.
Console.WriteLine($"Status: {addressValidationResult.Status}");

// See the validation message returned.
Console.WriteLine($"Validation Message Returned: {addressValidationResult.ValidationMessage ?? "No message returned."}");

// See the original address submitted for validation.
Console.WriteLine($"Original Address:\n{this.DisplayAddress(addressValidationResult.OriginalAddress)}");

// See the suggested addresses returned by the API, if any exist.
Console.WriteLine($"Suggested Addresses Returned: {addressValidationResult.SuggestedAddresses?.Count ?? "None."}");

if (addressValidationResult.SuggestedAddresses != null && addressValidationResult.SuggestedAddresses.Any())
{
    addressValidationResult.SuggestedAddresses.ForEach(a => Console.WriteLine(this.DisplayAddress(a)));
}

// Helper method to pretty-print an Address object.
private string DisplayAddress(Address address)
{
    StringBuilder sb = new StringBuilder();

    foreach (var property in address.GetType().GetProperties())
    {
        sb.AppendLine($"{property.Name}: {property.GetValue(address) ?? "None to Display."}");
    }

    return sb.ToString();
}
```

## <a name="rest-request"></a><span data-ttu-id="476b7-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="476b7-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="476b7-116">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="476b7-116">Request syntax</span></span>

| <span data-ttu-id="476b7-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="476b7-117">Method</span></span>   | <span data-ttu-id="476b7-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="476b7-118">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="476b7-119">**Post**</span><span class="sxs-lookup"><span data-stu-id="476b7-119">**POST**</span></span> | <span data-ttu-id="476b7-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="476b7-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="476b7-121">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="476b7-121">Request headers</span></span>

<span data-ttu-id="476b7-122">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="476b7-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="476b7-123">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="476b7-123">Request body</span></span>

<span data-ttu-id="476b7-124">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="476b7-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="476b7-125">Név</span><span class="sxs-lookup"><span data-stu-id="476b7-125">Name</span></span>         | <span data-ttu-id="476b7-126">Típus</span><span class="sxs-lookup"><span data-stu-id="476b7-126">Type</span></span>   | <span data-ttu-id="476b7-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="476b7-127">Required</span></span> | <span data-ttu-id="476b7-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="476b7-128">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="476b7-129">addressline1</span><span class="sxs-lookup"><span data-stu-id="476b7-129">addressline1</span></span> | <span data-ttu-id="476b7-130">sztring</span><span class="sxs-lookup"><span data-stu-id="476b7-130">string</span></span> | <span data-ttu-id="476b7-131">Y</span><span class="sxs-lookup"><span data-stu-id="476b7-131">Y</span></span>        | <span data-ttu-id="476b7-132">A cím első sorában.</span><span class="sxs-lookup"><span data-stu-id="476b7-132">The first line of the address.</span></span>                             |
| <span data-ttu-id="476b7-133">addressline2</span><span class="sxs-lookup"><span data-stu-id="476b7-133">addressline2</span></span> | <span data-ttu-id="476b7-134">sztring</span><span class="sxs-lookup"><span data-stu-id="476b7-134">string</span></span> | <span data-ttu-id="476b7-135">N</span><span class="sxs-lookup"><span data-stu-id="476b7-135">N</span></span>        | <span data-ttu-id="476b7-136">A cím második sorában.</span><span class="sxs-lookup"><span data-stu-id="476b7-136">The second line of the address.</span></span> <span data-ttu-id="476b7-137">Ez a tulajdonság nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="476b7-137">This property is optional.</span></span> |
| <span data-ttu-id="476b7-138">city</span><span class="sxs-lookup"><span data-stu-id="476b7-138">city</span></span>         | <span data-ttu-id="476b7-139">sztring</span><span class="sxs-lookup"><span data-stu-id="476b7-139">string</span></span> | <span data-ttu-id="476b7-140">Y</span><span class="sxs-lookup"><span data-stu-id="476b7-140">Y</span></span>        | <span data-ttu-id="476b7-141">A város.</span><span class="sxs-lookup"><span data-stu-id="476b7-141">The city.</span></span>                                                  |
| <span data-ttu-id="476b7-142">állapot</span><span class="sxs-lookup"><span data-stu-id="476b7-142">state</span></span>        | <span data-ttu-id="476b7-143">sztring</span><span class="sxs-lookup"><span data-stu-id="476b7-143">string</span></span> | <span data-ttu-id="476b7-144">Y</span><span class="sxs-lookup"><span data-stu-id="476b7-144">Y</span></span>        | <span data-ttu-id="476b7-145">Az állapot.</span><span class="sxs-lookup"><span data-stu-id="476b7-145">The state.</span></span>                                                 |
| <span data-ttu-id="476b7-146">irányítószám</span><span class="sxs-lookup"><span data-stu-id="476b7-146">postalcode</span></span>   | <span data-ttu-id="476b7-147">sztring</span><span class="sxs-lookup"><span data-stu-id="476b7-147">string</span></span> | <span data-ttu-id="476b7-148">Y</span><span class="sxs-lookup"><span data-stu-id="476b7-148">Y</span></span>        | <span data-ttu-id="476b7-149">Az irányítószám.</span><span class="sxs-lookup"><span data-stu-id="476b7-149">The postal code.</span></span>                                           |
| <span data-ttu-id="476b7-150">ország</span><span class="sxs-lookup"><span data-stu-id="476b7-150">country</span></span>      | <span data-ttu-id="476b7-151">sztring</span><span class="sxs-lookup"><span data-stu-id="476b7-151">string</span></span> | <span data-ttu-id="476b7-152">Y</span><span class="sxs-lookup"><span data-stu-id="476b7-152">Y</span></span>        | <span data-ttu-id="476b7-153">A két karakterből álló ISO alpha-2 országkód.</span><span class="sxs-lookup"><span data-stu-id="476b7-153">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="response-details"></a><span data-ttu-id="476b7-154">Válasz részletei</span><span class="sxs-lookup"><span data-stu-id="476b7-154">Response details</span></span>

<span data-ttu-id="476b7-155">A válasz a következő állapotüzenetek egyikét adja vissza:</span><span class="sxs-lookup"><span data-stu-id="476b7-155">The response will return one of the following status messages:</span></span>

| <span data-ttu-id="476b7-156">Állapot</span><span class="sxs-lookup"><span data-stu-id="476b7-156">Status</span></span>     | <span data-ttu-id="476b7-157">Leírás</span><span class="sxs-lookup"><span data-stu-id="476b7-157">Description</span></span> |    <span data-ttu-id="476b7-158">A visszaadott javasolt címek száma</span><span class="sxs-lookup"><span data-stu-id="476b7-158">Number of suggested addresses returned</span></span> |
|-------|---------------|-------------------|
|<span data-ttu-id="476b7-159">Ellenőrzött szállításra használható</span><span class="sxs-lookup"><span data-stu-id="476b7-159">Verified shippable</span></span> | <span data-ttu-id="476b7-160">A cím ellenőrizve van, és szállítható a címre.</span><span class="sxs-lookup"><span data-stu-id="476b7-160">Address is verified and can be shipped to.</span></span> | <span data-ttu-id="476b7-161">Egyirányú</span><span class="sxs-lookup"><span data-stu-id="476b7-161">Single</span></span> |
|<span data-ttu-id="476b7-162">Ellenőrzött</span><span class="sxs-lookup"><span data-stu-id="476b7-162">Verified</span></span> | <span data-ttu-id="476b7-163">A cím ellenőrizve van.</span><span class="sxs-lookup"><span data-stu-id="476b7-163">Address is verified.</span></span> | <span data-ttu-id="476b7-164">Egyirányú</span><span class="sxs-lookup"><span data-stu-id="476b7-164">Single</span></span> |
|<span data-ttu-id="476b7-165">Beavatkozás szükséges</span><span class="sxs-lookup"><span data-stu-id="476b7-165">Interaction required</span></span> | <span data-ttu-id="476b7-166">A javasolt cím jelentős mértékben módosult, és felhasználói megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="476b7-166">Suggested address has been changed significantly and needs user confirmation.</span></span> | <span data-ttu-id="476b7-167">Egyirányú</span><span class="sxs-lookup"><span data-stu-id="476b7-167">Single</span></span> |
|<span data-ttu-id="476b7-168">Utca részleges</span><span class="sxs-lookup"><span data-stu-id="476b7-168">Street partial</span></span> | <span data-ttu-id="476b7-169">A címben megadott utca részleges, és további információra van szüksége.</span><span class="sxs-lookup"><span data-stu-id="476b7-169">The given street in the address is partial and needs more info.</span></span> | <span data-ttu-id="476b7-170">Többszörös – legfeljebb három</span><span class="sxs-lookup"><span data-stu-id="476b7-170">Multiple—maximum of three</span></span> |
|<span data-ttu-id="476b7-171">Részleges helyszín</span><span class="sxs-lookup"><span data-stu-id="476b7-171">Premises partial</span></span> | <span data-ttu-id="476b7-172">Az adott helyszín (épületszám, csomagszám stb.) részleges, és további információra van szüksége.</span><span class="sxs-lookup"><span data-stu-id="476b7-172">The given premises (building number, suite number, and others) are partial and need more info.</span></span> | <span data-ttu-id="476b7-173">Többszörös – legfeljebb három</span><span class="sxs-lookup"><span data-stu-id="476b7-173">Multiple—maximum of three</span></span> |
|<span data-ttu-id="476b7-174">Többszörös</span><span class="sxs-lookup"><span data-stu-id="476b7-174">Multiple</span></span> | <span data-ttu-id="476b7-175">Több mező is részleges a címben (beleértve az utca részleges és a helyszíni részleges mezőket is).</span><span class="sxs-lookup"><span data-stu-id="476b7-175">There are multiple fields that are partial in the address (potentially also including street partial and premises partial).</span></span> | <span data-ttu-id="476b7-176">Többszörös – legfeljebb három</span><span class="sxs-lookup"><span data-stu-id="476b7-176">Multiple—maximum of three</span></span> |
|<span data-ttu-id="476b7-177">None</span><span class="sxs-lookup"><span data-stu-id="476b7-177">None</span></span> | <span data-ttu-id="476b7-178">A cím helytelen.</span><span class="sxs-lookup"><span data-stu-id="476b7-178">Address is incorrect.</span></span> | <span data-ttu-id="476b7-179">None</span><span class="sxs-lookup"><span data-stu-id="476b7-179">None</span></span> |
|<span data-ttu-id="476b7-180">Nincs ellenőrizve.</span><span class="sxs-lookup"><span data-stu-id="476b7-180">Not validated</span></span> | <span data-ttu-id="476b7-181">A cím nem lett elküldve az érvényesítési folyamaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="476b7-181">Address was not able to be sent through the validation process.</span></span> | <span data-ttu-id="476b7-182">None</span><span class="sxs-lookup"><span data-stu-id="476b7-182">None</span></span> |

### <a name="request-example"></a><span data-ttu-id="476b7-183">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="476b7-183">Request example</span></span>

```http
# "VerifiedShippable" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
Host: api.partnercenter.microsoft.com
Content-Length: 137
X-Locale: en-US

{
    "AddressLine1": "1 Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}

# "StreetPartial" Request Example

POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Accept: application/json
Content-Type: application/json
Authorization: Bearer <token>
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
Host: api.partnercenter.microsoft.com
Content-Length: 135
X-Locale: en-US

{
    "AddressLine1": "Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="476b7-184">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="476b7-184">REST response</span></span>

<span data-ttu-id="476b7-185">Sikeres művelet esetén a metódus egy **AddressValidationResponse** objektumot ad vissza a válasz törzsében, **http 200-as** állapotkóddal.</span><span class="sxs-lookup"><span data-stu-id="476b7-185">If successful, the method returns an **AddressValidationResponse** object in the response body, with a **HTTP 200** status code.</span></span> <span data-ttu-id="476b7-186">Erre mutat példát az alábbi ábra.</span><span class="sxs-lookup"><span data-stu-id="476b7-186">An example is shown below.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="476b7-187">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="476b7-187">Response success and error codes</span></span>

<span data-ttu-id="476b7-188">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="476b7-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="476b7-189">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="476b7-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="476b7-190">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="476b7-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="476b7-191">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="476b7-191">Response example</span></span>

```http
# "VerifiedShippable" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:19:19 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 29624f3c-90cb-4d34-a7e9-bd2de6d35218
MS-RequestId: eb55c2b8-6f4b-4b44-9557-f76df624b8c0
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-8300"
        }
    ],
    "status": "VerifiedShippable"
}

# "StreetPartial" Response Example

HTTP/1.1 200 OK
Date: Mon, 17 May 2021 23:34:08 GMT
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 2c95c9bc-fdfb-4c6a-84f4-57c9b0826b43
MS-RequestId: ee6cf74c-3ab5-48d6-9269-4a4b75bd59dc
X-Locale: en-US
 
{
    "originalAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "Microsoft Way",
        "postalCode": "98052"
    },
    "suggestedAddresses": [
        {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "1 Microsoft Way",
            "postalCode": "98052-6399"
        }
    ],
    "status": "StreetPartial",
    "validationMessage": "Address field invalid for property: 'Region', 'PostalCode', 'City'"
}
```
