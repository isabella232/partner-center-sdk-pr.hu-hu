---
title: Partner MPN-azonosítójának ellenőrzése
description: Megtudhatja, hogyan ellenőrizheti egy partner Microsoft Partner Network-azonosítóját (MPN-azonosítóját) a partner MPN-profiljának C-n vagy a \# Partnerközpont REST API.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bd51850c7bc5a099a34f9c028a58e247c2600a3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548821"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="b3966-103">Partner MPN-azonosítójának ellenőrzése C-n vagy a \# Partnerközpont REST API</span><span class="sxs-lookup"><span data-stu-id="b3966-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="b3966-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b3966-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b3966-105">A partner ügyfél-azonosítójának Microsoft Partner Network (MPN-azonosító).</span><span class="sxs-lookup"><span data-stu-id="b3966-105">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="b3966-106">Az itt bemutatott módszer úgy ellenőrzi a partner Microsoft Partner Network azonosítóját, hogy a partner MPN-profilját kéri le a partnerközpontból.</span><span class="sxs-lookup"><span data-stu-id="b3966-106">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="b3966-107">Az azonosító akkor minősül érvényesnek, ha a kérés sikeres volt.</span><span class="sxs-lookup"><span data-stu-id="b3966-107">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3966-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b3966-108">Prerequisites</span></span>

- <span data-ttu-id="b3966-109">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b3966-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b3966-110">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b3966-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b3966-111">Az ellenőriznie kell a partner MPN-azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="b3966-111">The partner MPN ID to verify.</span></span> <span data-ttu-id="b3966-112">Ha kihagyja ezt az értéket, a kérés lekéri a bejelentkezett partner MPN-profilját.</span><span class="sxs-lookup"><span data-stu-id="b3966-112">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="b3966-113">C\#</span><span class="sxs-lookup"><span data-stu-id="b3966-113">C\#</span></span>

<span data-ttu-id="b3966-114">A partner MPN-azonosítójának ellenőrzéséhez először az [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) tulajdonságból kell lekérni a partnerprofil-gyűjtési műveletek felületét.</span><span class="sxs-lookup"><span data-stu-id="b3966-114">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="b3966-115">Ezután szerezze be az MPN-profilműveleteket az [**MpnProfile tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile)</span><span class="sxs-lookup"><span data-stu-id="b3966-115">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="b3966-116">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) vagy [**GetAsync metódusokat**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) az MPN-azonosítóval az MPN-profil lekéréshez.</span><span class="sxs-lookup"><span data-stu-id="b3966-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="b3966-117">Ha kihagyja az MPN-azonosítót a Get vagy GetAsync hívásból, a kérés megkísérli lekérni a bejelentkezett partner MPN-profilját.</span><span class="sxs-lookup"><span data-stu-id="b3966-117">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="b3966-118">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="b3966-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b3966-119">**Project**: Partnerközpont SDK **osztály:** VerifyPartnerMpnId.cs</span><span class="sxs-lookup"><span data-stu-id="b3966-119">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b3966-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="b3966-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b3966-121">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="b3966-121">Request syntax</span></span>

| <span data-ttu-id="b3966-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="b3966-122">Method</span></span>  | <span data-ttu-id="b3966-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b3966-123">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="b3966-124">**Kap**</span><span class="sxs-lookup"><span data-stu-id="b3966-124">**GET**</span></span> | <span data-ttu-id="b3966-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b3966-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="b3966-126">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="b3966-126">URI parameter</span></span>

<span data-ttu-id="b3966-127">Adja meg a következő lekérdezési paramétert a partner azonosításához.</span><span class="sxs-lookup"><span data-stu-id="b3966-127">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="b3966-128">Ha kihagyja ezt a lekérdezési paramétert, a kérés a bejelentkezett partner MPN-profilját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="b3966-128">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="b3966-129">Név</span><span class="sxs-lookup"><span data-stu-id="b3966-129">Name</span></span>   | <span data-ttu-id="b3966-130">Típus</span><span class="sxs-lookup"><span data-stu-id="b3966-130">Type</span></span> | <span data-ttu-id="b3966-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b3966-131">Required</span></span> | <span data-ttu-id="b3966-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="b3966-132">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="b3966-133">mpn-id</span><span class="sxs-lookup"><span data-stu-id="b3966-133">mpn-id</span></span> | <span data-ttu-id="b3966-134">int</span><span class="sxs-lookup"><span data-stu-id="b3966-134">int</span></span>  | <span data-ttu-id="b3966-135">Nem</span><span class="sxs-lookup"><span data-stu-id="b3966-135">No</span></span>       | <span data-ttu-id="b3966-136">A Microsoft Partner Network azonosítóját.</span><span class="sxs-lookup"><span data-stu-id="b3966-136">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b3966-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b3966-137">Request headers</span></span>

<span data-ttu-id="b3966-138">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b3966-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b3966-139">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b3966-139">Request body</span></span>

<span data-ttu-id="b3966-140">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b3966-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b3966-141">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b3966-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="b3966-142">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b3966-142">REST response</span></span>

<span data-ttu-id="b3966-143">Sikeres művelet esetén a válasz törzse tartalmazza a partner [MpnProfile](profile-resources.md#mpnprofile) erőforrását.</span><span class="sxs-lookup"><span data-stu-id="b3966-143">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b3966-144">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b3966-144">Response success and error codes</span></span>

<span data-ttu-id="b3966-145">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="b3966-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b3966-146">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="b3966-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b3966-147">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b3966-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="b3966-148">Válasz példa (sikeres)</span><span class="sxs-lookup"><span data-stu-id="b3966-148">Response example (success)</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a><span data-ttu-id="b3966-149">Példa válaszra (hiba)</span><span class="sxs-lookup"><span data-stu-id="b3966-149">Response example (failure)</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
