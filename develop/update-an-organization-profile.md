---
title: Szervezeti profil frissítése
description: Egy szervezet számlázási profiljának frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ccf938fff285704f54d4717b2678e1419d857d8d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767871"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="fc0c1-103">Szervezeti profil frissítése</span><span class="sxs-lookup"><span data-stu-id="fc0c1-103">Update an organization profile</span></span>

<span data-ttu-id="fc0c1-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="fc0c1-104">**Applies To**</span></span>

- <span data-ttu-id="fc0c1-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="fc0c1-105">Partner Center</span></span>
- <span data-ttu-id="fc0c1-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="fc0c1-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="fc0c1-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="fc0c1-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="fc0c1-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="fc0c1-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fc0c1-109">A partner számlázási profiljának frissítése.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-109">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc0c1-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fc0c1-110">Prerequisites</span></span>

- <span data-ttu-id="fc0c1-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc0c1-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="fc0c1-113">C\#</span><span class="sxs-lookup"><span data-stu-id="fc0c1-113">C\#</span></span>

<span data-ttu-id="fc0c1-114">A szervezeti profil frissítéséhez kérje le a profilt, és végezze el a szükséges módosításokat.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-114">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="fc0c1-115">Ezután használja a **IAggregatePartner. Profiles** gyűjteményt, és hívja meg a **OrganizationProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-115">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="fc0c1-116">Végül hívja meg a **Update ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="fc0c1-117">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fc0c1-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fc0c1-118">**Projekt**: PartnerCenterSDK. FeaturesSamples **osztály**: UpdateOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="fc0c1-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc0c1-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="fc0c1-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc0c1-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fc0c1-120">Request syntax</span></span>

| <span data-ttu-id="fc0c1-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="fc0c1-121">Method</span></span>  | <span data-ttu-id="fc0c1-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="fc0c1-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="fc0c1-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="fc0c1-123">**PUT**</span></span> | <span data-ttu-id="fc0c1-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Organization http/1.1</span><span class="sxs-lookup"><span data-stu-id="fc0c1-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fc0c1-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="fc0c1-125">Request headers</span></span>

<span data-ttu-id="fc0c1-126">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fc0c1-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fc0c1-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="fc0c1-127">Request body</span></span>

<span data-ttu-id="fc0c1-128">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fc0c1-129">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="fc0c1-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="fc0c1-130">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="fc0c1-130">REST response</span></span>

<span data-ttu-id="fc0c1-131">Ha ez sikeres, ez a metódus egy **OrganizationProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc0c1-132">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fc0c1-132">Response success and error codes</span></span>

<span data-ttu-id="fc0c1-133">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc0c1-134">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="fc0c1-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc0c1-135">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fc0c1-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fc0c1-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="fc0c1-136">Response example</span></span>

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
