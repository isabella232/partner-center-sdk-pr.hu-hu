---
title: Egy előfizetés Azure-jogosultsági listájának lekérése
description: A AzureEntitlement-erőforrás segítségével beszerezhet egy, az előfizetéshez tartozó Azure-jogosultsági erőforrások gyűjteményét.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: d7d0a10c571dc073bd49e82084f3b7ece7234daf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767952"
---
# <a name="get-a-list-of-azure-entitlements-for-a-subscription"></a><span data-ttu-id="c0a94-103">Egy előfizetés Azure-jogosultsági listájának lekérése</span><span class="sxs-lookup"><span data-stu-id="c0a94-103">Get a list of Azure entitlements for a subscription</span></span>

<span data-ttu-id="c0a94-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="c0a94-104">**Applies to:**</span></span>

- <span data-ttu-id="c0a94-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="c0a94-105">Partner Center</span></span>

<span data-ttu-id="c0a94-106">Használhatja az [Azure jogosultsági erőforrást](subscription-resources.md#azureentitlement) (**AzureEntitlement**) az előfizetéshez tartozó erőforrások gyűjteményének beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="c0a94-106">You can use the [Azure entitlement resource](subscription-resources.md#azureentitlement) (**AzureEntitlement**) to get a collection of resources that belong to a subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0a94-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c0a94-107">Prerequisites</span></span>

- <span data-ttu-id="c0a94-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="c0a94-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c0a94-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="c0a94-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c0a94-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c0a94-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c0a94-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="c0a94-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c0a94-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="c0a94-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c0a94-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="c0a94-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c0a94-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="c0a94-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c0a94-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c0a94-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c0a94-116">Egy előfizetés-azonosító.</span><span class="sxs-lookup"><span data-stu-id="c0a94-116">A subscription identifier.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c0a94-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="c0a94-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c0a94-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="c0a94-118">Request syntax</span></span>

| <span data-ttu-id="c0a94-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="c0a94-119">Method</span></span>  | <span data-ttu-id="c0a94-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="c0a94-120">Request URI</span></span>                                                                                                                   |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="c0a94-121">**GET**</span><span class="sxs-lookup"><span data-stu-id="c0a94-121">**GET**</span></span> | <span data-ttu-id="c0a94-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/azureentitlements http/1.1</span><span class="sxs-lookup"><span data-stu-id="c0a94-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/azureentitlements HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="c0a94-123">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="c0a94-123">URI parameters</span></span>

<span data-ttu-id="c0a94-124">A következő táblázat felsorolja a szükséges lekérdezési paramétereket az előfizetéshez tartozó összes Azure-jogosultság beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="c0a94-124">The following table lists the required query parameters to get all the Azure entitlements for a subscription.</span></span>

| <span data-ttu-id="c0a94-125">Név</span><span class="sxs-lookup"><span data-stu-id="c0a94-125">Name</span></span>                   | <span data-ttu-id="c0a94-126">Típus</span><span class="sxs-lookup"><span data-stu-id="c0a94-126">Type</span></span>     | <span data-ttu-id="c0a94-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="c0a94-127">Required</span></span> | <span data-ttu-id="c0a94-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="c0a94-128">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="c0a94-129">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="c0a94-129">**customer-tenant-id**</span></span> | <span data-ttu-id="c0a94-130">**guid**</span><span class="sxs-lookup"><span data-stu-id="c0a94-130">**guid**</span></span> | <span data-ttu-id="c0a94-131">Y</span><span class="sxs-lookup"><span data-stu-id="c0a94-131">Y</span></span>        | <span data-ttu-id="c0a94-132">Az ügyfélhez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="c0a94-132">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="c0a94-133">**előfizetés-azonosító**</span><span class="sxs-lookup"><span data-stu-id="c0a94-133">**subscription-id**</span></span>       | <span data-ttu-id="c0a94-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="c0a94-134">**guid**</span></span> | <span data-ttu-id="c0a94-135">Y</span><span class="sxs-lookup"><span data-stu-id="c0a94-135">Y</span></span>        | <span data-ttu-id="c0a94-136">Az előfizetéshez tartozó GUID.</span><span class="sxs-lookup"><span data-stu-id="c0a94-136">A GUID corresponding to the subscription.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="c0a94-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="c0a94-137">Request headers</span></span>

<span data-ttu-id="c0a94-138">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c0a94-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c0a94-139">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="c0a94-139">Request body</span></span>

<span data-ttu-id="c0a94-140">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="c0a94-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c0a94-141">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="c0a94-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/11f9bc2a-1f38-431c-a0b0-9455c6f5bbc0/subscriptions/3f15978e-005c-b763-bb78-2a8fab289c58/azureEntitlements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="c0a94-142">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="c0a94-142">REST response</span></span>

<span data-ttu-id="c0a94-143">Ha ez sikeres, ez a metódus [**AzureEntitlement**](subscription-resources.md#azureentitlement) -erőforrások gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="c0a94-143">If successful, this method returns a collection of [**AzureEntitlement**](subscription-resources.md#azureentitlement) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c0a94-144">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="c0a94-144">Response success and error codes</span></span>

<span data-ttu-id="c0a94-145">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="c0a94-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c0a94-146">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="c0a94-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c0a94-147">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c0a94-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c0a94-148">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="c0a94-148">Response example</span></span>

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
