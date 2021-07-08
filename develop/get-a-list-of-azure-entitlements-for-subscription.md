---
title: Egy előfizetés Azure-jogosultsági listájának lekérése
description: Az AzureEntitlement erőforrással lekért Azure-jogosultságú erőforrások gyűjteményét, amelyek egy előfizetéshez tartoznak.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 280da155122ed9efd99838d7819fb34f8f7ec52c
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874363"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="30ab2-103">Egy előfizetés Azure-jogosultsági listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="30ab2-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="30ab2-104">Az [Azure-jogosultsági](subscription-resources.md#azureentitlement) erőforrás **(AzureEntitlement**) használatával egy előfizetéshez tartozó erőforrások gyűjteményét kaphatja meg.</span><span class="sxs-lookup"><span data-stu-id="30ab2-104">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30ab2-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="30ab2-105">Prerequisites</span></span>

- <span data-ttu-id="30ab2-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="30ab2-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="30ab2-107">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="30ab2-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="30ab2-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30ab2-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="30ab2-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="30ab2-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="30ab2-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="30ab2-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="30ab2-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="30ab2-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="30ab2-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="30ab2-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="30ab2-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30ab2-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="30ab2-114">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="30ab2-114">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="30ab2-115">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="30ab2-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="30ab2-116">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="30ab2-116">Request syntax</span></span>

| <span data-ttu-id="30ab2-117">Metódus</span><span class="sxs-lookup"><span data-stu-id="30ab2-117">Method</span></span>  | <span data-ttu-id="30ab2-118">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="30ab2-118">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="30ab2-119">**Kap**</span><span class="sxs-lookup"><span data-stu-id="30ab2-119">**GET**</span></span> | <span data-ttu-id="30ab2-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{előfizetés-azonosító}/azureentitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="30ab2-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="30ab2-121">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="30ab2-121">URI parameters</span></span>

<span data-ttu-id="30ab2-122">Az alábbi táblázat felsorolja az előfizetés összes Azure-jogosultságának lekérdezhető lekérdezési paramétereit.</span><span class="sxs-lookup"><span data-stu-id="30ab2-122">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="30ab2-123">Név</span><span class="sxs-lookup"><span data-stu-id="30ab2-123">Name</span></span>                   | <span data-ttu-id="30ab2-124">Típus</span><span class="sxs-lookup"><span data-stu-id="30ab2-124">Type</span></span>     | <span data-ttu-id="30ab2-125">Kötelező</span><span class="sxs-lookup"><span data-stu-id="30ab2-125">Required</span></span> | <span data-ttu-id="30ab2-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="30ab2-126">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="30ab2-127">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="30ab2-127">**customer-tenant-id**</span></span> | <span data-ttu-id="30ab2-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="30ab2-128">**guid**</span></span> | <span data-ttu-id="30ab2-129">Y</span><span class="sxs-lookup"><span data-stu-id="30ab2-129">Y</span></span>        | <span data-ttu-id="30ab2-130">Az ügyfélnek megfelelő GUID.</span><span class="sxs-lookup"><span data-stu-id="30ab2-130">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="30ab2-131">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="30ab2-131">**subscription-id**</span></span>       | <span data-ttu-id="30ab2-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="30ab2-132">**guid**</span></span> | <span data-ttu-id="30ab2-133">Y</span><span class="sxs-lookup"><span data-stu-id="30ab2-133">Y</span></span>        | <span data-ttu-id="30ab2-134">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="30ab2-134">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="30ab2-135">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="30ab2-135">Request headers</span></span>

<span data-ttu-id="30ab2-136">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="30ab2-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="30ab2-137">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="30ab2-137">Request body</span></span>

<span data-ttu-id="30ab2-138">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="30ab2-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="30ab2-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="30ab2-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="30ab2-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="30ab2-140">REST response</span></span>

<span data-ttu-id="30ab2-141">Ha a művelet sikeres, ez a metódus [**azureentitlement-erőforrások**](subscription-resources.md#azureentitlement) gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="30ab2-141">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="30ab2-142">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="30ab2-142">Response success and error codes</span></span>

<span data-ttu-id="30ab2-143">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="30ab2-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="30ab2-144">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="30ab2-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="30ab2-145">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="30ab2-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="30ab2-146">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="30ab2-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 04 Oct 2019 05:50:45 GMT

{
"totalCount":1,
"items":[
  {
    "id":"899ae6f1-8a74-4d5e-b6c6-e6b5019bbff8",
    "friendlyName":"Microsoft Azure",
    "status":"active",
    "subscriptionId":"3f15978e-005c-b763-bb78-2a8fab289c58"
   }],
    "attributes":{"objectType":"Collection"}
  }
```
