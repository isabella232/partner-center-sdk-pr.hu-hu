---
title: A partner kormányzati közösségi felhő-ellenőrzési kódjainak beszerzése
description: A partner kormányzati közösségi felhő-ellenőrzési kódjának beszerzése.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: d84a3d3c69d835e42565c4e6f1edb06ab338340a
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768064"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="27e98-103">Egy partner ellenőrzési kódjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="27e98-103">Get a partner's validation codes</span></span>

<span data-ttu-id="27e98-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="27e98-104">**Applies To**</span></span>

- <span data-ttu-id="27e98-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="27e98-105">Partner Center</span></span>

<span data-ttu-id="27e98-106">Hogyan szerezhet be egy partner kormányzati közösségi felhő-ellenőrzési kódjait.</span><span class="sxs-lookup"><span data-stu-id="27e98-106">How to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="27e98-107">Egy érvényesítési kódnak kell lennie ahhoz, hogy ügyfelet hozzon létre a kormányzati közösségi felhőben.</span><span class="sxs-lookup"><span data-stu-id="27e98-107">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="27e98-108">Ha szeretné, hogy a szervezete vagy az ügyfelek szervezete számára engedélyezett legyen az Office 365 Government GCC a CSP-hez, tekintse meg a következőt: [Office 365 Government GCC for CSP partner és ügyfél jogosultsági feltételei/partner-központ/CSP-GCC-validate).</span><span class="sxs-lookup"><span data-stu-id="27e98-108">If you are interested in having your organization or your customers organization approved for Office 365 Government GCC for CSP, please see [Office 365 Government GCC for CSP Partner and Customer Eligibility Criteria/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27e98-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="27e98-109">Prerequisites</span></span>

- <span data-ttu-id="27e98-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="27e98-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="27e98-111">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="27e98-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="27e98-112">Ellenőrzés megerősítése az űrlap kitöltése után [itt](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span><span class="sxs-lookup"><span data-stu-id="27e98-112">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="27e98-113">Az ügyfél minősítés nélkül.</span><span class="sxs-lookup"><span data-stu-id="27e98-113">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="27e98-114">C\#</span><span class="sxs-lookup"><span data-stu-id="27e98-114">C\#</span></span>

<span data-ttu-id="27e98-115">A partner összes érvényesítési kódjának listájának lekéréséhez hívja meg a **GetValidationCodes**.</span><span class="sxs-lookup"><span data-stu-id="27e98-115">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="27e98-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="27e98-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="27e98-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="27e98-117">Request syntax</span></span>

| <span data-ttu-id="27e98-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="27e98-118">Method</span></span>  | <span data-ttu-id="27e98-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="27e98-119">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="27e98-120">**GET**</span><span class="sxs-lookup"><span data-stu-id="27e98-120">**GET**</span></span> | <span data-ttu-id="27e98-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/all/validations http/1.1</span><span class="sxs-lookup"><span data-stu-id="27e98-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="27e98-122">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="27e98-122">Request headers</span></span>

<span data-ttu-id="27e98-123">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="27e98-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="27e98-124">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="27e98-124">Request body</span></span>

<span data-ttu-id="27e98-125">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="27e98-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="27e98-126">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="27e98-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="27e98-127">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="27e98-127">REST response</span></span>

<span data-ttu-id="27e98-128">Ha ez sikeres, ez a metódus a válasz törzsében lévő [**ValidationCode**](utility-resources.md#validationcode) -erőforrások listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="27e98-128">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="27e98-129">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="27e98-129">Response success and error codes</span></span>

<span data-ttu-id="27e98-130">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="27e98-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="27e98-131">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="27e98-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="27e98-132">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="27e98-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="27e98-133">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="27e98-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
