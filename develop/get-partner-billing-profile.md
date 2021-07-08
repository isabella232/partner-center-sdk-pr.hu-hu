---
title: Partner számlázási profiljának lekérése
description: Lekért egy objektumot, amely a partner számlázási profilját képviseli.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 225d8ea2d92933838ae47eaf3308276aa1f1684c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548974"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="67fea-103">Partner számlázási profiljának lekérése</span><span class="sxs-lookup"><span data-stu-id="67fea-103">Get partner billing profile</span></span>

<span data-ttu-id="67fea-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="67fea-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="67fea-105">Lekért egy objektumot, amely a partner számlázási profilját képviseli.</span><span class="sxs-lookup"><span data-stu-id="67fea-105">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67fea-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="67fea-106">Prerequisites</span></span>

- <span data-ttu-id="67fea-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="67fea-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="67fea-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="67fea-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="67fea-109">C\#</span><span class="sxs-lookup"><span data-stu-id="67fea-109">C\#</span></span>

<span data-ttu-id="67fea-110">A partner számlázási profiljának lehívásához használja **az IAggregatePartner.Profiles** gyűjteményt, és hívja meg **a BillingProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="67fea-110">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="67fea-111">Végül hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync)</span><span class="sxs-lookup"><span data-stu-id="67fea-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="67fea-112">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="67fea-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="67fea-113">**Project:** PartnerCenterSDK.FeaturesSamples **osztály:** GetBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="67fea-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="67fea-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="67fea-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="67fea-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="67fea-115">Request syntax</span></span>

| <span data-ttu-id="67fea-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="67fea-116">Method</span></span>  | <span data-ttu-id="67fea-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="67fea-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="67fea-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="67fea-118">**GET**</span></span> | <span data-ttu-id="67fea-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="67fea-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="67fea-120">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="67fea-120">Request headers</span></span>

<span data-ttu-id="67fea-121">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="67fea-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="67fea-122">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="67fea-122">Request body</span></span>

<span data-ttu-id="67fea-123">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="67fea-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="67fea-124">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="67fea-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="67fea-125">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="67fea-125">REST response</span></span>

<span data-ttu-id="67fea-126">Ha sikeres, ez a metódus egy **BillingProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="67fea-126">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="67fea-127">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="67fea-127">Response success and error codes</span></span>

<span data-ttu-id="67fea-128">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="67fea-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="67fea-129">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="67fea-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="67fea-130">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="67fea-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="67fea-131">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="67fea-131">Response example</span></span>

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
