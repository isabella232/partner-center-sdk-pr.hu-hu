---
title: Adatátviteli adatok beolvasása azonosító alapján
description: Az előfizetések átvitelének részletei az ügyfelek számára.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c39e9483f1e51469981b0d6fa2541a6372ff2dac
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767815"
---
# <a name="get-transfer-details-by-id"></a><span data-ttu-id="a0814-103">Adatátviteli adatok beolvasása azonosító alapján</span><span class="sxs-lookup"><span data-stu-id="a0814-103">Get transfer details by id</span></span>

<span data-ttu-id="a0814-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="a0814-104">**Applies to:**</span></span>

- <span data-ttu-id="a0814-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="a0814-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0814-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="a0814-106">Prerequisites</span></span>

- <span data-ttu-id="a0814-107">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="a0814-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a0814-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="a0814-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a0814-109">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a0814-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a0814-110">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="a0814-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a0814-111">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="a0814-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a0814-112">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="a0814-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a0814-113">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="a0814-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a0814-114">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a0814-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a0814-115">Egy meglévő átvitelhez tartozó adatátviteli azonosító.</span><span class="sxs-lookup"><span data-stu-id="a0814-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a0814-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="a0814-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a0814-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="a0814-117">Request syntax</span></span>

| <span data-ttu-id="a0814-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="a0814-118">Method</span></span>   | <span data-ttu-id="a0814-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="a0814-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0814-120">**GET**</span><span class="sxs-lookup"><span data-stu-id="a0814-120">**GET**</span></span> | <span data-ttu-id="a0814-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers/{Transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a0814-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="a0814-122">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="a0814-122">URI parameter</span></span>

<span data-ttu-id="a0814-123">A következő Path paraméter használatával azonosíthatja az ügyfelet, és megadhatja az elfogadásra váró átvitelt.</span><span class="sxs-lookup"><span data-stu-id="a0814-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="a0814-124">Név</span><span class="sxs-lookup"><span data-stu-id="a0814-124">Name</span></span>            | <span data-ttu-id="a0814-125">Típus</span><span class="sxs-lookup"><span data-stu-id="a0814-125">Type</span></span>     | <span data-ttu-id="a0814-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="a0814-126">Required</span></span> | <span data-ttu-id="a0814-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="a0814-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="a0814-128">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="a0814-128">**customer-id**</span></span> | <span data-ttu-id="a0814-129">sztring</span><span class="sxs-lookup"><span data-stu-id="a0814-129">string</span></span>   | <span data-ttu-id="a0814-130">Igen</span><span class="sxs-lookup"><span data-stu-id="a0814-130">Yes</span></span>      | <span data-ttu-id="a0814-131">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="a0814-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="a0814-132">**átvitel-azonosító**</span><span class="sxs-lookup"><span data-stu-id="a0814-132">**transfer-id**</span></span> | <span data-ttu-id="a0814-133">sztring</span><span class="sxs-lookup"><span data-stu-id="a0814-133">string</span></span>   | <span data-ttu-id="a0814-134">Igen</span><span class="sxs-lookup"><span data-stu-id="a0814-134">Yes</span></span>      | <span data-ttu-id="a0814-135">GUID formátumú átvitel-azonosító, amely azonosítja az átvitelt.</span><span class="sxs-lookup"><span data-stu-id="a0814-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="a0814-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="a0814-136">Request headers</span></span>

<span data-ttu-id="a0814-137">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a0814-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-example"></a><span data-ttu-id="a0814-138">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="a0814-138">Request example</span></span>

```http
GET /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556 HTTP/1.1
Authorization: Bearer <token>
Connection: keep-alive
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
Accept: application/json
```

## <a name="rest-response"></a><span data-ttu-id="a0814-139">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="a0814-139">REST response</span></span>

<span data-ttu-id="a0814-140">Ha ez sikeres, ez a metódus a válasz törzsében lévő [TransferEntity](transfer-entity-resources.md) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="a0814-140">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a0814-141">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="a0814-141">Response success and error codes</span></span>

<span data-ttu-id="a0814-142">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="a0814-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a0814-143">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="a0814-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a0814-144">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a0814-144">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a0814-145">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="a0814-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1501
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 68eacc61-971c-43b0-c06f-2622bf79b090
MS-RequestId: 0d61b5ce-b396-4f5e-a50b-e8779d0d23cc
X-Locale: en-US
Date: Fri, 27 Mar 2020 18:25:25 GMT

{
  "id": "46e8ed67-8adf-4f65-b3d8-d31318080556",
  "status": "Active",
  "createdTime": "2020-03-27T18:22:33.2875302Z",
  "lastModifiedTime": "2020-03-27T18:22:33Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "edc0524d-2e42-4619-af7e-349c015cfdfd",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "75B71186-73C3-45B4-A403-281C0D7EB032",
      "offerId": "F72752C8-3E37-4C9B-A1A0-69E8442068DC",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central Team Member",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 1,
      "subscriptionId": "1FB4CB0A-EB79-4300-9E87-7D486054888A",
      "offerId": "88F9EB8A-0636-45E8-A601-553E0A48AA9E",
      "billingCycle": "annual",
      "friendlyName": "Dynamics 365 Business Central External Accountant",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    },
    {
      "id": 2,
      "subscriptionId": "08AB3010-B647-402E-8955-B6C0FB364D8F",
      "offerId": "4D8F3B90-29B3-4E7B-B37C-4A435DDEF1D9",
      "billingCycle": "annual",
      "friendlyName": "Common Area Phone",
      "quantity": 1,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/46e8ed67-8adf-4f65-b3d8-d31318080556",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "TransferEntity"
  }
}

```
