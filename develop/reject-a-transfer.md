---
title: Átadás elutasítása
description: Hogyan utasítható el az előfizetések átadása egy ügyfél számára.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d09905979a89c9b2092462512c485524cd681d5f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445374"
---
# <a name="reject-a-transfer"></a><span data-ttu-id="63529-103">Átadás elutasítása</span><span class="sxs-lookup"><span data-stu-id="63529-103">Reject a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63529-104">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="63529-104">Prerequisites</span></span>

- <span data-ttu-id="63529-105">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="63529-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="63529-106">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="63529-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="63529-107">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63529-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="63529-108">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="63529-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="63529-109">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="63529-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="63529-110">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="63529-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="63529-111">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="63529-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="63529-112">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="63529-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="63529-113">Egy meglévő átvitel átvitelazonosítója.</span><span class="sxs-lookup"><span data-stu-id="63529-113">A transfer identifier for an existing transfer.</span></span>

## <a name="rest-request"></a><span data-ttu-id="63529-114">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="63529-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="63529-115">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="63529-115">Request syntax</span></span>

| <span data-ttu-id="63529-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="63529-116">Method</span></span>   | <span data-ttu-id="63529-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="63529-117">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="63529-118">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="63529-118">**PATCH**</span></span> | <span data-ttu-id="63529-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/transfers/{transfer-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="63529-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers/{transfer-id} HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="63529-120">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="63529-120">URI parameter</span></span>

<span data-ttu-id="63529-121">Az alábbi elérésiút-paraméterrel azonosíthatja az ügyfelet, és megadhatja az elfogadni kívánt átvitelt.</span><span class="sxs-lookup"><span data-stu-id="63529-121">Use the following path parameter to identify the customer and specify the transfer to be accepted.</span></span>

| <span data-ttu-id="63529-122">Név</span><span class="sxs-lookup"><span data-stu-id="63529-122">Name</span></span>            | <span data-ttu-id="63529-123">Típus</span><span class="sxs-lookup"><span data-stu-id="63529-123">Type</span></span>     | <span data-ttu-id="63529-124">Kötelező</span><span class="sxs-lookup"><span data-stu-id="63529-124">Required</span></span> | <span data-ttu-id="63529-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="63529-125">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="63529-126">**ügyfél-azonosító**</span><span class="sxs-lookup"><span data-stu-id="63529-126">**customer-id**</span></span> | <span data-ttu-id="63529-127">sztring</span><span class="sxs-lookup"><span data-stu-id="63529-127">string</span></span>   | <span data-ttu-id="63529-128">Igen</span><span class="sxs-lookup"><span data-stu-id="63529-128">Yes</span></span>      | <span data-ttu-id="63529-129">Egy GUID formátumú ügyfél-azonosító, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="63529-129">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="63529-130">**transfer-id (átviteli azonosító)**</span><span class="sxs-lookup"><span data-stu-id="63529-130">**transfer-id**</span></span> | <span data-ttu-id="63529-131">sztring</span><span class="sxs-lookup"><span data-stu-id="63529-131">string</span></span>   | <span data-ttu-id="63529-132">Igen</span><span class="sxs-lookup"><span data-stu-id="63529-132">Yes</span></span>      | <span data-ttu-id="63529-133">Az átvitelt azonosító GUID formátumú átviteli azonosító.</span><span class="sxs-lookup"><span data-stu-id="63529-133">A GUID formatted transfer-id that identifies the transfer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="63529-134">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="63529-134">Request headers</span></span>

<span data-ttu-id="63529-135">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="63529-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="63529-136">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="63529-136">Request body</span></span>

<span data-ttu-id="63529-137">Ez a táblázat a [kérés törzsében található TransferEntity](transfer-entity-resources.md) tulajdonságokat ismerteti.</span><span class="sxs-lookup"><span data-stu-id="63529-137">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="63529-138">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="63529-138">Property</span></span>              | <span data-ttu-id="63529-139">Típus</span><span class="sxs-lookup"><span data-stu-id="63529-139">Type</span></span>          | <span data-ttu-id="63529-140">Kötelező</span><span class="sxs-lookup"><span data-stu-id="63529-140">Required</span></span>  | <span data-ttu-id="63529-141">Leírás</span><span class="sxs-lookup"><span data-stu-id="63529-141">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="63529-142">id</span><span class="sxs-lookup"><span data-stu-id="63529-142">id</span></span>                    | <span data-ttu-id="63529-143">sztring</span><span class="sxs-lookup"><span data-stu-id="63529-143">string</span></span>        | <span data-ttu-id="63529-144">No</span><span class="sxs-lookup"><span data-stu-id="63529-144">No</span></span>    | <span data-ttu-id="63529-145">A transferEntity sikeres létrehozásakor megadott transferEntity azonosító.</span><span class="sxs-lookup"><span data-stu-id="63529-145">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="63529-146">status</span><span class="sxs-lookup"><span data-stu-id="63529-146">status</span></span>                | <span data-ttu-id="63529-147">sztring</span><span class="sxs-lookup"><span data-stu-id="63529-147">string</span></span>        | <span data-ttu-id="63529-148">No</span><span class="sxs-lookup"><span data-stu-id="63529-148">No</span></span>    | <span data-ttu-id="63529-149">A transferEntity állapota.</span><span class="sxs-lookup"><span data-stu-id="63529-149">The status of the transferEntity.</span></span> <span data-ttu-id="63529-150">Az átadás elutasításához az értéket "elutasításként" kell beállítani</span><span class="sxs-lookup"><span data-stu-id="63529-150">To reject a transfer, the value is to be set as "reject"</span></span>|

### <a name="request-example"></a><span data-ttu-id="63529-151">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="63529-151">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="63529-152">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="63529-152">REST response</span></span>

<span data-ttu-id="63529-153">Ha sikeres, ez a metódus visszaadja a válasz törzsében a megadott [TransferEntity](transfer-entity-resources.md) erőforrást.</span><span class="sxs-lookup"><span data-stu-id="63529-153">If successful, this method returns the populated [TransferEntity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="63529-154">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="63529-154">Response success and error codes</span></span>

<span data-ttu-id="63529-155">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="63529-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="63529-156">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="63529-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="63529-157">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="63529-157">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="63529-158">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="63529-158">Response example</span></span>

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
