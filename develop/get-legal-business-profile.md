---
title: A partner hivatalos vállalkozási profiljának lekérése
description: Megtudhatja, hogyan használhatja az API-kat a jogi üzleti profilja lekért útjára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0654e364674bc2db129a0904d411c6fb67cbb9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549059"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="9c2a7-103">A partner hivatalos vállalkozási profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="9c2a7-103">Get the partner legal business profile</span></span>

<span data-ttu-id="9c2a7-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9c2a7-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9c2a7-105">A partner jogi üzleti profiljának lekért létrehozása.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-105">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c2a7-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9c2a7-106">Prerequisites</span></span>

- <span data-ttu-id="9c2a7-107">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9c2a7-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9c2a7-108">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="9c2a7-109">C\#</span><span class="sxs-lookup"><span data-stu-id="9c2a7-109">C\#</span></span>

<span data-ttu-id="9c2a7-110">A partner jogi üzleti profiljának legyűjtéséhez először szerezze be a partnerprofil-műveletek gyűjteményének felületét az **IAggregatePartner.Profiles tulajdonságból.**</span><span class="sxs-lookup"><span data-stu-id="9c2a7-110">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="9c2a7-111">Ezután lekéri a **LegalBusinessProfile** tulajdonság értékét, hogy lekérje a jogi üzleti profil műveleteinek felületét.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-111">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="9c2a7-112">Végül hívja meg a [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) vagy a [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) metódust a profil lekéréshez.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="9c2a7-113">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="9c2a7-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9c2a7-114">**Project**: Partnerközpont SDK **Osztály:** GetLegalBusinessProfile.cs</span><span class="sxs-lookup"><span data-stu-id="9c2a7-114">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9c2a7-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="9c2a7-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9c2a7-116">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="9c2a7-116">Request syntax</span></span>

| <span data-ttu-id="9c2a7-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="9c2a7-117">Method</span></span>  | <span data-ttu-id="9c2a7-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9c2a7-118">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="9c2a7-119">**Kap**</span><span class="sxs-lookup"><span data-stu-id="9c2a7-119">**GET**</span></span> | <span data-ttu-id="9c2a7-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9c2a7-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9c2a7-121">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9c2a7-121">Request headers</span></span>

<span data-ttu-id="9c2a7-122">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9c2a7-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9c2a7-123">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9c2a7-123">Request body</span></span>

<span data-ttu-id="9c2a7-124">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9c2a7-125">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9c2a7-125">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness?vettingVersion=Current HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9c2a7-126">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9c2a7-126">REST response</span></span>

<span data-ttu-id="9c2a7-127">Ha a művelet sikeres, ez a metódus egy **LegalBusinessProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-127">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9c2a7-128">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9c2a7-128">Response success and error codes</span></span>

<span data-ttu-id="9c2a7-129">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9c2a7-130">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="9c2a7-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9c2a7-131">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9c2a7-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9c2a7-132">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9c2a7-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1151
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CV: MEgCpJUoGUeXG+4a.0
MS-ServerId: 030011719
Date: Tue, 21 Mar 2017 17:29:52 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550100"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550100"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
