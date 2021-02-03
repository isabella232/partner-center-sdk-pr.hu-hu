---
title: Cím ellenőrzése
description: Címek érvényesítése a címek érvényesítésére szolgáló API használatával.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 22d5faec2fdab4907067bb01cb74e110032dea9a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767828"
---
# <a name="validate-an-address"></a><span data-ttu-id="5a3d2-103">Cím ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="5a3d2-103">Validate an address</span></span>

<span data-ttu-id="5a3d2-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="5a3d2-104">**Applies To**</span></span>

- <span data-ttu-id="5a3d2-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5a3d2-105">Partner Center</span></span>
- <span data-ttu-id="5a3d2-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="5a3d2-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5a3d2-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5a3d2-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5a3d2-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5a3d2-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5a3d2-109">Címek érvényesítése a címek érvényesítésére szolgáló API használatával.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-109">How to validate an address using the address validation API.</span></span>

<span data-ttu-id="5a3d2-110">A címek érvényesítésére szolgáló API-t csak az ügyfél-profil frissítéseinek előzetes érvényesítéséhez kell használni.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-110">The address validation API should only be used for pre-validation of customer profile updates.</span></span> <span data-ttu-id="5a3d2-111">Azzal a feltétellel, hogy ha az ország a Egyesült Államok, Kanadában, Kínában vagy Mexikóban található, a State (állam) mezőt a rendszer érvényesíti az adott országban érvényes állapotok listájával.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-111">Use it with the understanding that if the country is the United States, Canada, China, or Mexico, the state field is validated against a list of valid states for the respective country.</span></span> <span data-ttu-id="5a3d2-112">Az összes többi országban ez a teszt nem történik meg, és az API csak azt ellenőrzi, hogy az állapot érvényes karakterlánc-e.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-112">In all other countries, this test does not occur, and the API only checks that the state is a valid string.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a3d2-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5a3d2-113">Prerequisites</span></span>

<span data-ttu-id="5a3d2-114">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5a3d2-115">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="5a3d2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="5a3d2-116">C\#</span></span>

<span data-ttu-id="5a3d2-117">A címek érvényesítéséhez először egy új **címlistát** kell létrehoznia, és azt a következő címen kell feltöltenie: Validate.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-117">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="5a3d2-118">Ezután kérjen le egy illesztőfelületet a **IAggregatePartner. valids** tulajdonságból származó **érvényesítési** műveletekre, és hívja meg a **IsAddressValid** metódust a címe objektummal.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-118">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.Validations** property, and call the **IsAddressValid** method with the address object.</span></span>

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

## <a name="java"></a><span data-ttu-id="5a3d2-119">Java</span><span class="sxs-lookup"><span data-stu-id="5a3d2-119">Java</span></span>

<span data-ttu-id="5a3d2-120">A címek érvényesítéséhez először egy új **címlistát** kell létrehoznia, és azt a következő címen kell feltöltenie: Validate.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-120">To validate an address, first instantiate a new **Address** object and populate it with the address to validate.</span></span> <span data-ttu-id="5a3d2-121">Ezután kérjen le egy illesztőfelületet a **IAggregatePartner. getValidations** függvénytől az **érvényesítési** műveletekhez, és hívja meg a **isAddressValid** metódust a címe objektummal.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-121">Then, retrieve an interface to **Validations** operations from the **IAggregatePartner.getValidations** function, and call the **isAddressValid** method with the address object.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="5a3d2-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a3d2-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="5a3d2-123">A címek ellenőrzéséhez hajtsa végre a [**test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) paramétert a megadott címekkel.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-123">To validate an address, execute the [**Test-PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) with the address parameters populated.</span></span>

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="rest-request"></a><span data-ttu-id="5a3d2-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5a3d2-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5a3d2-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5a3d2-125">Request syntax</span></span>

| <span data-ttu-id="5a3d2-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="5a3d2-126">Method</span></span>   | <span data-ttu-id="5a3d2-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5a3d2-127">Request URI</span></span>                                                                 |
|----------|-----------------------------------------------------------------------------|
| <span data-ttu-id="5a3d2-128">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="5a3d2-128">**POST**</span></span> | <span data-ttu-id="5a3d2-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/Address http/1.1</span><span class="sxs-lookup"><span data-stu-id="5a3d2-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5a3d2-130">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5a3d2-130">Request headers</span></span>

<span data-ttu-id="5a3d2-131">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5a3d2-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5a3d2-132">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5a3d2-132">Request body</span></span>

