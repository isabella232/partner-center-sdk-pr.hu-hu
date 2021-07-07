---
title: Szervezeti profil frissítése
description: Frissíti egy szervezet számlázási profilját.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0ef736a722cde16f95ed6dfdbdab278c98fcf738
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530055"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="003c4-103">Szervezeti profil frissítése</span><span class="sxs-lookup"><span data-stu-id="003c4-103">Update an organization profile</span></span>

<span data-ttu-id="003c4-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="003c4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="003c4-105">Frissíti a partner számlázási profilját.</span><span class="sxs-lookup"><span data-stu-id="003c4-105">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="003c4-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="003c4-106">Prerequisites</span></span>

- <span data-ttu-id="003c4-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="003c4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="003c4-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="003c4-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="003c4-109">C\#</span><span class="sxs-lookup"><span data-stu-id="003c4-109">C\#</span></span>

<span data-ttu-id="003c4-110">A szervezeti profil frissítéséhez olvassa be a profilt, és tegye meg a szükséges módosításokat.</span><span class="sxs-lookup"><span data-stu-id="003c4-110">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="003c4-111">Ezután használja az **IAggregatePartner.Profiles** gyűjteményt, és hívja meg az **OrganizationProfile tulajdonságot.**</span><span class="sxs-lookup"><span data-stu-id="003c4-111">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="003c4-112">Végül hívja meg az **Update() metódust.**</span><span class="sxs-lookup"><span data-stu-id="003c4-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="003c4-113">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="003c4-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="003c4-114">**Project:** PartnerCenterSDK.FeaturesSamples **osztály:** UpdateOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="003c4-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="003c4-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="003c4-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="003c4-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="003c4-116">Request syntax</span></span>

| <span data-ttu-id="003c4-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="003c4-117">Method</span></span>  | <span data-ttu-id="003c4-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="003c4-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="003c4-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="003c4-119">**PUT**</span></span> | <span data-ttu-id="003c4-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="003c4-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="003c4-121">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="003c4-121">Request headers</span></span>

<span data-ttu-id="003c4-122">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="003c4-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="003c4-123">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="003c4-123">Request body</span></span>

<span data-ttu-id="003c4-124">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="003c4-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="003c4-125">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="003c4-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 624
Expect: 100-continue

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="003c4-126">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="003c4-126">REST response</span></span>

<span data-ttu-id="003c4-127">Sikeres művelet esetén ez a metódus egy **OrganizationProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="003c4-127">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="003c4-128">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="003c4-128">Response success and error codes</span></span>

<span data-ttu-id="003c4-129">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="003c4-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="003c4-130">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="003c4-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="003c4-131">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="003c4-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="003c4-132">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="003c4-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
Date: Mon, 21 Mar 2016 05:48:41 GMT

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "profileType":"OrganizationProfile",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```
