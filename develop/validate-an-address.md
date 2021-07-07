---
title: Cím ellenőrzése
description: Cím ellenőrzése a címérvényesítési API-val.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14d45977f3af6e8bba1b7cb7f969aa7c5bb671da
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529885"
---
# <a name="validate-an-address"></a><span data-ttu-id="3e0bb-103">Cím ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="3e0bb-103">Validate an address</span></span>

<span data-ttu-id="3e0bb-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3e0bb-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3e0bb-105">Cím ellenőrzése a címérvényesítési API-val.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-105">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="3e0bb-106">A címérvényesítési API csak az ügyfélprofilok frissítésének előzetes érvényesítéséhez használható.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-106">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="3e0bb-107">Használja annak tudatában, hogy ha az ország az Egyesült Államok, Kanada, Kína vagy Mexikó, akkor az állam mező az adott ország érvényes államlistával lesz ellenőrizve.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-107">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="3e0bb-108">Az összes többi országban ez a teszt nem történik meg, és az API csak azt ellenőrzi, hogy az állam érvényes sztring-e.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-108">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e0bb-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3e0bb-109">Prerequisites</span></span>

<span data-ttu-id="3e0bb-110">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3e0bb-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3e0bb-111">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="3e0bb-112">C\#</span><span class="sxs-lookup"><span data-stu-id="3e0bb-112">C\#</span></span>

<span data-ttu-id="3e0bb-113">Egy cím érvényesítéséhez először példányosítenie kell egy új **Cím** objektumot, és fel kell tölti azt az érvényesítenie kell a címmel.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-113">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="3e0bb-114">Ezután az **IAggregatePartner.Validations** tulajdonságból olvassa be az Ellenőrzési műveletek felületét, és hívja meg az **IsAddressValid** metódust a címobjektummal. </span><span class="sxs-lookup"><span data-stu-id="3e0bb-114">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

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
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";

    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);

    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

## <a name="java"></a><span data-ttu-id="3e0bb-115">Java</span><span class="sxs-lookup"><span data-stu-id="3e0bb-115">Java</span></span>

<span data-ttu-id="3e0bb-116">Egy cím érvényesítéséhez először példányosítenie kell egy új **Cím** objektumot, és fel kell tölti azt az érvényesítenie kell a címmel.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-116">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="3e0bb-117">Ezután az **IAggregatePartner.getValidations** függvényből szerezze be az Ellenőrzési műveletek felületét, és hívja meg az **isAddressValid** metódust a címobjektummal. </span><span class="sxs-lookup"><span data-stu-id="3e0bb-117">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");

    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

## <a name="powershell"></a><span data-ttu-id="3e0bb-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e0bb-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="3e0bb-119">Egy cím érvényesítéséhez futtasa le a [**Test-PartnerAddress paramétert**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) a megadott címparaméterekkel.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-119">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="3e0bb-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="3e0bb-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3e0bb-121">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="3e0bb-121">Request syntax</span></span>

| <span data-ttu-id="3e0bb-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="3e0bb-122">Method</span></span>   | <span data-ttu-id="3e0bb-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3e0bb-123">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="3e0bb-124">**Post**</span><span class="sxs-lookup"><span data-stu-id="3e0bb-124">**POST**</span></span> | <span data-ttu-id="3e0bb-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3e0bb-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3e0bb-126">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3e0bb-126">Request headers</span></span>

<span data-ttu-id="3e0bb-127">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3e0bb-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3e0bb-128">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="3e0bb-128">Request body</span></span>

