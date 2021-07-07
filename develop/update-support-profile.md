---
title: Támogatási profil frissítése
description: Frissíti a felhasználó támogatási profilját.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 143328c5501f525d52911eead805d420f79b78ff
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530344"
---
# <a name="update-support-profile"></a><span data-ttu-id="71c86-103">Támogatási profil frissítése</span><span class="sxs-lookup"><span data-stu-id="71c86-103">Update support profile</span></span>

<span data-ttu-id="71c86-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="71c86-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="71c86-105">Frissíti a felhasználó támogatási profilját.</span><span class="sxs-lookup"><span data-stu-id="71c86-105">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71c86-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="71c86-106">Prerequisites</span></span>

- <span data-ttu-id="71c86-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="71c86-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="71c86-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="71c86-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="71c86-109">C\#</span><span class="sxs-lookup"><span data-stu-id="71c86-109">C\#</span></span>

<span data-ttu-id="71c86-110">A támogatási profil frissítéséhez először szerezze be [a támogatási profilt,](get-support-profile.md) és tegye meg a kívánt módosításokat.</span><span class="sxs-lookup"><span data-stu-id="71c86-110">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="71c86-111">Ezután használja az [**IPartnerOperations.Profiles gyűjteményt.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="71c86-111">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="71c86-112">Hívja meg [**a SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) tulajdonságot, majd az [**Update() vagy**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) [**az UpdateAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync)</span><span class="sxs-lookup"><span data-stu-id="71c86-112">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// updated profile
SupportProfile newSupportProfile = new SupportProfile
{
   Email = supportProfile.Email,
   Website = supportProfile.Website,
   Telephone = new Random().Next(10000000, 99999999).ToString(CultureInfo.InvariantCulture)
};

SupportProfile updatedSupportProfile = partnerOperations.Profiles.SupportProfile.Update(newSupportProfile);
```

<span data-ttu-id="71c86-113">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="71c86-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="71c86-114">**Project:** PartnerCenterSDK.FeaturesSamples **osztály:** UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="71c86-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="71c86-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="71c86-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="71c86-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="71c86-116">Request syntax</span></span>

| <span data-ttu-id="71c86-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="71c86-117">Method</span></span>  | <span data-ttu-id="71c86-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="71c86-118">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="71c86-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="71c86-119">**PUT**</span></span> | <span data-ttu-id="71c86-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="71c86-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="71c86-121">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="71c86-121">Request headers</span></span>

<span data-ttu-id="71c86-122">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="71c86-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="71c86-123">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="71c86-123">Request body</span></span>

<span data-ttu-id="71c86-124">A teljes támogatásiprofil-erőforrás.</span><span class="sxs-lookup"><span data-stu-id="71c86-124">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="71c86-125">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="71c86-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/supportprofile HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
Content-Type: application/json
Content-Length: 167
Expect: 100-continue

{
    "Email": "email@sample.com",
    "Telephone": "4255555555",
    "Website": "www.microsoft.com",
    "ProfileType": "support_profile",
    "Attributes": {
        "ObjectType": "PartnerSupportProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="71c86-126">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="71c86-126">REST response</span></span>

<span data-ttu-id="71c86-127">Ha a művelet sikeres, ez a metódus a válasz törzsében adja vissza a **frissített SupportProfile** objektumtulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="71c86-127">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="71c86-128">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="71c86-128">Response success and error codes</span></span>

<span data-ttu-id="71c86-129">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="71c86-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="71c86-130">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="71c86-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="71c86-131">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="71c86-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="71c86-132">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="71c86-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
Date: Wed, 25 Nov 2015 07:16:18 GMT

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
