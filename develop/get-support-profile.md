---
title: Támogatási profil lekérése
description: Egy felhasználó támogatási profilját jelképező objektum beolvasása.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b8b0fa533aaba74418985ea02cbb13bd722cede2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768412"
---
# <a name="get-support-profile"></a><span data-ttu-id="5d548-103">Támogatási profil lekérése</span><span class="sxs-lookup"><span data-stu-id="5d548-103">Get support profile</span></span>

<span data-ttu-id="5d548-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="5d548-104">**Applies To**</span></span>

- <span data-ttu-id="5d548-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5d548-105">Partner Center</span></span>
- <span data-ttu-id="5d548-106">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5d548-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5d548-107">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="5d548-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5d548-108">Egy felhasználó támogatási profilját jelképező objektum beolvasása.</span><span class="sxs-lookup"><span data-stu-id="5d548-108">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d548-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5d548-109">Prerequisites</span></span>

- <span data-ttu-id="5d548-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5d548-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5d548-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="5d548-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="5d548-112">C\#</span><span class="sxs-lookup"><span data-stu-id="5d548-112">C\#</span></span>

<span data-ttu-id="5d548-113">A támogatási profil beszerzéséhez használja a **IAggregatePartner. Profiles** gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="5d548-113">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="5d548-114">Hívja meg a [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) tulajdonságot, majd a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="5d548-114">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="5d548-115">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5d548-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5d548-116">**Projekt**: PartnerCenterSDK. FeaturesSamples **osztály**: GetSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="5d548-116">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5d548-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5d548-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5d548-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5d548-118">Request syntax</span></span>

| <span data-ttu-id="5d548-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="5d548-119">Method</span></span>  | <span data-ttu-id="5d548-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5d548-120">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="5d548-121">**GET**</span><span class="sxs-lookup"><span data-stu-id="5d548-121">**GET**</span></span> | <span data-ttu-id="5d548-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/support http/1.1</span><span class="sxs-lookup"><span data-stu-id="5d548-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5d548-123">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5d548-123">Request headers</span></span>

<span data-ttu-id="5d548-124">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5d548-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5d548-125">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="5d548-125">Request body</span></span>

<span data-ttu-id="5d548-126">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="5d548-126">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5d548-127">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5d548-127">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="5d548-128">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5d548-128">REST response</span></span>

<span data-ttu-id="5d548-129">Ha ez sikeres, ez a metódus egy **SupportProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="5d548-129">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5d548-130">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5d548-130">Response success and error codes</span></span>

<span data-ttu-id="5d548-131">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5d548-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5d548-132">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5d548-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5d548-133">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5d548-133">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5d548-134">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5d548-134">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```