<span data-ttu-id="5a3d2-133">Ez a táblázat a kérelem törzsében szereplő kötelező tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-133">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="5a3d2-134">Név</span><span class="sxs-lookup"><span data-stu-id="5a3d2-134">Name</span></span>         | <span data-ttu-id="5a3d2-135">Típus</span><span class="sxs-lookup"><span data-stu-id="5a3d2-135">Type</span></span>   | <span data-ttu-id="5a3d2-136">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5a3d2-136">Required</span></span> | <span data-ttu-id="5a3d2-137">Leírás</span><span class="sxs-lookup"><span data-stu-id="5a3d2-137">Description</span></span>                                                |
|--------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="5a3d2-138">addressline1</span><span class="sxs-lookup"><span data-stu-id="5a3d2-138">addressline1</span></span> | <span data-ttu-id="5a3d2-139">sztring</span><span class="sxs-lookup"><span data-stu-id="5a3d2-139">string</span></span> | <span data-ttu-id="5a3d2-140">Y</span><span class="sxs-lookup"><span data-stu-id="5a3d2-140">Y</span></span>        | <span data-ttu-id="5a3d2-141">A címe első sora.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-141">The first line of the address.</span></span>                             |
| <span data-ttu-id="5a3d2-142">addressline2</span><span class="sxs-lookup"><span data-stu-id="5a3d2-142">addressline2</span></span> | <span data-ttu-id="5a3d2-143">sztring</span><span class="sxs-lookup"><span data-stu-id="5a3d2-143">string</span></span> | <span data-ttu-id="5a3d2-144">N</span><span class="sxs-lookup"><span data-stu-id="5a3d2-144">N</span></span>        | <span data-ttu-id="5a3d2-145">A címe második sora.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-145">The second line of the address.</span></span> <span data-ttu-id="5a3d2-146">Ez a tulajdonság nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-146">This property is optional.</span></span> |
| <span data-ttu-id="5a3d2-147">city</span><span class="sxs-lookup"><span data-stu-id="5a3d2-147">city</span></span>         | <span data-ttu-id="5a3d2-148">sztring</span><span class="sxs-lookup"><span data-stu-id="5a3d2-148">string</span></span> | <span data-ttu-id="5a3d2-149">Y</span><span class="sxs-lookup"><span data-stu-id="5a3d2-149">Y</span></span>        | <span data-ttu-id="5a3d2-150">A város.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-150">The city.</span></span>                                                  |
| <span data-ttu-id="5a3d2-151">állapot</span><span class="sxs-lookup"><span data-stu-id="5a3d2-151">state</span></span>        | <span data-ttu-id="5a3d2-152">sztring</span><span class="sxs-lookup"><span data-stu-id="5a3d2-152">string</span></span> | <span data-ttu-id="5a3d2-153">Y</span><span class="sxs-lookup"><span data-stu-id="5a3d2-153">Y</span></span>        | <span data-ttu-id="5a3d2-154">Az állapot.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-154">The state.</span></span>                                                 |
| <span data-ttu-id="5a3d2-155">Irányítószám</span><span class="sxs-lookup"><span data-stu-id="5a3d2-155">postalcode</span></span>   | <span data-ttu-id="5a3d2-156">sztring</span><span class="sxs-lookup"><span data-stu-id="5a3d2-156">string</span></span> | <span data-ttu-id="5a3d2-157">Y</span><span class="sxs-lookup"><span data-stu-id="5a3d2-157">Y</span></span>        | <span data-ttu-id="5a3d2-158">A postai irányítószám.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-158">The postal code.</span></span>                                           |
| <span data-ttu-id="5a3d2-159">ország</span><span class="sxs-lookup"><span data-stu-id="5a3d2-159">country</span></span>      | <span data-ttu-id="5a3d2-160">sztring</span><span class="sxs-lookup"><span data-stu-id="5a3d2-160">string</span></span> | <span data-ttu-id="5a3d2-161">Y</span><span class="sxs-lookup"><span data-stu-id="5a3d2-161">Y</span></span>        | <span data-ttu-id="5a3d2-162">A két karakterből álló ISO Alpha-2 országkód.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-162">The two-character ISO alpha-2 country code.</span></span>                |

### <a name="request-example"></a><span data-ttu-id="5a3d2-163">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5a3d2-163">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5a3d2-164">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5a3d2-164">REST response</span></span>

<span data-ttu-id="5a3d2-165">Ha a művelet sikeres, a metódus a 200 állapotkódot adja vissza, amint az alább látható a válasz-érvényesítés sikeres példája.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-165">If successful, the method returns a status code 200 as demonstrated in the Response - validation succeeded example shown below.</span></span>

<span data-ttu-id="5a3d2-166">Ha a kérelem meghiúsul, a metódus a 400 állapotkódot adja vissza, amint az alább látható válasz-érvényesítés sikertelen.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-166">If the request fails, the method returns a status code 400 as demonstrated in the Response - validation failed example shown below.</span></span> <span data-ttu-id="5a3d2-167">A válasz törzse egy JSON-adattartalommal rendelkezik, amely további információkat tartalmaz a hibáról.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-167">The response body contains a JSON payload with additional information about the error.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5a3d2-168">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5a3d2-168">Response success and error codes</span></span>

<span data-ttu-id="5a3d2-169">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5a3d2-170">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5a3d2-171">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="5a3d2-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response---validation-succeeded-example"></a><span data-ttu-id="5a3d2-172">A válasz érvényesítése sikeres példa</span><span class="sxs-lookup"><span data-stu-id="5a3d2-172">Response - validation succeeded example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

### <a name="response---validation-failed-example"></a><span data-ttu-id="5a3d2-173">Válasz – sikertelen érvényesítés – példa</span><span class="sxs-lookup"><span data-stu-id="5a3d2-173">Response - validation failed example</span></span>

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
