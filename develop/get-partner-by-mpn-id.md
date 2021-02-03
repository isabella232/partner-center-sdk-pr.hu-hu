---
title: Partner MPN-azonosítójának ellenőrzése
description: Megtudhatja, hogyan ellenőrizheti egy partner Microsoft Partner Network-azonosítóját (MPN-AZONOSÍTÓját) a partner MPN-profiljának C \# -n vagy a partner Center-REST API keresztül történő kérelmezésével.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768500"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="c77fd-103">Partner MPN-azonosító ellenőrzése C \# vagy a partner Center REST API használatával</span><span class="sxs-lookup"><span data-stu-id="c77fd-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="c77fd-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="c77fd-104">**Applies To**</span></span>

- <span data-ttu-id="c77fd-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c77fd-105">Partner Center</span></span>
- <span data-ttu-id="c77fd-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="c77fd-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c77fd-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c77fd-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c77fd-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="c77fd-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c77fd-109">Partner Microsoft Partner Network-azonosítójának (MPN-azonosító) ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="c77fd-109">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="c77fd-110">Az itt bemutatott módszer ellenőrzi a partner Microsoft Partner Network azonosítóját, ha a partneri MPN-profilt kéri a partner Centertől.</span><span class="sxs-lookup"><span data-stu-id="c77fd-110">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="c77fd-111">Az azonosító akkor minősül érvényesnek, ha a kérelem sikeres.</span><span class="sxs-lookup"><span data-stu-id="c77fd-111">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c77fd-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c77fd-112">Prerequisites</span></span>

- <span data-ttu-id="c77fd-113">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c77fd-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c77fd-114">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="c77fd-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c77fd-115">A partner MPN-AZONOSÍTÓjának ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="c77fd-115">The partner MPN ID to verify.</span></span> <span data-ttu-id="c77fd-116">Ha kihagyja ezt az értéket, a kérelem lekéri a bejelentkezett partner MPN-profilját.</span><span class="sxs-lookup"><span data-stu-id="c77fd-116">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="c77fd-117">C\#</span><span class="sxs-lookup"><span data-stu-id="c77fd-117">C\#</span></span>

<span data-ttu-id="c77fd-118">A partner MPN-AZONOSÍTÓjának ellenőrzéséhez először kérjen le egy felületet a [**IAggregatePartner. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) tulajdonságból a partneri profil gyűjtési műveleteihez.</span><span class="sxs-lookup"><span data-stu-id="c77fd-118">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="c77fd-119">Ezután szerezzen be egy felületet az MPN-profil műveleteihez a [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) tulajdonságból.</span><span class="sxs-lookup"><span data-stu-id="c77fd-119">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="c77fd-120">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) metódust az MPN-azonosítóval az MPN-profil lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="c77fd-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="c77fd-121">Ha kihagyja az MPN-azonosítót a Get vagy a GetAsync hívásból, a kérelem megkísérli a bejelentkezett partner MPN-profiljának beolvasását.</span><span class="sxs-lookup"><span data-stu-id="c77fd-121">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="c77fd-122">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c77fd-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c77fd-123">**Projekt**: partner Center SDK Samples **osztály**: VerifyPartnerMpnId.cs</span><span class="sxs-lookup"><span data-stu-id="c77fd-123">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="c77fd-124">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c77fd-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c77fd-125">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c77fd-125">Request syntax</span></span>

| <span data-ttu-id="c77fd-126">Metódus</span><span class="sxs-lookup"><span data-stu-id="c77fd-126">Method</span></span>  | <span data-ttu-id="c77fd-127">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c77fd-127">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="c77fd-128">**GET**</span><span class="sxs-lookup"><span data-stu-id="c77fd-128">**GET**</span></span> | <span data-ttu-id="c77fd-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/MPN? mpnId = {MPN-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c77fd-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="c77fd-130">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="c77fd-130">URI parameter</span></span>

<span data-ttu-id="c77fd-131">Adja meg a következő lekérdezési paramétert a partner azonosításához.</span><span class="sxs-lookup"><span data-stu-id="c77fd-131">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="c77fd-132">Ha kihagyja ezt a lekérdezési paramétert, a kérelem a bejelentkezett partner MPN-profilját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="c77fd-132">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="c77fd-133">Név</span><span class="sxs-lookup"><span data-stu-id="c77fd-133">Name</span></span>   | <span data-ttu-id="c77fd-134">Típus</span><span class="sxs-lookup"><span data-stu-id="c77fd-134">Type</span></span> | <span data-ttu-id="c77fd-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c77fd-135">Required</span></span> | <span data-ttu-id="c77fd-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="c77fd-136">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="c77fd-137">MPN-azonosító</span><span class="sxs-lookup"><span data-stu-id="c77fd-137">mpn-id</span></span> | <span data-ttu-id="c77fd-138">int</span><span class="sxs-lookup"><span data-stu-id="c77fd-138">int</span></span>  | <span data-ttu-id="c77fd-139">Nem</span><span class="sxs-lookup"><span data-stu-id="c77fd-139">No</span></span>       | <span data-ttu-id="c77fd-140">A partnert azonosító Microsoft Partner Network-azonosító.</span><span class="sxs-lookup"><span data-stu-id="c77fd-140">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c77fd-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c77fd-141">Request headers</span></span>

<span data-ttu-id="c77fd-142">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c77fd-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c77fd-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c77fd-143">Request body</span></span>

<span data-ttu-id="c77fd-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c77fd-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c77fd-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c77fd-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c77fd-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c77fd-146">REST response</span></span>

<span data-ttu-id="c77fd-147">Ha a művelet sikeres, a válasz törzse tartalmazza a partner [MpnProfile](profile-resources.md#mpnprofile) -erőforrását.</span><span class="sxs-lookup"><span data-stu-id="c77fd-147">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c77fd-148">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c77fd-148">Response success and error codes</span></span>

<span data-ttu-id="c77fd-149">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c77fd-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c77fd-150">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c77fd-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c77fd-151">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="c77fd-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="c77fd-152">Válasz példa (sikeres)</span><span class="sxs-lookup"><span data-stu-id="c77fd-152">Response example (success)</span></span>

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

### <a name="response-example-failure"></a><span data-ttu-id="c77fd-153">Válasz példa (hiba)</span><span class="sxs-lookup"><span data-stu-id="c77fd-153">Response example (failure)</span></span>

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
