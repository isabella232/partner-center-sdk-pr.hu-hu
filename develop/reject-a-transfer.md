---
title: Átvitel elutasítása
description: Az előfizetések átvitelének elutasítása egy ügyfél számára.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e4a182ff92a21cf72ca1c2da9de7e211b433725f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767860"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="6f0fb-103">Átvitel elutasítása</span><span class="sxs-lookup"><span data-stu-id="6f0fb-103">Reject a transfer</span></span>

<span data-ttu-id="6f0fb-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="6f0fb-104">**Applies to:**</span></span>

- <span data-ttu-id="6f0fb-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="6f0fb-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f0fb-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="6f0fb-106">Prerequisites</span></span>

- <span data-ttu-id="6f0fb-107">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6f0fb-108">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6f0fb-109">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f0fb-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6f0fb-110">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="6f0fb-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6f0fb-111">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6f0fb-112">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6f0fb-113">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6f0fb-114">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f0fb-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6f0fb-115">Egy meglévő átvitelhez tartozó adatátviteli azonosító.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-115">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="6f0fb-116">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="6f0fb-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6f0fb-117">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="6f0fb-117">Request syntax</span></span>

| <span data-ttu-id="6f0fb-118">Metódus</span><span class="sxs-lookup"><span data-stu-id="6f0fb-118">Method</span></span>   | <span data-ttu-id="6f0fb-119">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="6f0fb-119">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6f0fb-120">**JAVÍTÁS**</span><span class="sxs-lookup"><span data-stu-id="6f0fb-120">**PATCH**</span></span> | <span data-ttu-id="6f0fb-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Transfers/{Transfer-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6f0fb-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="6f0fb-122">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="6f0fb-122">URI parameter</span></span>

<span data-ttu-id="6f0fb-123">A következő Path paraméter használatával azonosíthatja az ügyfelet, és megadhatja az elfogadásra váró átvitelt.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-123">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="6f0fb-124">Név</span><span class="sxs-lookup"><span data-stu-id="6f0fb-124">Name</span></span>            | <span data-ttu-id="6f0fb-125">Típus</span><span class="sxs-lookup"><span data-stu-id="6f0fb-125">Type</span></span>     | <span data-ttu-id="6f0fb-126">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6f0fb-126">Required</span></span> | <span data-ttu-id="6f0fb-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="6f0fb-127">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="6f0fb-128">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="6f0fb-128">**customer-id**</span></span> | <span data-ttu-id="6f0fb-129">sztring</span><span class="sxs-lookup"><span data-stu-id="6f0fb-129">string</span></span>   | <span data-ttu-id="6f0fb-130">Igen</span><span class="sxs-lookup"><span data-stu-id="6f0fb-130">Yes</span></span>      | <span data-ttu-id="6f0fb-131">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-131">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="6f0fb-132">**átvitel-azonosító**</span><span class="sxs-lookup"><span data-stu-id="6f0fb-132">**transfer-id**</span></span> | <span data-ttu-id="6f0fb-133">sztring</span><span class="sxs-lookup"><span data-stu-id="6f0fb-133">string</span></span>   | <span data-ttu-id="6f0fb-134">Igen</span><span class="sxs-lookup"><span data-stu-id="6f0fb-134">Yes</span></span>      | <span data-ttu-id="6f0fb-135">GUID formátumú átvitel-azonosító, amely azonosítja az átvitelt.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-135">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="6f0fb-136">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="6f0fb-136">Request headers</span></span>

<span data-ttu-id="6f0fb-137">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6f0fb-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6f0fb-138">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="6f0fb-138">Request body</span></span>

<span data-ttu-id="6f0fb-139">Ez a táblázat a kérelem törzsének [TransferEntity](transfer-entity-resources.md) tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-139">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="6f0fb-140">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="6f0fb-140">Property</span></span>              | <span data-ttu-id="6f0fb-141">Típus</span><span class="sxs-lookup"><span data-stu-id="6f0fb-141">Type</span></span>          | <span data-ttu-id="6f0fb-142">Kötelező</span><span class="sxs-lookup"><span data-stu-id="6f0fb-142">Required</span></span>  | <span data-ttu-id="6f0fb-143">Leírás</span><span class="sxs-lookup"><span data-stu-id="6f0fb-143">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="6f0fb-144">id</span><span class="sxs-lookup"><span data-stu-id="6f0fb-144">id</span></span>                    | <span data-ttu-id="6f0fb-145">sztring</span><span class="sxs-lookup"><span data-stu-id="6f0fb-145">string</span></span>        | <span data-ttu-id="6f0fb-146">No</span><span class="sxs-lookup"><span data-stu-id="6f0fb-146">No</span></span>    | <span data-ttu-id="6f0fb-147">A transferEntity sikeres létrehozásakor megadott transferEntity-azonosító.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-147">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="6f0fb-148">status</span><span class="sxs-lookup"><span data-stu-id="6f0fb-148">status</span></span>                | <span data-ttu-id="6f0fb-149">sztring</span><span class="sxs-lookup"><span data-stu-id="6f0fb-149">string</span></span>        | <span data-ttu-id="6f0fb-150">No</span><span class="sxs-lookup"><span data-stu-id="6f0fb-150">No</span></span>    | <span data-ttu-id="6f0fb-151">A transferEntity állapota.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-151">The status of the transferEntity.</span></span> <span data-ttu-id="6f0fb-152">Az átvitel elutasításához az értéket "elutasítás" értékre kell állítani</span><span class="sxs-lookup"><span data-stu-id="6f0fb-152">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="6f0fb-153">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="6f0fb-153">Request example</span></span>

```http
PATCH /v1/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
Connection: keep-alive
Content-Length: 63

{"id":"ac4a9d22-ba07-444e-890f-cfe084eed498","status":"reject"}

```

## <a name="rest-response"></a><span data-ttu-id="6f0fb-154">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="6f0fb-154">REST response</span></span>

<span data-ttu-id="6f0fb-155">Ha ez sikeres, ez a metódus a válasz törzsében lévő [TransferEntity](transfer-entity-resources.md) -erőforrást adja vissza.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-155">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6f0fb-156">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="6f0fb-156">Response success and error codes</span></span>

<span data-ttu-id="6f0fb-157">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6f0fb-158">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="6f0fb-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6f0fb-159">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6f0fb-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6f0fb-160">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="6f0fb-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1069
Content-Type: application/json; charset=utf-8
MS-CorrelationId: efa4c6f5-153a-4f76-e458-1375e181cc14
MS-RequestId: 5b46e795-b661-428e-a2e7-f208b8d0d25c
X-Locale: en-US
Date: Fri, 27 Mar 2020 17:50:33 GMT

{
  "id": "ac4a9d22-ba07-444e-890f-cfe084eed498",
  "status": "Reject",
  "createdTime": "2020-03-25T22:05:25.1057725Z",
  "lastModifiedTime": "2020-03-27T17:50:32Z",
  "customerTenantId": "b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0",
  "partnertenantid": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "sourcePartnerName": "Test_Test_09092019GBL",
  "sourcePartnerTenantId": "7c8db11f-1e5e-4472-8386-f0b627d1f3e1",
  "targetPartnerName": "Test_Test_09032019GBL",
  "targetPartnerTenantId": "3a9a35ce-d5be-4814-ab58-4451c36fe157",
  "lastModifiedUser": "01a7548d-1136-4cf0-ba9a-300f921ffb22",
  "lineItems": [
    {
      "id": 0,
      "subscriptionId": "1151B8CE-125C-49D7-8C48-E62FC9101B77",
      "offerId": "13D32E13-A1B0-400D-96C0-4EAAA14DCED5",
      "billingCycle": "monthly",
      "friendlyName": "Dynamics 365 for Supply Chain Management Attach to Qualifying Dynamics 365 Base Offer (Qualified Offer)",
      "quantity": 20,
      "partnerIdOnRecord": "5139005",
      "addonItems": [

      ]
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/b67f0b00-f9e8-4c57-bcb5-0b8b95c6ccf0/transfers/ac4a9d22-ba07-444e-890f-cfe084eed498",
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
