---
title: A Microsoft Partner Network-profil lekérése
description: Lekért egy objektumot, amely a partner MPN-profilját képviseli.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38c12a9a9755b9838b7742d9f38c5cbd52b81210
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548855"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="d2b5f-103">A Microsoft Partner Network-profil lekérése</span><span class="sxs-lookup"><span data-stu-id="d2b5f-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="d2b5f-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d2b5f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d2b5f-105">Lekért egy objektumot, amely a partner MPN-profilját képviseli.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-105">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2b5f-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d2b5f-106">Prerequisites</span></span>

- <span data-ttu-id="d2b5f-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d2b5f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d2b5f-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="d2b5f-109">C\#</span><span class="sxs-lookup"><span data-stu-id="d2b5f-109">C\#</span></span>

<span data-ttu-id="d2b5f-110">A partnerhálózati profil lehívásához használja az **IAggregatePartner.Profiles** gyűjteményt, és hívja meg **az MpnProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-110">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="d2b5f-111">Végül hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="d2b5f-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="d2b5f-112">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d2b5f-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d2b5f-113">**Project**:P centerSDK.FeaturesSamples **osztály:** GetMPNProfile.cs</span><span class="sxs-lookup"><span data-stu-id="d2b5f-113">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="d2b5f-114">Java</span><span class="sxs-lookup"><span data-stu-id="d2b5f-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="d2b5f-115">A partnerhálózati profil lehívásához használja az **IAggregatePartner.getProfiles** függvényt, és hívja meg a **getMpnProfile** függvényt.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-115">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="d2b5f-116">Végül hívja meg a **get()** függvényt.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="d2b5f-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2b5f-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="d2b5f-118">A partnerhálózati profil lekért végrehajtásához hajtsa végre a [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) parancsot.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-118">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="d2b5f-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="d2b5f-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d2b5f-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d2b5f-120">Request syntax</span></span>

| <span data-ttu-id="d2b5f-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="d2b5f-121">Method</span></span>  | <span data-ttu-id="d2b5f-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d2b5f-122">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="d2b5f-123">**Kap**</span><span class="sxs-lookup"><span data-stu-id="d2b5f-123">**GET**</span></span> | <span data-ttu-id="d2b5f-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d2b5f-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d2b5f-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d2b5f-125">Request headers</span></span>

<span data-ttu-id="d2b5f-126">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d2b5f-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d2b5f-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="d2b5f-127">Request body</span></span>

<span data-ttu-id="d2b5f-128">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d2b5f-129">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d2b5f-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="d2b5f-130">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d2b5f-130">REST response</span></span>

<span data-ttu-id="d2b5f-131">Ha sikeres, ez a metódus egy **MPNProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-131">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d2b5f-132">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d2b5f-132">Response success and error codes</span></span>

<span data-ttu-id="d2b5f-133">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d2b5f-134">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="d2b5f-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d2b5f-135">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d2b5f-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d2b5f-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d2b5f-136">Response example</span></span>

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
