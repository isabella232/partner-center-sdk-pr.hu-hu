---
title: A Microsoft Partner Network-profil lekérése
description: Lekéri a partner MPN-profilját jelképező objektumot.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8f3e74462da05de0be47964beb34228650b1f53
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768483"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="f1a10-103">A Microsoft Partner Network-profil lekérése</span><span class="sxs-lookup"><span data-stu-id="f1a10-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="f1a10-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="f1a10-104">**Applies To**</span></span>

- <span data-ttu-id="f1a10-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f1a10-105">Partner Center</span></span>
- <span data-ttu-id="f1a10-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="f1a10-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f1a10-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f1a10-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f1a10-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f1a10-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f1a10-109">Lekéri a partner MPN-profilját jelképező objektumot.</span><span class="sxs-lookup"><span data-stu-id="f1a10-109">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1a10-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f1a10-110">Prerequisites</span></span>

- <span data-ttu-id="f1a10-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="f1a10-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f1a10-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="f1a10-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="f1a10-113">C\#</span><span class="sxs-lookup"><span data-stu-id="f1a10-113">C\#</span></span>

<span data-ttu-id="f1a10-114">Partner hálózati profil beszerzéséhez használja a **IAggregatePartner. Profiles** gyűjteményt, és hívja meg a **MpnProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="f1a10-114">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="f1a10-115">Végül hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="f1a10-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="f1a10-116">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f1a10-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f1a10-117">**Projekt**:P Artnercentersdk. FeaturesSamples **osztály**: GetMPNProfile.cs</span><span class="sxs-lookup"><span data-stu-id="f1a10-117">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="f1a10-118">Java</span><span class="sxs-lookup"><span data-stu-id="f1a10-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f1a10-119">Partner hálózati profil beszerzéséhez használja a **IAggregatePartner. getProfiles** függvényt, és hívja meg a **getMpnProfile** függvényt.</span><span class="sxs-lookup"><span data-stu-id="f1a10-119">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="f1a10-120">Végül hívja meg a **Get ()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="f1a10-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="f1a10-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1a10-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f1a10-122">Partner hálózati profil beszerzéséhez hajtsa végre a [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="f1a10-122">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="f1a10-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="f1a10-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f1a10-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f1a10-124">Request syntax</span></span>

| <span data-ttu-id="f1a10-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="f1a10-125">Method</span></span>  | <span data-ttu-id="f1a10-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f1a10-126">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="f1a10-127">**GET**</span><span class="sxs-lookup"><span data-stu-id="f1a10-127">**GET**</span></span> | <span data-ttu-id="f1a10-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN http/1.1</span><span class="sxs-lookup"><span data-stu-id="f1a10-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f1a10-129">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f1a10-129">Request headers</span></span>

<span data-ttu-id="f1a10-130">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f1a10-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f1a10-131">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f1a10-131">Request body</span></span>

<span data-ttu-id="f1a10-132">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="f1a10-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f1a10-133">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f1a10-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="f1a10-134">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f1a10-134">REST response</span></span>

<span data-ttu-id="f1a10-135">Ha ez sikeres, ez a metódus egy **MPNProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="f1a10-135">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f1a10-136">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f1a10-136">Response success and error codes</span></span>

<span data-ttu-id="f1a10-137">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="f1a10-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f1a10-138">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="f1a10-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f1a10-139">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f1a10-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f1a10-140">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="f1a10-140">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```
