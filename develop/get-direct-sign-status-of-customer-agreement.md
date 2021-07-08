---
title: Lekérte az ügyfél közvetlen aláírási állapotát a Microsoft Ügyfélszerződés.
description: A DirectSignedCustomerAgreementStatus erőforrás használatával lekértheti az ügyfél közvetlen aláírásának (közvetlen elfogadásának) állapotát a Microsoft Ügyfélszerződés.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: a17775614b4eb328514b2b32b4cac1e513019cff
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549178"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a><span data-ttu-id="7539a-103">Az ügyfél közvetlen aláírásának (közvetlen elfogadásának) állapotát Microsoft Ügyfélszerződés</span><span class="sxs-lookup"><span data-stu-id="7539a-103">Get the status of a customer's direct signing (direct acceptance) of Microsoft Customer Agreement</span></span>

<span data-ttu-id="7539a-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="7539a-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="7539a-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="7539a-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7539a-106">A **DirectSignedCustomerAgreementStatus** erőforrást jelenleg csak a Microsoft nyilvános Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="7539a-106">The **DirectSignedCustomerAgreementStatus** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

<span data-ttu-id="7539a-107">Ez a cikk azt ismerteti, hogyan lehet lekérni az ügyfél által a Microsoft Ügyfélszerződés.</span><span class="sxs-lookup"><span data-stu-id="7539a-107">This article explains how you can retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7539a-108">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="7539a-108">Prerequisites</span></span>

- <span data-ttu-id="7539a-109">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7539a-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7539a-110">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="7539a-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7539a-111">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7539a-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7539a-112">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="7539a-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7539a-113">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="7539a-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7539a-114">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="7539a-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7539a-115">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="7539a-115">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7539a-116">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7539a-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7539a-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7539a-117">C\#</span></span>

<span data-ttu-id="7539a-118">Az ügyfél általi közvetlen ügyfél-elfogadás állapotának Microsoft Ügyfélszerződés hívja meg az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="7539a-118">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier.</span></span> <span data-ttu-id="7539a-119">Ezután a [**Agreements tulajdonság**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) használatával lekér egy [**ICustomerAgreementCollection felületet.**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection)</span><span class="sxs-lookup"><span data-stu-id="7539a-119">Then use the [**Agreements**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) property to retrieve a [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) interface.</span></span> <span data-ttu-id="7539a-120">Végül hívja meg a `GetDirectSignedCustomerAgreementStatus()` vagy `GetDirectSignedCustomerAgreementStatusAsync()` a et az állapot lekérése.</span><span class="sxs-lookup"><span data-stu-id="7539a-120">Finally, call `GetDirectSignedCustomerAgreementStatus()` or `GetDirectSignedCustomerAgreementStatusAsync()` to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

