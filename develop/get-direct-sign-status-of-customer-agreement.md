---
title: Ügyfél közvetlen aláírási állapotának beolvasása a Microsoft ügyfél-szerződéshez.
description: A DirectSignedCustomerAgreementStatus-erőforrás segítségével lekérheti a Microsoft ügyfél-szerződés közvetlen aláírásának (közvetlen elfogadásának) állapotát.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030556"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="b352c-103">Ügyfél közvetlen aláírása (közvetlen elfogadás) állapotának lekérése a Microsoft ügyfél-szerződésből</span><span class="sxs-lookup"><span data-stu-id="b352c-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="b352c-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="b352c-104">**Applies to:**</span></span>

- <span data-ttu-id="b352c-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b352c-105">Partner Center</span></span>

<span data-ttu-id="b352c-106">A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános felhőben támogatja a partner Center.</span><span class="sxs-lookup"><span data-stu-id="b352c-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="b352c-107">Ez az erőforrás *nem alkalmazható* a következőre:</span><span class="sxs-lookup"><span data-stu-id="b352c-107">This resource is *not applicable* to:</span></span>

- <span data-ttu-id="b352c-108">A 21Vianet által üzemeltetett Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b352c-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b352c-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b352c-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b352c-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="b352c-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b352c-111">Ez a cikk azt ismerteti, hogyan kérheti le a Microsoft ügyfél-szerződés közvetlen elfogadásának állapotát.</span><span class="sxs-lookup"><span data-stu-id="b352c-111">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b352c-112">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b352c-112">Prerequisites</span></span>

- <span data-ttu-id="b352c-113">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b352c-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b352c-114">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b352c-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b352c-115">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b352c-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b352c-116">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="b352c-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b352c-117">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="b352c-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b352c-118">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b352c-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b352c-119">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="b352c-119">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b352c-120">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b352c-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b352c-121">C\#</span><span class="sxs-lookup"><span data-stu-id="b352c-121">C\#</span></span>

<span data-ttu-id="b352c-122">Az ügyfél Microsoft-szerződéssel kapcsolatos közvetlen elfogadásának állapotának lekéréséhez hívja meg a [**IAggregatePartner. customers. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="b352c-122">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="b352c-123">Ezután használja a [**szerződések**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) tulajdonságot egy [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) -felület lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="b352c-123">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="b352c-124">Végül hívja `GetDirectSignedCustomerAgreementStatus()` meg vagy kérje `GetDirectSignedCustomerAgreementStatusAsync()` le az állapotot.</span><span class="sxs-lookup"><span data-stu-id="b352c-124">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="b352c-125">**Példa**: [konzolos minta alkalmazás](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span><span class="sxs-lookup"><span data-stu-id="b352c-125">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="b352c-126">**Projekt**: SdkSamples **osztály**: GetDirectSignedCustomerAgreementStatus. cs</span><span class="sxs-lookup"><span data-stu-id="b352c-126">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b352c-127">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b352c-127">REST request</span></span>

<span data-ttu-id="b352c-128">Az ügyfél Microsoft-szerződéssel kapcsolatos közvetlen elfogadásának állapotának lekéréséhez hozzon létre egy REST-kérelmet az ügyfél [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="b352c-128">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b352c-129">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b352c-129">Request syntax</span></span>

<span data-ttu-id="b352c-130">Használja a következő kérelem szintaxisát:</span><span class="sxs-lookup"><span data-stu-id="b352c-130">Use the following request syntax:</span></span>

| <span data-ttu-id="b352c-131">Metódus</span><span class="sxs-lookup"><span data-stu-id="b352c-131">Method</span></span> | <span data-ttu-id="b352c-132">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b352c-132">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b352c-133">GET</span><span class="sxs-lookup"><span data-stu-id="b352c-133">GET</span></span>    | <span data-ttu-id="b352c-134">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directSignedMicrosoftCustomerAgreementStatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="b352c-134">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b352c-135">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="b352c-135">URI parameters</span></span>

<span data-ttu-id="b352c-136">A kérelemhez a következő URI-paramétereket használhatja:</span><span class="sxs-lookup"><span data-stu-id="b352c-136">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="b352c-137">Név</span><span class="sxs-lookup"><span data-stu-id="b352c-137">Name</span></span>             | <span data-ttu-id="b352c-138">Típus</span><span class="sxs-lookup"><span data-stu-id="b352c-138">Type</span></span> | <span data-ttu-id="b352c-139">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b352c-139">Required</span></span> | <span data-ttu-id="b352c-140">Leírás</span><span class="sxs-lookup"><span data-stu-id="b352c-140">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="b352c-141">ügyfél – bérlő – azonosító</span><span class="sxs-lookup"><span data-stu-id="b352c-141">customer-tenant-id</span></span> | <span data-ttu-id="b352c-142">GUID</span><span class="sxs-lookup"><span data-stu-id="b352c-142">GUID</span></span> | <span data-ttu-id="b352c-143">Igen</span><span class="sxs-lookup"><span data-stu-id="b352c-143">Yes</span></span> | <span data-ttu-id="b352c-144">Az érték egy GUID-formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél BÉRLŐi azonosítójának megadását.</span><span class="sxs-lookup"><span data-stu-id="b352c-144">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b352c-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b352c-145">Request headers</span></span>

<span data-ttu-id="b352c-146">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b352c-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b352c-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b352c-147">Request body</span></span>

<span data-ttu-id="b352c-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b352c-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b352c-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b352c-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="b352c-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b352c-150">REST response</span></span>

<span data-ttu-id="b352c-151">Ha ez sikeres, ez a metódus egy [ **DirectSignedCustomerAgreementStatus** -erőforrást](./customer-agreement-direct-sign-status-resource.md) ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="b352c-151">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="b352c-152">Az erőforrás rendelkezik egy **isSigned** tulajdonsággal, amely az ügyfél közvetlen aláírása (közvetlen elfogadás) állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="b352c-152">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="b352c-153">A **true** érték azt jelzi, hogy a szerződés aláírása (elfogadva) közvetlenül az ügyfél által történt.</span><span class="sxs-lookup"><span data-stu-id="b352c-153">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="b352c-154">A **false** érték azt jelzi, hogy a szerződés *nem* lett aláírva (elfogadva) közvetlenül az ügyfél által.</span><span class="sxs-lookup"><span data-stu-id="b352c-154">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b352c-155">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b352c-155">Response success and error codes</span></span>

<span data-ttu-id="b352c-156">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b352c-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="b352c-157">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b352c-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b352c-158">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="b352c-158">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b352c-159">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b352c-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
