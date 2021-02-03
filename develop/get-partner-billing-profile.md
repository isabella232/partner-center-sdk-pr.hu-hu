---
title: Partner számlázási profiljának lekérése
description: Lekéri a partner számlázási profilját jelképező objektumot.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 94c5ff8fc351282ca3b4721511f02ba6a0cc403c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768435"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="9debe-103">Partner számlázási profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="9debe-103">Get partner billing profile</span></span>

<span data-ttu-id="9debe-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="9debe-104">**Applies To**</span></span>

- <span data-ttu-id="9debe-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="9debe-105">Partner Center</span></span>
- <span data-ttu-id="9debe-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="9debe-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9debe-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="9debe-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9debe-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="9debe-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9debe-109">Lekéri a partner számlázási profilját jelképező objektumot.</span><span class="sxs-lookup"><span data-stu-id="9debe-109">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9debe-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9debe-110">Prerequisites</span></span>

- <span data-ttu-id="9debe-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="9debe-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9debe-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="9debe-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="9debe-113">C\#</span><span class="sxs-lookup"><span data-stu-id="9debe-113">C\#</span></span>

<span data-ttu-id="9debe-114">Partner számlázási profil beszerzéséhez használja a **IAggregatePartner. Profiles** gyűjteményt, és hívja meg a **BillingProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="9debe-114">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="9debe-115">Végül hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="9debe-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="9debe-116">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9debe-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9debe-117">**Projekt**: PartnerCenterSDK. FeaturesSamples **osztály**: GetBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="9debe-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9debe-118">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="9debe-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9debe-119">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="9debe-119">Request syntax</span></span>

| <span data-ttu-id="9debe-120">Metódus</span><span class="sxs-lookup"><span data-stu-id="9debe-120">Method</span></span>  | <span data-ttu-id="9debe-121">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="9debe-121">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="9debe-122">**GET**</span><span class="sxs-lookup"><span data-stu-id="9debe-122">**GET**</span></span> | <span data-ttu-id="9debe-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="9debe-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9debe-124">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="9debe-124">Request headers</span></span>

<span data-ttu-id="9debe-125">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9debe-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9debe-126">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="9debe-126">Request body</span></span>

<span data-ttu-id="9debe-127">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="9debe-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9debe-128">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="9debe-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="9debe-129">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="9debe-129">REST response</span></span>

<span data-ttu-id="9debe-130">Ha ez sikeres, ez a metódus egy **BillingProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="9debe-130">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9debe-131">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="9debe-131">Response success and error codes</span></span>

<span data-ttu-id="9debe-132">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="9debe-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9debe-133">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="9debe-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9debe-134">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9debe-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9debe-135">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="9debe-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
Date: Tue, 22 Mar 2016 17:10:02 GMT

{
    "companyName":"TEST_TEST_BugBash1",
    "address":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"1 Microsoft Way",
        "addressLine2":"","postalCode":"98052"
    },
    "primaryContact":{
        "firstName":"James",
        "lastName":"Burk",
        "phoneNumber":"2066017143"
    },
    "purchaseOrderNumber":"9888",
    "taxId":"12-345678",
    "billingCurrency":"USD",
    "profileType":"BillingProfile",
    "links":{
        "self":{
            "uri":"/profiles/billing",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"BillingProfile"
    }
}
```
