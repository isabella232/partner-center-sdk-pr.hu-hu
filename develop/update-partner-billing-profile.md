---
title: A partner számlázási profiljának frissítése
description: Frissíti a partner számlázási profilját.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 2b09a0045df15d774c892a59fba8502d4d4f7024
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529766"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="154e0-103">A partner számlázási profiljának frissítése</span><span class="sxs-lookup"><span data-stu-id="154e0-103">Update the partner billing profile</span></span>

<span data-ttu-id="154e0-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="154e0-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="154e0-105">Frissíti egy partner számlázási profilját</span><span class="sxs-lookup"><span data-stu-id="154e0-105">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="154e0-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="154e0-106">Prerequisites</span></span>

- <span data-ttu-id="154e0-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="154e0-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="154e0-108">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="154e0-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="154e0-109">C\#</span><span class="sxs-lookup"><span data-stu-id="154e0-109">C\#</span></span>

<span data-ttu-id="154e0-110">A partner számlázási profiljának frissítéséhez olvassa be a meglévő profilt.</span><span class="sxs-lookup"><span data-stu-id="154e0-110">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="154e0-111">A profil frissítése után használja az **IAggregatePartner.Profiles** gyűjteményt, és hívja meg **a BillingProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="154e0-111">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="154e0-112">Végül hívja meg az **Update() metódust.**</span><span class="sxs-lookup"><span data-stu-id="154e0-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="154e0-113">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="154e0-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="154e0-114">**Project:** Partnerközpont SDK **Osztály:** UpdateBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="154e0-114">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="154e0-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="154e0-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="154e0-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="154e0-116">Request syntax</span></span>

| <span data-ttu-id="154e0-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="154e0-117">Method</span></span>  | <span data-ttu-id="154e0-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="154e0-118">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="154e0-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="154e0-119">**PUT**</span></span> | <span data-ttu-id="154e0-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="154e0-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="154e0-121">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="154e0-121">Request headers</span></span>

<span data-ttu-id="154e0-122">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="154e0-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="154e0-123">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="154e0-123">Request body</span></span>

<span data-ttu-id="154e0-124">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="154e0-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="154e0-125">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="154e0-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 613
Expect: 100-continue

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="154e0-126">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="154e0-126">REST response</span></span>

<span data-ttu-id="154e0-127">Ha sikeres, ez a metódus egy **BillingProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="154e0-127">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="154e0-128">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="154e0-128">Response success and error codes</span></span>

<span data-ttu-id="154e0-129">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="154e0-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="154e0-130">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="154e0-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="154e0-131">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="154e0-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="154e0-132">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="154e0-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
Date: Mon, 21 Mar 2016 05:47:16 GMT

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```
