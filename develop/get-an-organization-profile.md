---
title: Szervezet profiljának lekérése
description: Lekért egy objektumot, amely a partner szervezeti profilját képviseli.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 1c7272761612e573388d4facea1a78808a5bad52
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760555"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="aa25a-103">Szervezet profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="aa25a-103">Get an organization profile</span></span>

<span data-ttu-id="aa25a-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="aa25a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="aa25a-105">Lekért egy objektumot, amely a partner szervezeti profilját képviseli.</span><span class="sxs-lookup"><span data-stu-id="aa25a-105">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa25a-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="aa25a-106">Prerequisites</span></span>

- <span data-ttu-id="aa25a-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="aa25a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="aa25a-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="aa25a-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="aa25a-109">C\#</span><span class="sxs-lookup"><span data-stu-id="aa25a-109">C\#</span></span>

<span data-ttu-id="aa25a-110">A szervezeti profil lehíváshoz használja az **IAggregatePartner.Profiles** gyűjteményt, és hívja meg az **OrganizationProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="aa25a-110">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="aa25a-111">Végül hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="aa25a-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="aa25a-112">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="aa25a-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="aa25a-113">**Project:** PartnerCenterSDK.FeaturesSamples **osztály:** GetOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="aa25a-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="aa25a-114">Java</span><span class="sxs-lookup"><span data-stu-id="aa25a-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="aa25a-115">A szervezeti profil lehíváshoz használja az **IAggregatePartner.getProfiles** függvényt, és hívja meg a **getOrganizationProfile** függvényt.</span><span class="sxs-lookup"><span data-stu-id="aa25a-115">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="aa25a-116">Végül hívja meg a **get()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="aa25a-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="aa25a-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa25a-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="aa25a-118">A szervezeti profil lekért végrehajtásához hajtsa végre a [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="aa25a-118">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="aa25a-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="aa25a-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="aa25a-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="aa25a-120">Request syntax</span></span>

| <span data-ttu-id="aa25a-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="aa25a-121">Method</span></span>  | <span data-ttu-id="aa25a-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="aa25a-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="aa25a-123">**Kap**</span><span class="sxs-lookup"><span data-stu-id="aa25a-123">**GET**</span></span> | <span data-ttu-id="aa25a-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="aa25a-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="aa25a-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="aa25a-125">Request headers</span></span>

<span data-ttu-id="aa25a-126">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="aa25a-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="aa25a-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="aa25a-127">Request body</span></span>

<span data-ttu-id="aa25a-128">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="aa25a-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="aa25a-129">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="aa25a-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="aa25a-130">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="aa25a-130">REST response</span></span>

<span data-ttu-id="aa25a-131">Sikeres művelet esetén ez a metódus egy **OrganizationProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="aa25a-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="aa25a-132">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="aa25a-132">Response success and error codes</span></span>

<span data-ttu-id="aa25a-133">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="aa25a-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="aa25a-134">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="aa25a-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="aa25a-135">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="aa25a-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="aa25a-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="aa25a-136">Response example</span></span>

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
