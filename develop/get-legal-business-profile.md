---
title: A partner hivatalos vállalkozási profiljának lekérése
description: Ismerje meg, hogyan használhatja az API-kat a jogi üzleti profil beszerzéséhez.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1d488c8deb9f01110e92327035ce0c3c023fcb46
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500022"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="d6d76-103">A partner hivatalos vállalkozási profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="d6d76-103">Get the partner legal business profile</span></span>

<span data-ttu-id="d6d76-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="d6d76-104">**Applies To**</span></span>

- <span data-ttu-id="d6d76-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d6d76-105">Partner Center</span></span>
- <span data-ttu-id="d6d76-106">A 21Vianet által üzemeltetett Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d6d76-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d6d76-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d6d76-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d6d76-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="d6d76-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d6d76-109">Partner jogi üzleti profiljának beszerzése.</span><span class="sxs-lookup"><span data-stu-id="d6d76-109">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6d76-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d6d76-110">Prerequisites</span></span>

- <span data-ttu-id="d6d76-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="d6d76-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d6d76-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="d6d76-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d6d76-113">C\#</span><span class="sxs-lookup"><span data-stu-id="d6d76-113">C\#</span></span>

<span data-ttu-id="d6d76-114">A partner jogi üzleti profil beszerzéséhez először a **IAggregatePartner. Profiles** tulajdonságból kap egy felületet a partneri profil műveleteinek gyűjteményéhez.</span><span class="sxs-lookup"><span data-stu-id="d6d76-114">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="d6d76-115">Ezután a **LegalBusinessProfile** tulajdonság értékének lekérésével kérjen le egy felületet a jogi üzleti profil műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="d6d76-115">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="d6d76-116">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) metódust a profil lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="d6d76-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="d6d76-117">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d6d76-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d6d76-118">**Projekt**: partner Center SDK Samples **osztály**: GetLegalBusinessProfile. cs</span><span class="sxs-lookup"><span data-stu-id="d6d76-118">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d6d76-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="d6d76-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d6d76-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d6d76-120">Request syntax</span></span>

| <span data-ttu-id="d6d76-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="d6d76-121">Method</span></span>  | <span data-ttu-id="d6d76-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d6d76-122">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="d6d76-123">**GET**</span><span class="sxs-lookup"><span data-stu-id="d6d76-123">**GET**</span></span> | <span data-ttu-id="d6d76-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="d6d76-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d6d76-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d6d76-125">Request headers</span></span>

<span data-ttu-id="d6d76-126">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d6d76-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d6d76-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d6d76-127">Request body</span></span>

<span data-ttu-id="d6d76-128">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d6d76-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d6d76-129">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d6d76-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness?vettingVersion=Current HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d6d76-130">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d6d76-130">REST response</span></span>

<span data-ttu-id="d6d76-131">Ha ez sikeres, ez a metódus egy **LegalBusinessProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="d6d76-131">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d6d76-132">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d6d76-132">Response success and error codes</span></span>

<span data-ttu-id="d6d76-133">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="d6d76-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d6d76-134">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="d6d76-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d6d76-135">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="d6d76-135">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d6d76-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d6d76-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1151
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CV: MEgCpJUoGUeXG+4a.0
MS-ServerId: 030011719
Date: Tue, 21 Mar 2017 17:29:52 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550100"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550100"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
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
