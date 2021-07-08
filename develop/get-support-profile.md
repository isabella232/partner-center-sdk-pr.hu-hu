---
title: Támogatási profil lekérése
description: Lekért egy objektumot, amely a felhasználó támogatási profilját képviseli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b112ccbbff731795c21f95845a08be9e9dfb6775
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548634"
---
# <a name="get-support-profile"></a><span data-ttu-id="ee0de-103">Támogatási profil lekérése</span><span class="sxs-lookup"><span data-stu-id="ee0de-103">Get support profile</span></span>

<span data-ttu-id="ee0de-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ee0de-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ee0de-105">Lekért egy objektumot, amely a felhasználó támogatási profilját képviseli.</span><span class="sxs-lookup"><span data-stu-id="ee0de-105">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee0de-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ee0de-106">Prerequisites</span></span>

- <span data-ttu-id="ee0de-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ee0de-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ee0de-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="ee0de-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="ee0de-109">C\#</span><span class="sxs-lookup"><span data-stu-id="ee0de-109">C\#</span></span>

<span data-ttu-id="ee0de-110">A támogatási profilhoz használja az **IAggregatePartner.Profiles gyűjteményt.**</span><span class="sxs-lookup"><span data-stu-id="ee0de-110">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="ee0de-111">Hívja meg [**a SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) tulajdonságot, majd a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="ee0de-111">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="ee0de-112">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ee0de-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ee0de-113">**Project:** PartnerCenterSDK.FeaturesSamples **osztály:** GetSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="ee0de-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ee0de-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ee0de-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ee0de-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ee0de-115">Request syntax</span></span>

| <span data-ttu-id="ee0de-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="ee0de-116">Method</span></span>  | <span data-ttu-id="ee0de-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ee0de-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="ee0de-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="ee0de-118">**GET**</span></span> | <span data-ttu-id="ee0de-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ee0de-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ee0de-120">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ee0de-120">Request headers</span></span>

<span data-ttu-id="ee0de-121">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ee0de-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ee0de-122">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ee0de-122">Request body</span></span>

<span data-ttu-id="ee0de-123">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ee0de-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ee0de-124">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ee0de-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="ee0de-125">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ee0de-125">REST response</span></span>

<span data-ttu-id="ee0de-126">Ha a művelet sikeres, ez a metódus egy **SupportProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="ee0de-126">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ee0de-127">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ee0de-127">Response success and error codes</span></span>

<span data-ttu-id="ee0de-128">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ee0de-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ee0de-129">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ee0de-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ee0de-130">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ee0de-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ee0de-131">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ee0de-131">Response example</span></span>

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
