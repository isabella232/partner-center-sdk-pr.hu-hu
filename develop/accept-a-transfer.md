---
title: Előfizetések átvitelének elfogadása
description: Megtudhatja, hogyan használhatja a partner Center REST API az előfizetések elfogadására az ügyfelek számára. A REST-kérelmek szintaxisát, fejléceit és REST-válaszokat tartalmaz.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd9a6788b3dd022470e516ba928a6cd873970e53
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768516"
---
# <a name="accept-a-transfer-of-subscriptions-for-a-customer-using-partner-center-rest-apis"></a><span data-ttu-id="d2cbb-104">Előfizetés elfogadása egy ügyfél számára a partner Center REST API-k használatával</span><span class="sxs-lookup"><span data-stu-id="d2cbb-104">Accept a transfer of subscriptions for a customer using Partner Center REST APIs</span></span>

<span data-ttu-id="d2cbb-105">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="d2cbb-105">**Applies to:**</span></span>

- <span data-ttu-id="d2cbb-106">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="d2cbb-106">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2cbb-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="d2cbb-107">Prerequisites</span></span>

- <span data-ttu-id="d2cbb-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d2cbb-109">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d2cbb-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d2cbb-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d2cbb-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="d2cbb-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d2cbb-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d2cbb-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d2cbb-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d2cbb-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d2cbb-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d2cbb-116">Egy meglévő átvitelhez tartozó adatátviteli azonosító.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-116">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="d2cbb-117">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="d2cbb-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d2cbb-118">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="d2cbb-118">Request syntax</span></span>

| <span data-ttu-id="d2cbb-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="d2cbb-119">Method</span></span>   | <span data-ttu-id="d2cbb-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="d2cbb-120">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d2cbb-121">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="d2cbb-121">**POST**</span></span> | <span data-ttu-id="d2cbb-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers/{Transfer-ID}/Accept http/1.1</span><span class="sxs-lookup"><span data-stu-id="d2cbb-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id}/accept HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="d2cbb-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="d2cbb-123">URI parameter</span></span>

<span data-ttu-id="d2cbb-124">A következő Path paraméter használatával azonosíthatja az ügyfelet, és megadhatja az elfogadásra váró átvitelt.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-124">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="d2cbb-125">Név</span><span class="sxs-lookup"><span data-stu-id="d2cbb-125">Name</span></span>            | <span data-ttu-id="d2cbb-126">Típus</span><span class="sxs-lookup"><span data-stu-id="d2cbb-126">Type</span></span>     | <span data-ttu-id="d2cbb-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="d2cbb-127">Required</span></span> | <span data-ttu-id="d2cbb-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="d2cbb-128">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="d2cbb-129">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="d2cbb-129">**customer-id**</span></span> | <span data-ttu-id="d2cbb-130">sztring</span><span class="sxs-lookup"><span data-stu-id="d2cbb-130">string</span></span>   | <span data-ttu-id="d2cbb-131">Igen</span><span class="sxs-lookup"><span data-stu-id="d2cbb-131">Yes</span></span>      | <span data-ttu-id="d2cbb-132">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-132">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="d2cbb-133">**átvitel-azonosító**</span><span class="sxs-lookup"><span data-stu-id="d2cbb-133">**transfer-id**</span></span> | <span data-ttu-id="d2cbb-134">sztring</span><span class="sxs-lookup"><span data-stu-id="d2cbb-134">string</span></span>   | <span data-ttu-id="d2cbb-135">Igen</span><span class="sxs-lookup"><span data-stu-id="d2cbb-135">Yes</span></span>      | <span data-ttu-id="d2cbb-136">GUID formátumú átvitel-azonosító, amely azonosítja az átvitelt.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-136">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="d2cbb-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="d2cbb-137">Request headers</span></span>

<span data-ttu-id="d2cbb-138">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d2cbb-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="d2cbb-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="d2cbb-139">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers/aa2bddb6-9cc8-4949-80fe-a37d5e0a13ba/accept HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0

```

## <a name="rest-response"></a><span data-ttu-id="d2cbb-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="d2cbb-140">REST response</span></span>

<span data-ttu-id="d2cbb-141">Ha ez sikeres, ez a metódus a válasz törzsében lévő [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-141">If successful, this method returns the populated [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d2cbb-142">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="d2cbb-142">Response success and error codes</span></span>

<span data-ttu-id="d2cbb-143">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d2cbb-144">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="d2cbb-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d2cbb-145">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d2cbb-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d2cbb-146">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="d2cbb-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3389
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4827b753-8541-428b-8c90-059b6b4851bd
MS-RequestId: 8389053b-731c-4261-9899-1583d7859153
X-Locale: en-US
Date: Wed, 25 Mar 2020 19:13:06 GMT

{
  "orders": [
    {
      "id": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "alternateId": "21b92393-ffce-4bc7-87c5-62cfa897d8f9",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "5344C201-3099-44E5-B333-C3EB0401EDE0",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Customer Engagement Plan (36 mo)",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:23.183+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/21b92393-ffce-4bc7-87c5-62cfa897d8f9",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6IjIxYjkyMzkzLWZmY2UtNGJjNy04N2M1LTYyY2ZhODk3ZDhmOSIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    },
    {
      "id": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "alternateId": "7414b8ea-c167-4cc4-bc8e-b43efc177a46",
      "referenceCustomerId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
      "billingCycle": "annual",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "1A90EE13-2CB4-4785-BB0F-542813F00A37",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Dynamics 365 Business Central Essential",
          "quantity": 1,
          "partnerIdOnRecord": "5139005",
          "links": {
          }
        }
      ],
      "creationDate": "2020-03-25T22:24:34.59+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {
        "self": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "GET",
          "headers": [ ]
        },
        "patchOperation": {
          "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/orders/7414b8ea-c167-4cc4-bc8e-b43efc177a46",
          "method": "PATCH",
          "headers": [ ]
        }
      },
      "attributes": {
        "etag": "eyJpZCI6Ijc0MTRiOGVhLWMxNjctNGNjNC1iYzhlLWI0M2VmYzE3N2E0NiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
      }
    }
  ],
  "transferErrors": [
    {
      "transferGroupId": "1",
      "lineItems": [
        {
          "id": 1,
          "subscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "entitlementId": "637FF8F6-D842-4573-8DA8-89765356CD1A",
          "offerId": "A4179D30-CC09-49F0-977E-DC2CB70B874F",
          "friendlyName": "Project Online Essentials",
          "quantity": 1,
          "transferGroupId": "1",
          "addonItems": [ ],
          "partnerIdOnRecord": "5139005",
          "billingCycle": "annual",
          "sourceSubscriptionId": "637FF8F6-D842-4573-8DA8-89765356CD1A"
        }
      ],
      "code": 900103,
      "description": "Subscription SyncState must be SyncComplete for the Subscription to be a source in a Subscription Ownership Transfer. Subscription: 637ff8f6-d842-4573-8da8-89765356cd1a, current state: None",
      "attributes": {
        "objectType": "TransferError"
      }
    }
  ],
  "attributes": {
    "objectType": "TransferSubmitResult"
  }
}
```
