---
title: Támogatási profil frissítése
description: A felhasználó támogatási profiljának frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 605c509eeb18f301144fec6287c9611d5a5acfe2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768271"
---
# <a name="update-support-profile"></a><span data-ttu-id="bbad6-103">Támogatási profil frissítése</span><span class="sxs-lookup"><span data-stu-id="bbad6-103">Update support profile</span></span>

<span data-ttu-id="bbad6-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="bbad6-104">**Applies To**</span></span>

- <span data-ttu-id="bbad6-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="bbad6-105">Partner Center</span></span>
- <span data-ttu-id="bbad6-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="bbad6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="bbad6-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="bbad6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="bbad6-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="bbad6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bbad6-109">A felhasználó támogatási profiljának frissítése.</span><span class="sxs-lookup"><span data-stu-id="bbad6-109">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbad6-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="bbad6-110">Prerequisites</span></span>

- <span data-ttu-id="bbad6-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="bbad6-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bbad6-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="bbad6-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="bbad6-113">C\#</span><span class="sxs-lookup"><span data-stu-id="bbad6-113">C\#</span></span>

<span data-ttu-id="bbad6-114">A támogatási profil frissítéséhez először [szerezze be a támogatási profilt](get-support-profile.md) , és végezze el a kívánt módosításokat.</span><span class="sxs-lookup"><span data-stu-id="bbad6-114">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="bbad6-115">Ezután használja a [**IPartnerOperations. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="bbad6-115">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="bbad6-116">Hívja meg a [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) tulajdonságot, majd a [**Update ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) vagy a [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="bbad6-116">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

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

<span data-ttu-id="bbad6-117">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bbad6-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bbad6-118">**Projekt**: PartnerCenterSDK. FeaturesSamples **osztály**: UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="bbad6-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bbad6-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="bbad6-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bbad6-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="bbad6-120">Request syntax</span></span>

| <span data-ttu-id="bbad6-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="bbad6-121">Method</span></span>  | <span data-ttu-id="bbad6-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="bbad6-122">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="bbad6-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="bbad6-123">**PUT**</span></span> | <span data-ttu-id="bbad6-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/supportprofile http/1.1</span><span class="sxs-lookup"><span data-stu-id="bbad6-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bbad6-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="bbad6-125">Request headers</span></span>

<span data-ttu-id="bbad6-126">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bbad6-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bbad6-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="bbad6-127">Request body</span></span>

<span data-ttu-id="bbad6-128">A teljes támogatási profil erőforrása.</span><span class="sxs-lookup"><span data-stu-id="bbad6-128">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="bbad6-129">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="bbad6-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="bbad6-130">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="bbad6-130">REST response</span></span>

<span data-ttu-id="bbad6-131">Ha ez sikeres, ez a metódus a válasz törzsében a frissített **SupportProfile** objektum tulajdonságait adja vissza.</span><span class="sxs-lookup"><span data-stu-id="bbad6-131">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bbad6-132">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="bbad6-132">Response success and error codes</span></span>

<span data-ttu-id="bbad6-133">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="bbad6-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bbad6-134">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="bbad6-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bbad6-135">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bbad6-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bbad6-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="bbad6-136">Response example</span></span>

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
