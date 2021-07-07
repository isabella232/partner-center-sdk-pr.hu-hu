---
title: Előfizetések átvitelének elfogadása
description: Megtudhatja, hogyan használhatja Partnerközpont REST API ügyfél számára az előfizetések átvitelének elfogadására. TARTALMAZZA a REST-kérések szintaxisát, a fejléceket és a REST-válaszokat.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 762f2106d6173e352bec11936c96bc3a9c9f89cb
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025751"
---
# <a name="accept-a-transfer-of-subscriptions-for-a-customer-using-partner-center-rest-apis"></a><span data-ttu-id="a3af4-104">Előfizetések átadásának elfogadása egy ügyfél számára Partnerközpont REST API-k használatával</span><span class="sxs-lookup"><span data-stu-id="a3af4-104">Accept a transfer of subscriptions for a customer using Partner Center REST APIs</span></span>

<span data-ttu-id="a3af4-105">Ez a cikk azt REST API be, Partnerközpont hogyan fogadhatja el az előfizetések átadását egy ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="a3af4-105">This article covers how to use the REST API in Partner Center to accept the transfer of subscriptions for a customer.</span></span> <span data-ttu-id="a3af4-106">A példa REST-szintaxist, fejléceket és REST-válaszokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="a3af4-106">The example includes REST syntax, headers, and REST responses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3af4-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a3af4-107">Prerequisites</span></span>

- <span data-ttu-id="a3af4-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a3af4-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a3af4-109">Ez a forgatókönyv támogatja az önálló alkalmazás- és app+felhasználói hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="a3af4-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a3af4-110">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a3af4-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a3af4-111">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="a3af4-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a3af4-112">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a3af4-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a3af4-113">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="a3af4-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a3af4-114">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="a3af4-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a3af4-115">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a3af4-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a3af4-116">Egy meglévő átvitel átviteli azonosítója.</span><span class="sxs-lookup"><span data-stu-id="a3af4-116">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a3af4-117">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="a3af4-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a3af4-118">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="a3af4-118">Request syntax</span></span>

| <span data-ttu-id="a3af4-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="a3af4-119">Method</span></span>   | <span data-ttu-id="a3af4-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a3af4-120">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a3af4-121">**Post**</span><span class="sxs-lookup"><span data-stu-id="a3af4-121">**POST**</span></span> | <span data-ttu-id="a3af4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/transfers/{transfer-id}/accept HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a3af4-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id}/accept HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="a3af4-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a3af4-123">URI parameter</span></span>

<span data-ttu-id="a3af4-124">Az alábbi elérésiút-paraméterrel azonosíthatja az ügyfelet, és megadhatja az elfogadni kívánt átvitelt.</span><span class="sxs-lookup"><span data-stu-id="a3af4-124">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="a3af4-125">Név</span><span class="sxs-lookup"><span data-stu-id="a3af4-125">Name</span></span>            | <span data-ttu-id="a3af4-126">Típus</span><span class="sxs-lookup"><span data-stu-id="a3af4-126">Type</span></span>     | <span data-ttu-id="a3af4-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a3af4-127">Required</span></span> | <span data-ttu-id="a3af4-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="a3af4-128">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="a3af4-129">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="a3af4-129">**customer-id**</span></span> | <span data-ttu-id="a3af4-130">sztring</span><span class="sxs-lookup"><span data-stu-id="a3af4-130">string</span></span>   | <span data-ttu-id="a3af4-131">Igen</span><span class="sxs-lookup"><span data-stu-id="a3af4-131">Yes</span></span>      | <span data-ttu-id="a3af4-132">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="a3af4-132">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="a3af4-133">**átviteli azonosító**</span><span class="sxs-lookup"><span data-stu-id="a3af4-133">**transfer-id**</span></span> | <span data-ttu-id="a3af4-134">sztring</span><span class="sxs-lookup"><span data-stu-id="a3af4-134">string</span></span>   | <span data-ttu-id="a3af4-135">Igen</span><span class="sxs-lookup"><span data-stu-id="a3af4-135">Yes</span></span>      | <span data-ttu-id="a3af4-136">Az átvitelt azonosító GUID formátumú átviteli azonosító.</span><span class="sxs-lookup"><span data-stu-id="a3af4-136">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="a3af4-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a3af4-137">Request headers</span></span>

<span data-ttu-id="a3af4-138">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a3af4-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="a3af4-139">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a3af4-139">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a3af4-140">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a3af4-140">REST response</span></span>

<span data-ttu-id="a3af4-141">Ha ez a metódus sikeres, a válasz törzsében adja vissza a megadott [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="a3af4-141">If successful, this method returns the populated [TransferSubmitResult](transfer-entity-resources.md#transfersubmitresult) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a3af4-142">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a3af4-142">Response success and error codes</span></span>

<span data-ttu-id="a3af4-143">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="a3af4-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a3af4-144">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="a3af4-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a3af4-145">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a3af4-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a3af4-146">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a3af4-146">Response example</span></span>

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