<span data-ttu-id="3e0bb-129">Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-129">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="3e0bb-130">Név</span><span class="sxs-lookup"><span data-stu-id="3e0bb-130">Name</span></span>         | <span data-ttu-id="3e0bb-131">Típus</span><span class="sxs-lookup"><span data-stu-id="3e0bb-131">Type</span></span>   | <span data-ttu-id="3e0bb-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3e0bb-132">Required</span></span> | <span data-ttu-id="3e0bb-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="3e0bb-133">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="3e0bb-134">addressline1</span><span class="sxs-lookup"><span data-stu-id="3e0bb-134">addressline1</span></span> | <span data-ttu-id="3e0bb-135">sztring</span><span class="sxs-lookup"><span data-stu-id="3e0bb-135">string</span></span> | <span data-ttu-id="3e0bb-136">Y</span><span class="sxs-lookup"><span data-stu-id="3e0bb-136">Y</span></span>        | <span data-ttu-id="3e0bb-137">A cím első sorát.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-137">The first line of the address.</span></span>                             |
| <span data-ttu-id="3e0bb-138">addressline2</span><span class="sxs-lookup"><span data-stu-id="3e0bb-138">addressline2</span></span> | <span data-ttu-id="3e0bb-139">sztring</span><span class="sxs-lookup"><span data-stu-id="3e0bb-139">string</span></span> | <span data-ttu-id="3e0bb-140">N</span><span class="sxs-lookup"><span data-stu-id="3e0bb-140">N</span></span>        | <span data-ttu-id="3e0bb-141">A cím második sorában.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-141">The second line of the address.</span></span> <span data-ttu-id="3e0bb-142">Ez a tulajdonság nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-142">This property is optional.</span></span> |
| <span data-ttu-id="3e0bb-143">city</span><span class="sxs-lookup"><span data-stu-id="3e0bb-143">city</span></span>         | <span data-ttu-id="3e0bb-144">sztring</span><span class="sxs-lookup"><span data-stu-id="3e0bb-144">string</span></span> | <span data-ttu-id="3e0bb-145">Y</span><span class="sxs-lookup"><span data-stu-id="3e0bb-145">Y</span></span>        | <span data-ttu-id="3e0bb-146">A város.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-146">The city.</span></span>                                                  |
| <span data-ttu-id="3e0bb-147">állapot</span><span class="sxs-lookup"><span data-stu-id="3e0bb-147">state</span></span>        | <span data-ttu-id="3e0bb-148">sztring</span><span class="sxs-lookup"><span data-stu-id="3e0bb-148">string</span></span> | <span data-ttu-id="3e0bb-149">Y</span><span class="sxs-lookup"><span data-stu-id="3e0bb-149">Y</span></span>        | <span data-ttu-id="3e0bb-150">Az állapot.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-150">The state.</span></span>                                                 |
| <span data-ttu-id="3e0bb-151">irányítószám</span><span class="sxs-lookup"><span data-stu-id="3e0bb-151">postalcode</span></span>   | <span data-ttu-id="3e0bb-152">sztring</span><span class="sxs-lookup"><span data-stu-id="3e0bb-152">string</span></span> | <span data-ttu-id="3e0bb-153">Y</span><span class="sxs-lookup"><span data-stu-id="3e0bb-153">Y</span></span>        | <span data-ttu-id="3e0bb-154">Az irányítószám.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-154">The postal code.</span></span>                                           |
| <span data-ttu-id="3e0bb-155">ország</span><span class="sxs-lookup"><span data-stu-id="3e0bb-155">country</span></span>      | <span data-ttu-id="3e0bb-156">sztring</span><span class="sxs-lookup"><span data-stu-id="3e0bb-156">string</span></span> | <span data-ttu-id="3e0bb-157">Y</span><span class="sxs-lookup"><span data-stu-id="3e0bb-157">Y</span></span>        | <span data-ttu-id="3e0bb-158">A két karakterből álló ISO alpha-2 országkód.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-158">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="3e0bb-159">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="3e0bb-159">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    "AddressLine1": "One Microsoft Way",
    "City": "Redmond",
    "State": "WA",
    "PostalCode": "98052",
    "Country": "US"
}
```

## <a name="rest-response"></a><span data-ttu-id="3e0bb-160">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3e0bb-160">REST response</span></span>

<span data-ttu-id="3e0bb-161">Sikeres művelet esetén a metódus a 200-as állapotkódot adja vissza az alább látható Válasz – sikeres ellenőrzés példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-161">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="3e0bb-162">Ha a kérés meghiúsul, a metódus a 400-as állapotkódot adja vissza az alább látható Válasz – ellenőrzés sikertelen példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-162">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="3e0bb-163">A válasz törzse tartalmaz egy hasznos JSON-adatokat, amely további információkat tartalmaz a hibáról.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-163">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3e0bb-164">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3e0bb-164">Response success and error codes</span></span>

<span data-ttu-id="3e0bb-165">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3e0bb-166">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="3e0bb-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3e0bb-167">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3e0bb-167">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="3e0bb-168">Válasz – sikeres érvényesítés – példa</span><span class="sxs-lookup"><span data-stu-id="3e0bb-168">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="3e0bb-169">Válasz – sikertelen érvényesítés – példa</span><span class="sxs-lookup"><span data-stu-id="3e0bb-169">Response - validation failed example</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```
