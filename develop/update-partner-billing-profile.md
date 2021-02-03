---
title: A partner számlázási profiljának frissítése
description: A partner számlázási profiljának frissítése.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 34e7d2396d6dbdd45a6cf87a3bda481f51326f1e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768003"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="393d3-103">A partner számlázási profiljának frissítése</span><span class="sxs-lookup"><span data-stu-id="393d3-103">Update the partner billing profile</span></span>

<span data-ttu-id="393d3-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="393d3-104">**Applies To**</span></span>

- <span data-ttu-id="393d3-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="393d3-105">Partner Center</span></span>
- <span data-ttu-id="393d3-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="393d3-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="393d3-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="393d3-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="393d3-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="393d3-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="393d3-109">A partner számlázási profiljának frissítése</span><span class="sxs-lookup"><span data-stu-id="393d3-109">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="393d3-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="393d3-110">Prerequisites</span></span>

- <span data-ttu-id="393d3-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="393d3-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="393d3-112">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="393d3-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="393d3-113">C\#</span><span class="sxs-lookup"><span data-stu-id="393d3-113">C\#</span></span>

<span data-ttu-id="393d3-114">Ha frissíteni szeretne egy partner számlázási profilt, kérje le a meglévő profilt.</span><span class="sxs-lookup"><span data-stu-id="393d3-114">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="393d3-115">A profil frissítése után használja a **IAggregatePartner. Profiles** gyűjteményt, és hívja meg a **BillingProfile** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="393d3-115">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="393d3-116">Végül hívja meg a **Update ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="393d3-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="393d3-117">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="393d3-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="393d3-118">**Projekt**: partner Center SDK Samples **osztály**: UpdateBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="393d3-118">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="393d3-119">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="393d3-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="393d3-120">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="393d3-120">Request syntax</span></span>

| <span data-ttu-id="393d3-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="393d3-121">Method</span></span>  | <span data-ttu-id="393d3-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="393d3-122">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="393d3-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="393d3-123">**PUT**</span></span> | <span data-ttu-id="393d3-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/Profiles/Billing http/1.1</span><span class="sxs-lookup"><span data-stu-id="393d3-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="393d3-125">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="393d3-125">Request headers</span></span>

<span data-ttu-id="393d3-126">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="393d3-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="393d3-127">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="393d3-127">Request body</span></span>

<span data-ttu-id="393d3-128">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="393d3-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="393d3-129">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="393d3-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="393d3-130">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="393d3-130">REST response</span></span>

<span data-ttu-id="393d3-131">Ha ez sikeres, ez a metódus egy **BillingProfile** objektumot ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="393d3-131">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="393d3-132">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="393d3-132">Response success and error codes</span></span>

<span data-ttu-id="393d3-133">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="393d3-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="393d3-134">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="393d3-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="393d3-135">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="393d3-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="393d3-136">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="393d3-136">Response example</span></span>

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
