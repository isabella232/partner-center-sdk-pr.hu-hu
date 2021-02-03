---
title: A partner hivatalos vállalkozási profiljának frissítése
description: A partner jogi üzleti profiljának frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 6c61b51ab0680e36daa99c11dc8e8c3506259d29
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768275"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="baa4b-103">A partner hivatalos vállalkozási profiljának frissítése</span><span class="sxs-lookup"><span data-stu-id="baa4b-103">Update the partner legal business profile</span></span>

<span data-ttu-id="baa4b-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="baa4b-104">**Applies To**</span></span>

- <span data-ttu-id="baa4b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="baa4b-105">Partner Center</span></span>
- <span data-ttu-id="baa4b-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="baa4b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="baa4b-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="baa4b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="baa4b-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="baa4b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="baa4b-109">A partner jogi üzleti profiljának frissítése.</span><span class="sxs-lookup"><span data-stu-id="baa4b-109">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baa4b-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="baa4b-110">Prerequisites</span></span>

- <span data-ttu-id="baa4b-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="baa4b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="baa4b-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="baa4b-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="baa4b-113">C\#</span><span class="sxs-lookup"><span data-stu-id="baa4b-113">C\#</span></span>

<span data-ttu-id="baa4b-114">A partner jogi üzleti profil frissítéséhez először hozza létre a **LegalBusinessProfile** objektumot, és töltse fel azt a meglévő profillal.</span><span class="sxs-lookup"><span data-stu-id="baa4b-114">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="baa4b-115">További információ: [a partner jogi üzleti profiljának beszerzése](get-legal-business-profile.md).</span><span class="sxs-lookup"><span data-stu-id="baa4b-115">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="baa4b-116">Ezután frissítse a módosítani kívánt tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="baa4b-116">Then, update the properties that you need to change.</span></span> <span data-ttu-id="baa4b-117">A következő kódrészlet szemlélteti a címek és az elsődleges névjegyek telefonszámának módosítását.</span><span class="sxs-lookup"><span data-stu-id="baa4b-117">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="baa4b-118">Ezután szerezzen be egy felületet a partner profiljának műveleti gyűjteményéből a **IAggregatePartner. Profiles** tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="baa4b-118">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="baa4b-119">Ezután a **LegalBusinessProfile** tulajdonság értékének lekérésével beolvashatja a jogi üzleti profil műveleteihez szükséges felületet.</span><span class="sxs-lookup"><span data-stu-id="baa4b-119">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="baa4b-120">Végül hívja meg az [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) vagy a [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) metódust a módosított objektummal a profil frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="baa4b-120">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="baa4b-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="baa4b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="baa4b-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="baa4b-122">Request syntax</span></span>

| <span data-ttu-id="baa4b-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="baa4b-123">Method</span></span>  | <span data-ttu-id="baa4b-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="baa4b-124">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="baa4b-125">**PUT**</span><span class="sxs-lookup"><span data-stu-id="baa4b-125">**PUT**</span></span> | <span data-ttu-id="baa4b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="baa4b-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="baa4b-127">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="baa4b-127">Request headers</span></span>

<span data-ttu-id="baa4b-128">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="baa4b-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="baa4b-129">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="baa4b-129">Request body</span></span>

<span data-ttu-id="baa4b-130">A jogi üzleti profil erőforrása.</span><span class="sxs-lookup"><span data-stu-id="baa4b-130">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="baa4b-131">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="baa4b-131">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 806
Expect: 100-continue

{
    "CompanyName": "Lucerne Publishing",
    "Address": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": "Gena",
        "LastName": "Soto",
        "PhoneNumber": "4255550110"
    },
    "PrimaryContact": {
        "FirstName": "Gena",
        "LastName": "Soto",
        "Email": "gena@lucernepublishing.com",
        "PhoneNumber": "4255550110"
    },
    "CompanyApproverAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": null,
        "LastName": null,
        "PhoneNumber": null
    },
    "CompanyApproverEmail": "gena@lucernepublishing.com",
    "VettingStatus": "authorized",
    "VettingSubStatus": "none",
    "Links": {
        "Self": {
            "Uri": "/profiles/legalbusiness",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "LegalBusinessProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="baa4b-132">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="baa4b-132">REST response</span></span>

<span data-ttu-id="baa4b-133">Ha a művelet sikeres, a válasz törzse tartalmazza a frissített **LegalBusinessProfile**</span><span class="sxs-lookup"><span data-stu-id="baa4b-133">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="baa4b-134">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="baa4b-134">Response success and error codes</span></span>

<span data-ttu-id="baa4b-135">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="baa4b-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="baa4b-136">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="baa4b-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="baa4b-137">A teljes listát a következő témakörben talál: [partner Center hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="baa4b-137">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="baa4b-138">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="baa4b-138">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1157
Content-Type: application/json; charset=utf-8
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CV: KZLU42qJ4EObO75q.0
MS-ServerId: 030020643
Date: Tue, 21 Mar 2017 22:03:15 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550110"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550110"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
