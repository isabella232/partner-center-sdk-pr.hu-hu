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
# <a name="validate-an-address"></a>Cím ellenőrzése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

Cím ellenőrzése a címérvényesítési API-val.

A címérvényesítési API csak az ügyfélprofilok frissítésének előzetes érvényesítéséhez használható. Használja annak tudatában, hogy ha az ország az Egyesült Államok, Kanada, Kína vagy Mexikó, akkor az állam mező az adott ország érvényes államlistával lesz ellenőrizve. Az összes többi országban ez a teszt nem történik meg, és az API csak azt ellenőrzi, hogy az állam érvényes sztring-e.

## <a name="prerequisites"></a>Előfeltételek

A hitelesítéssel Partnerközpont [hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja az önálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.

## <a name="c"></a>C\#

A cím érvényesítéséhez először példányosítenie kell egy új **Cím** objektumot, és ki kell feltöltenie a címet az ellenőrzéshez. Ezután az **IAggregatePartner.Validations** tulajdonságból olvassa be az Ellenőrzési műveletek felületét, és hívja meg az **IsAddressValid** metódust a címobjektummal. 

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

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                 |
|----------|-----------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/validations/address HTTP/1.1 |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Ez a táblázat a kérelem törzsében szükséges tulajdonságokat ismerteti.

| Név         | Típus   | Kötelező | Leírás                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | sztring | Y        | A cím első sorában.                             |
| addressline2 | sztring | N        | A cím második sorában. Ez a tulajdonság nem kötelező. |
| city         | sztring | Y        | A város.                                                  |
| állapot        | sztring | Y        | Az állapot.                                                 |
| irányítószám   | sztring | Y        | Az irányítószám.                                           |
| ország      | sztring | Y        | A két karakterből álló ISO alpha-2 országkód.                |

### <a name="response-details"></a>Válasz részletei

A válasz a következő állapotüzenetek egyikét adja vissza:

| Állapot     | Leírás |    A visszaadott javasolt címek száma |
|-------|---------------|-------------------|
|Ellenőrzött szállításra használható | A cím ellenőrizve van, és szállítható a címre. | Egyirányú |
|Ellenőrzött | A cím ellenőrizve van. | Egyirányú |
|Beavatkozás szükséges | A javasolt cím jelentős mértékben módosult, és felhasználói megerősítést kér. | Egyirányú |
|Utca részleges | A címben megadott utca részleges, és további információra van szüksége. | Többszörös – legfeljebb három |
|Részleges helyszín | Az adott helyszín (épületszám, csomagszám stb.) részleges, és további információra van szüksége. | Többszörös – legfeljebb három |
|Többszörös | Több mező is részleges a címben (beleértve az utca részleges és a helyszíni részleges mezőket is). | Többszörös – legfeljebb három |
|None | A cím helytelen. | None |
|Nincs ellenőrizve. | A cím nem lett elküldve az érvényesítési folyamaton keresztül. | None |

### <a name="request-example"></a>Példa kérésre

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

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén a metódus egy **AddressValidationResponse** objektumot ad vissza a válasz törzsében, **http 200-as** állapotkóddal. Erre mutat példát az alábbi ábra.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelen állapotot, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

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
