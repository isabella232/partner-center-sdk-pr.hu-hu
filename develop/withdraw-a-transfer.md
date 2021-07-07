---
title: Átadás kiesését
description: Hogyan lehet létrehozni az előfizetések ügyfél számára létrehozott átvitelét.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3c15cf09b4e466e178c7afb5f9d324fe1199418e
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445204"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="fc041-103">Átadás kiesését</span><span class="sxs-lookup"><span data-stu-id="fc041-103">Withdraw a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc041-104">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="fc041-104">Prerequisites</span></span>

- <span data-ttu-id="fc041-105">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fc041-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fc041-106">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="fc041-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fc041-107">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc041-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fc041-108">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fc041-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fc041-109">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="fc041-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fc041-110">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="fc041-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fc041-111">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="fc041-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fc041-112">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fc041-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fc041-113">Egy meglévő átvitel átvitelazonosítója.</span><span class="sxs-lookup"><span data-stu-id="fc041-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="fc041-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="fc041-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fc041-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="fc041-115">Request syntax</span></span>

| <span data-ttu-id="fc041-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="fc041-116">Method</span></span>    | <span data-ttu-id="fc041-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="fc041-117">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fc041-118">**Töröl**</span><span class="sxs-lookup"><span data-stu-id="fc041-118">**DELETE**</span></span>| <span data-ttu-id="fc041-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fc041-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="fc041-120">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="fc041-120">URI parameter</span></span>

<span data-ttu-id="fc041-121">Az ügyfél azonosításához használja a következő path paramétert.</span><span class="sxs-lookup"><span data-stu-id="fc041-121">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="fc041-122">Név</span><span class="sxs-lookup"><span data-stu-id="fc041-122">Name</span></span>            | <span data-ttu-id="fc041-123">Típus</span><span class="sxs-lookup"><span data-stu-id="fc041-123">Type</span></span>     | <span data-ttu-id="fc041-124">Kötelező</span><span class="sxs-lookup"><span data-stu-id="fc041-124">Required</span></span> | <span data-ttu-id="fc041-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="fc041-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="fc041-126">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="fc041-126">**customer-id**</span></span> | <span data-ttu-id="fc041-127">sztring</span><span class="sxs-lookup"><span data-stu-id="fc041-127">string</span></span>   | <span data-ttu-id="fc041-128">Igen</span><span class="sxs-lookup"><span data-stu-id="fc041-128">Yes</span></span>      | <span data-ttu-id="fc041-129">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="fc041-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="fc041-130">**transfer-id (átviteli azonosító)**</span><span class="sxs-lookup"><span data-stu-id="fc041-130">**transfer-id**</span></span> | <span data-ttu-id="fc041-131">sztring</span><span class="sxs-lookup"><span data-stu-id="fc041-131">string</span></span>   | <span data-ttu-id="fc041-132">Igen</span><span class="sxs-lookup"><span data-stu-id="fc041-132">Yes</span></span>      | <span data-ttu-id="fc041-133">Az átvitelt azonosító GUID formátumú átviteli azonosító.</span><span class="sxs-lookup"><span data-stu-id="fc041-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="fc041-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="fc041-134">Request headers</span></span>

<span data-ttu-id="fc041-135">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fc041-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="fc041-136">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="fc041-136">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="fc041-137">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="fc041-137">REST response</span></span>

<span data-ttu-id="fc041-138">Ha ez a módszer sikeres, akkor a Nincs tartalom (204) értéket adja vissza.</span><span class="sxs-lookup"><span data-stu-id="fc041-138">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fc041-139">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="fc041-139">Response success and error codes</span></span>

<span data-ttu-id="fc041-140">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="fc041-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fc041-141">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="fc041-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fc041-142">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fc041-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fc041-143">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="fc041-143">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
