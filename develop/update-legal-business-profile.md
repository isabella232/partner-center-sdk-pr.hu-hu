---
title: A partner hivatalos vállalkozási profiljának frissítése
description: A partner jogi profiljának frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: cb9f5815e0019c5e9b648dfd865e9752f0afdf05
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530327"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="4ba43-103">A partner hivatalos vállalkozási profiljának frissítése</span><span class="sxs-lookup"><span data-stu-id="4ba43-103">Update the partner legal business profile</span></span>

<span data-ttu-id="4ba43-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4ba43-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4ba43-105">A partner jogi profiljának frissítése.</span><span class="sxs-lookup"><span data-stu-id="4ba43-105">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ba43-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4ba43-106">Prerequisites</span></span>

- <span data-ttu-id="4ba43-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4ba43-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4ba43-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="4ba43-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="4ba43-109">C\#</span><span class="sxs-lookup"><span data-stu-id="4ba43-109">C\#</span></span>

<span data-ttu-id="4ba43-110">A partner jogi üzleti profiljának frissítéséhez először példányosítenie kell egy **LegalBusinessProfile** objektumot, és fel kell töltve a meglévő profillal.</span><span class="sxs-lookup"><span data-stu-id="4ba43-110">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="4ba43-111">További információ: [Partner jogi profiljának lekérte.](get-legal-business-profile.md)</span><span class="sxs-lookup"><span data-stu-id="4ba43-111">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="4ba43-112">Ezután frissítse a módosítani szükséges tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="4ba43-112">Then, update the properties that you need to change.</span></span> <span data-ttu-id="4ba43-113">Az alábbi példakód a cím és az elsődleges kapcsolattartási telefonszámok megváltoztatását mutatja be.</span><span class="sxs-lookup"><span data-stu-id="4ba43-113">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="4ba43-114">Ezután szerezze be a partnerprofil műveleti gyűjteményének interfészét az **IAggregatePartner.Profiles tulajdonságból.**</span><span class="sxs-lookup"><span data-stu-id="4ba43-114">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="4ba43-115">Ezután lekéri a **LegalBusinessProfile** tulajdonság értékét, hogy lekérje a jogi üzletiprofil-műveletek felületét.</span><span class="sxs-lookup"><span data-stu-id="4ba43-115">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="4ba43-116">Végül hívja meg az [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) vagy [**az UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) metódust a módosított objektummal a profil frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4ba43-116">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="4ba43-117">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="4ba43-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4ba43-118">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4ba43-118">Request syntax</span></span>

| <span data-ttu-id="4ba43-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="4ba43-119">Method</span></span>  | <span data-ttu-id="4ba43-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4ba43-120">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="4ba43-121">**PUT**</span><span class="sxs-lookup"><span data-stu-id="4ba43-121">**PUT**</span></span> | <span data-ttu-id="4ba43-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4ba43-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4ba43-123">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4ba43-123">Request headers</span></span>

<span data-ttu-id="4ba43-124">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4ba43-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4ba43-125">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4ba43-125">Request body</span></span>

<span data-ttu-id="4ba43-126">A jogi üzleti profil erőforrása.</span><span class="sxs-lookup"><span data-stu-id="4ba43-126">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="4ba43-127">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4ba43-127">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4ba43-128">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4ba43-128">REST response</span></span>

<span data-ttu-id="4ba43-129">Ha a művelet sikeres, a válasz törzse tartalmazza a **frissített LegalBusinessProfile adatokat**</span><span class="sxs-lookup"><span data-stu-id="4ba43-129">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4ba43-130">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4ba43-130">Response success and error codes</span></span>

<span data-ttu-id="4ba43-131">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="4ba43-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4ba43-132">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="4ba43-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4ba43-133">A teljes listát a következő Partnerközpont [tartalmazza:](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4ba43-133">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4ba43-134">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4ba43-134">Response example</span></span>

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
