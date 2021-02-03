---
title: Ügyfél közvetlen aláírási állapotának beolvasása a Microsoft ügyfél-szerződéshez.
description: A DirectSignedCustomerAgreementStatus-erőforrás segítségével lekérheti a Microsoft ügyfél-szerződés közvetlen aláírásának (közvetlen elfogadásának) állapotát.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767700"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="7726c-103">Ügyfél közvetlen aláírása (közvetlen elfogadás) állapotának lekérése a Microsoft ügyfél-szerződésből</span><span class="sxs-lookup"><span data-stu-id="7726c-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="7726c-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="7726c-104">**Applies to:**</span></span>

- <span data-ttu-id="7726c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="7726c-105">Partner Center</span></span>

<span data-ttu-id="7726c-106">A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános felhőben támogatja a partner Center.</span><span class="sxs-lookup"><span data-stu-id="7726c-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="7726c-107">Ez az erőforrás *nem alkalmazható* a következőre:</span><span class="sxs-lookup"><span data-stu-id="7726c-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="7726c-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="7726c-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7726c-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="7726c-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7726c-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="7726c-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7726c-111">Ez a cikk azt ismerteti, hogyan kérheti le a Microsoft ügyfél-szerződés közvetlen elfogadásának állapotát.</span><span class="sxs-lookup"><span data-stu-id="7726c-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7726c-112">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="7726c-112">REST request</span></span>

<span data-ttu-id="7726c-113">Az ügyfél Microsoft-szerződéssel kapcsolatos közvetlen elfogadásának állapotának lekéréséhez hozzon létre egy REST-kérelmet az ügyfél [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="7726c-113">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7726c-114">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7726c-114">Request syntax</span></span>

<span data-ttu-id="7726c-115">Használja a következő kérelem szintaxisát:</span><span class="sxs-lookup"><span data-stu-id="7726c-115">Use the following request syntax:</span></span>

| <span data-ttu-id="7726c-116">Metódus</span><span class="sxs-lookup"><span data-stu-id="7726c-116">Method</span></span> | <span data-ttu-id="7726c-117">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7726c-117">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7726c-118">GET</span><span class="sxs-lookup"><span data-stu-id="7726c-118">GET</span></span>    | <span data-ttu-id="7726c-119">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="7726c-119">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="7726c-120">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7726c-120">URI parameters</span></span>

<span data-ttu-id="7726c-121">A kérelemhez a következő URI-paramétereket használhatja:</span><span class="sxs-lookup"><span data-stu-id="7726c-121">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="7726c-122">Név</span><span class="sxs-lookup"><span data-stu-id="7726c-122">Name</span></span>             | <span data-ttu-id="7726c-123">Típus</span><span class="sxs-lookup"><span data-stu-id="7726c-123">Type</span></span> | <span data-ttu-id="7726c-124">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7726c-124">Required</span></span> | <span data-ttu-id="7726c-125">Leírás</span><span class="sxs-lookup"><span data-stu-id="7726c-125">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="7726c-126">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="7726c-126">customer-tenant-id</span></span> | <span data-ttu-id="7726c-127">GUID</span><span class="sxs-lookup"><span data-stu-id="7726c-127">GUID</span></span> | <span data-ttu-id="7726c-128">Igen</span><span class="sxs-lookup"><span data-stu-id="7726c-128">Yes</span></span> | <span data-ttu-id="7726c-129">Az érték egy GUID-formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél BÉRLŐi azonosítójának megadását.</span><span class="sxs-lookup"><span data-stu-id="7726c-129">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7726c-130">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7726c-130">Request headers</span></span>

<span data-ttu-id="7726c-131">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7726c-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7726c-132">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7726c-132">Request body</span></span>

<span data-ttu-id="7726c-133">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7726c-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7726c-134">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7726c-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="7726c-135">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7726c-135">REST response</span></span>

<span data-ttu-id="7726c-136">Ha ez sikeres, ez a metódus egy [ **DirectSignedCustomerAgreementStatus** -erőforrást](./customer-agreement-direct-sign-status-resource.md) ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="7726c-136">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="7726c-137">Az erőforrás rendelkezik egy **isSigned** tulajdonsággal, amely az ügyfél közvetlen aláírása (közvetlen elfogadás) állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="7726c-137">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="7726c-138">A **true** érték azt jelzi, hogy a szerződés aláírása (elfogadva) közvetlenül az ügyfél által történt.</span><span class="sxs-lookup"><span data-stu-id="7726c-138">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="7726c-139">A **false** érték azt jelzi, hogy a szerződés *nem* lett aláírva (elfogadva) közvetlenül az ügyfél által.</span><span class="sxs-lookup"><span data-stu-id="7726c-139">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7726c-140">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7726c-140">Response success and error codes</span></span>

<span data-ttu-id="7726c-141">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="7726c-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="7726c-142">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="7726c-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7726c-143">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="7726c-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7726c-144">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7726c-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
