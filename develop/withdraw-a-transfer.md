---
title: Átvitel visszavonása
description: Előfizetések létrehozott átvitelének visszavonása egy ügyfélre.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a9e1e2a33d21fc1338a36b8ac96b528e70b61c86
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767676"
---
# <a name="withdraw-a-transfer"></a><span data-ttu-id="5d092-103">Átvitel visszavonása</span><span class="sxs-lookup"><span data-stu-id="5d092-103">Withdraw a transfer</span></span>

<span data-ttu-id="5d092-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="5d092-104">**Applies to:**</span></span>

- <span data-ttu-id="5d092-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="5d092-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d092-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="5d092-106">Prerequisites</span></span>

- <span data-ttu-id="5d092-107">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="5d092-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5d092-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="5d092-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5d092-109">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5d092-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5d092-110">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="5d092-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5d092-111">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="5d092-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5d092-112">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="5d092-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5d092-113">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="5d092-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5d092-114">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5d092-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5d092-115">Egy meglévő átvitelhez tartozó adatátviteli azonosító.</span><span class="sxs-lookup"><span data-stu-id="5d092-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5d092-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="5d092-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5d092-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="5d092-117">Request syntax</span></span>

| <span data-ttu-id="5d092-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="5d092-118">Method</span></span>    | <span data-ttu-id="5d092-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="5d092-119">Request URI</span></span>                                                                                                 |
|-----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5d092-120">**TÖRLÉSE**</span><span class="sxs-lookup"><span data-stu-id="5d092-120">**DELETE**</span></span>| <span data-ttu-id="5d092-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers/{Transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5d092-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>      |

### <a name="uri-parameter"></a><span data-ttu-id="5d092-122">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="5d092-122">URI parameter</span></span>

<span data-ttu-id="5d092-123">Az ügyfél azonosításához használja a következő Path paramétert.</span><span class="sxs-lookup"><span data-stu-id="5d092-123">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="5d092-124">Név</span><span class="sxs-lookup"><span data-stu-id="5d092-124">Name</span></span>            | <span data-ttu-id="5d092-125">Típus</span><span class="sxs-lookup"><span data-stu-id="5d092-125">Type</span></span>     | <span data-ttu-id="5d092-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="5d092-126">Required</span></span> | <span data-ttu-id="5d092-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="5d092-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="5d092-128">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="5d092-128">**customer-id**</span></span> | <span data-ttu-id="5d092-129">sztring</span><span class="sxs-lookup"><span data-stu-id="5d092-129">string</span></span>   | <span data-ttu-id="5d092-130">Igen</span><span class="sxs-lookup"><span data-stu-id="5d092-130">Yes</span></span>      | <span data-ttu-id="5d092-131">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="5d092-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="5d092-132">**átvitel-azonosító**</span><span class="sxs-lookup"><span data-stu-id="5d092-132">**transfer-id**</span></span> | <span data-ttu-id="5d092-133">sztring</span><span class="sxs-lookup"><span data-stu-id="5d092-133">string</span></span>   | <span data-ttu-id="5d092-134">Igen</span><span class="sxs-lookup"><span data-stu-id="5d092-134">Yes</span></span>      | <span data-ttu-id="5d092-135">GUID formátumú átvitel-azonosító, amely azonosítja az átvitelt.</span><span class="sxs-lookup"><span data-stu-id="5d092-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="5d092-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="5d092-136">Request headers</span></span>

<span data-ttu-id="5d092-137">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5d092-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="5d092-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="5d092-138">Request example</span></span>

```http
DELETE /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
Connection: keep-alive
```

## <a name="rest-response"></a><span data-ttu-id="5d092-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="5d092-139">REST response</span></span>

<span data-ttu-id="5d092-140">Ha ez sikeres, a metódus nem ad vissza tartalmat (204).</span><span class="sxs-lookup"><span data-stu-id="5d092-140">If successful, this method returns No Content (204).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5d092-141">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="5d092-141">Response success and error codes</span></span>

<span data-ttu-id="5d092-142">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="5d092-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5d092-143">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="5d092-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5d092-144">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5d092-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5d092-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="5d092-145">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 9041d76d-8915-43a8-8e82-00ca46a1a73d
MS-RequestId: cdf6e25c-7b32-4cc3-d8bc-53e0b37eebd8
Date: Tue, 24 Mar 2020 23:44:06 GMT
```
