---
title: Szervezet profiljának lekérése
description: Beolvas egy objektumot, amely a partner szervezeti profilját jelképezi.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 132a1e0efa3efea69d4bf649e55b412e300b0685
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768452"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="732a0-103">Szervezet profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="732a0-103">Get an organization profile</span></span>

<span data-ttu-id="732a0-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="732a0-104">**Applies To**</span></span>

- <span data-ttu-id="732a0-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="732a0-105">Partner Center</span></span>
- <span data-ttu-id="732a0-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="732a0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="732a0-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="732a0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="732a0-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="732a0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="732a0-109">Beolvas egy objektumot, amely a partner szervezeti profilját jelképezi.</span><span class="sxs-lookup"><span data-stu-id="732a0-109">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="732a0-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="732a0-110">Prerequisites</span></span>

- <span data-ttu-id="732a0-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="732a0-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="732a0-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="732a0-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="732a0-113">C\#</span><span class="sxs-lookup"><span data-stu-id="732a0-113">C\#</span></span>

<span data-ttu-id="732a0-114">A szervezeti profil beszerzéséhez használja a **IAggregatePartner. Profiles** gyűjteményt, és hívja meg a **OrganizationProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="732a0-114">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="732a0-115">Végül hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="732a0-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="732a0-116">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="732a0-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="732a0-117">**Projekt**: PartnerCenterSDK. FeaturesSamples **osztály**: GetOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="732a0-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="732a0-118">Java</span><span class="sxs-lookup"><span data-stu-id="732a0-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="732a0-119">A szervezeti profil beszerzéséhez használja a **IAggregatePartner. getProfiles** függvényt, és hívja meg a **getOrganizationProfile** függvényt.</span><span class="sxs-lookup"><span data-stu-id="732a0-119">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="732a0-120">Végül hívja meg a **Get ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="732a0-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="732a0-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="732a0-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="732a0-122">A szervezet profiljának beszerzéséhez hajtsa végre a [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="732a0-122">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="732a0-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="732a0-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="732a0-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="732a0-124">Request syntax</span></span>

| <span data-ttu-id="732a0-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="732a0-125">Method</span></span>  | <span data-ttu-id="732a0-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="732a0-126">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="732a0-127">**GET**</span><span class="sxs-lookup"><span data-stu-id="732a0-127">**GET**</span></span> | <span data-ttu-id="732a0-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Organization http/1.1</span><span class="sxs-lookup"><span data-stu-id="732a0-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="732a0-129">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="732a0-129">Request headers</span></span>

<span data-ttu-id="732a0-130">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="732a0-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="732a0-131">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="732a0-131">Request body</span></span>

<span data-ttu-id="732a0-132">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="732a0-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="732a0-133">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="732a0-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="732a0-134">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="732a0-134">REST response</span></span>

<span data-ttu-id="732a0-135">Ha ez sikeres, ez a metódus egy **OrganizationProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="732a0-135">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="732a0-136">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="732a0-136">Response success and error codes</span></span>

<span data-ttu-id="732a0-137">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="732a0-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="732a0-138">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="732a0-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="732a0-139">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="732a0-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="732a0-140">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="732a0-140">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
Date: Tue, 22 Mar 2016 17:11:06 GMT

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
