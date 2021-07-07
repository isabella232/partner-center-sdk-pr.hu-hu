---
title: Partner ellenőrzőkódok Government Community Cloud le
description: Hogyan lehet lekérte a partnerek Government Community Cloud ellenőrző kódjait.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 04bccf587628337004a5825b534048945f791839
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873870"
---
# <a name="get-a-partners-validation-codes"></a><span data-ttu-id="c4a90-103">Egy partner ellenőrzési kódjainak lekérése</span><span class="sxs-lookup"><span data-stu-id="c4a90-103">Get a partner's validation codes</span></span>

<span data-ttu-id="c4a90-104">Ez a cikk bemutatja, hogyan gyűjti be egy partner Government Community Cloud érvényesítési kódjait.</span><span class="sxs-lookup"><span data-stu-id="c4a90-104">This article describes how to get a collection of a partner's Government Community Cloud validation codes.</span></span> <span data-ttu-id="c4a90-105">Az ügyfél kormányzati közösségi felhőben való létrehozásához érvényesítési kód szükséges.</span><span class="sxs-lookup"><span data-stu-id="c4a90-105">A validation code is required to create a customer in the government community cloud.</span></span>

<span data-ttu-id="c4a90-106">Ha érdekli, hogy szervezete vagy ügyfele szervezete jogosult-e Office 365 Kormányzati verzió GCC CSP használatára, tekintse meg az Office 365 Kormányzati verzió GCC CSP-partnerre és ügyfélre vonatkozó [jogosultsági feltételeket.](/partner-center/csp-gcc-validate)</span><span class="sxs-lookup"><span data-stu-id="c4a90-106">If you are interested in having your organization or your customer's organization approved for Office 365 Government GCC for CSP, see [Office 365 Government GCC for CSP Partner and Customer eligibility criteria](/partner-center/csp-gcc-validate).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4a90-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c4a90-107">Prerequisites</span></span>

- <span data-ttu-id="c4a90-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c4a90-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c4a90-109">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="c4a90-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c4a90-110">Megerősítést nyert az ellenőrzés az űrlap kitöltése [után itt.](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner)</span><span class="sxs-lookup"><span data-stu-id="c4a90-110">Confirmed validation after filling out form [here](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).</span></span>

- <span data-ttu-id="c4a90-111">Egy minősítéssel nem rendelkező ügyfél.</span><span class="sxs-lookup"><span data-stu-id="c4a90-111">A customer without a qualification.</span></span>

## <a name="c"></a><span data-ttu-id="c4a90-112">C\#</span><span class="sxs-lookup"><span data-stu-id="c4a90-112">C\#</span></span>

<span data-ttu-id="c4a90-113">Egy partner érvényesítési kódjai listájának lehívásához hívja meg a **GetValidationCodes kódot.**</span><span class="sxs-lookup"><span data-stu-id="c4a90-113">To get a list of all of a partner's validation codes, call **GetValidationCodes**.</span></span>

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a><span data-ttu-id="c4a90-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="c4a90-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c4a90-115">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="c4a90-115">Request syntax</span></span>

| <span data-ttu-id="c4a90-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="c4a90-116">Method</span></span>  | <span data-ttu-id="c4a90-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c4a90-117">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c4a90-118">**Kap**</span><span class="sxs-lookup"><span data-stu-id="c4a90-118">**GET**</span></span> | <span data-ttu-id="c4a90-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c4a90-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/all/validations HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c4a90-120">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c4a90-120">Request headers</span></span>

<span data-ttu-id="c4a90-121">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c4a90-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c4a90-122">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c4a90-122">Request body</span></span>

<span data-ttu-id="c4a90-123">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c4a90-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c4a90-124">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c4a90-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a><span data-ttu-id="c4a90-125">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c4a90-125">REST response</span></span>

<span data-ttu-id="c4a90-126">Ha a művelet sikeres, ez a metódus a válasz törzsében található [**ValidationCode**](utility-resources.md#validationcode) erőforrások listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="c4a90-126">If successful, this method returns a list of [**ValidationCode**](utility-resources.md#validationcode) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c4a90-127">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c4a90-127">Response success and error codes</span></span>

<span data-ttu-id="c4a90-128">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="c4a90-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c4a90-129">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="c4a90-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c4a90-130">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c4a90-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c4a90-131">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c4a90-131">Response example</span></span>

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