<span data-ttu-id="7539a-121">**Minta:** [Konzol mintaalkalmazás.](https://github.com/microsoft/Partner-Center-DotNet-Samples)</span><span class="sxs-lookup"><span data-stu-id="7539a-121">**Sample**: [Console Sample App](https://github.com/microsoft/Partner-Center-DotNet-Samples).</span></span> <span data-ttu-id="7539a-122">**Project:** SdkSamples **osztály:** GetDirectSignedCustomerAgreementStatus.cs</span><span class="sxs-lookup"><span data-stu-id="7539a-122">**Project**: SdkSamples **Class**: GetDirectSignedCustomerAgreementStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7539a-123">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="7539a-123">REST request</span></span>

<span data-ttu-id="7539a-124">Az Microsoft Ügyfélszerződés ügyfél általi közvetlen elfogadás állapotának lekérésére hozzon létre egy REST-kérést, amely lekéri a [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) adatokat az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="7539a-124">To retrieve the status of a customer's direct acceptance of the Microsoft Customer Agreement, create a REST request to retrieve the [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) for the customer.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7539a-125">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="7539a-125">Request syntax</span></span>

<span data-ttu-id="7539a-126">Használja a következő kérésszintaxist:</span><span class="sxs-lookup"><span data-stu-id="7539a-126">Use the following request syntax:</span></span>

| <span data-ttu-id="7539a-127">Metódus</span><span class="sxs-lookup"><span data-stu-id="7539a-127">Method</span></span> | <span data-ttu-id="7539a-128">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="7539a-128">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7539a-129">GET</span><span class="sxs-lookup"><span data-stu-id="7539a-129">GET</span></span>    | <span data-ttu-id="7539a-130">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="7539a-130">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="7539a-131">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="7539a-131">URI parameters</span></span>

<span data-ttu-id="7539a-132">A kérelemhez a következő URI-paramétereket használhatja:</span><span class="sxs-lookup"><span data-stu-id="7539a-132">You can use the following URI parameters with your request:</span></span>

| <span data-ttu-id="7539a-133">Név</span><span class="sxs-lookup"><span data-stu-id="7539a-133">Name</span></span>             | <span data-ttu-id="7539a-134">Típus</span><span class="sxs-lookup"><span data-stu-id="7539a-134">Type</span></span> | <span data-ttu-id="7539a-135">Kötelező</span><span class="sxs-lookup"><span data-stu-id="7539a-135">Required</span></span> | <span data-ttu-id="7539a-136">Leírás</span><span class="sxs-lookup"><span data-stu-id="7539a-136">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="7539a-137">ügyfél-bérlő-azonosító</span><span class="sxs-lookup"><span data-stu-id="7539a-137">customer-tenant-id</span></span> | <span data-ttu-id="7539a-138">GUID</span><span class="sxs-lookup"><span data-stu-id="7539a-138">GUID</span></span> | <span data-ttu-id="7539a-139">Igen</span><span class="sxs-lookup"><span data-stu-id="7539a-139">Yes</span></span> | <span data-ttu-id="7539a-140">Az érték egy GUID formátumú **CustomerTenantId,** amely lehetővé teszi az ügyfél bérlőazonosítójának megadását.</span><span class="sxs-lookup"><span data-stu-id="7539a-140">The value is a GUID-formatted **CustomerTenantId** that allows you to specify the tenant ID of a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7539a-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="7539a-141">Request headers</span></span>

<span data-ttu-id="7539a-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7539a-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7539a-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="7539a-143">Request body</span></span>

<span data-ttu-id="7539a-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="7539a-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7539a-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="7539a-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="7539a-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="7539a-146">REST response</span></span>

<span data-ttu-id="7539a-147">Ha sikeres, ez a metódus egy [ **DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) erőforrást ad vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="7539a-147">If successful, this method returns a [**DirectSignedCustomerAgreementStatus** resource](./customer-agreement-direct-sign-status-resource.md) in the response body.</span></span>

<span data-ttu-id="7539a-148">Az erőforrás rendelkezik **egy isSigned tulajdonságtal,** amely az ügyfél közvetlen aláírási (közvetlen elfogadási) állapotát jelzi.</span><span class="sxs-lookup"><span data-stu-id="7539a-148">The resource has an **isSigned** property that indicates the customer's direct signing (direct acceptance) status.</span></span>

- <span data-ttu-id="7539a-149">A true **(igaz) érték** azt jelzi, hogy a szerződést közvetlenül az ügyfél írta alá (fogadta el).</span><span class="sxs-lookup"><span data-stu-id="7539a-149">A value of **true** indicates that the agreement has been signed (accepted) directly by the customer.</span></span>

- <span data-ttu-id="7539a-150">A false **(hamis)** érték  azt jelzi, hogy a szerződést nem közvetlenül az ügyfél írta alá (fogadta el).</span><span class="sxs-lookup"><span data-stu-id="7539a-150">A value of **false** indicates that the agreement has *not* been signed (accepted) directly by the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7539a-151">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="7539a-151">Response success and error codes</span></span>

<span data-ttu-id="7539a-152">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="7539a-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span>

<span data-ttu-id="7539a-153">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="7539a-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7539a-154">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7539a-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7539a-155">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="7539a-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
