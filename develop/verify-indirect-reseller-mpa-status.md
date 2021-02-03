---
title: Közvetett viszonteladó Microsoft partneri szerződésének aláírása állapotának ellenőrzése
description: A AgreementStatus API segítségével ellenőrizheti, hogy a közvetett viszonteladó aláírta-e a Microsoft partneri szerződést.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 436f690991a2920465a5a13c73eb4c194956ae94
ms.sourcegitcommit: ca932ba511bf7464a634195d71891f989036ab74
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/29/2020
ms.locfileid: "97768496"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="e5e1b-103">Közvetett viszonteladó Microsoft partneri szerződésének aláírása állapotának ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="e5e1b-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="e5e1b-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="e5e1b-104">**Applies to:**</span></span>

- <span data-ttu-id="e5e1b-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="e5e1b-105">Partner Center</span></span>
- <span data-ttu-id="e5e1b-106">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="e5e1b-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e5e1b-107">Ellenőrizheti, hogy a közvetett viszonteladó aláírta-e a Microsoft partneri szerződést a Microsoft Partner Network (MPN) azonosító (PGA/PLA) vagy a Cloud Solution Provider (CSP) bérlői azonosító (Microsoft ID) használatával.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-107">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="e5e1b-108">Ezen azonosítók egyikével ellenőrizhető a Microsoft partneri szerződés aláírása állapota a **AgreementStatus** API használatával.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-108">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5e1b-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="e5e1b-109">Prerequisites</span></span>

- <span data-ttu-id="e5e1b-110">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e5e1b-111">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e5e1b-112">Az MPN-azonosító (PGA/PLA) vagy a közvetett viszonteladóhoz tartozó CSP-bérlő azonosítója (Microsoft-azonosító).</span><span class="sxs-lookup"><span data-stu-id="e5e1b-112">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="e5e1b-113">*A két azonosító közül egyet kell használnia.*</span><span class="sxs-lookup"><span data-stu-id="e5e1b-113">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="e5e1b-114">C\#</span><span class="sxs-lookup"><span data-stu-id="e5e1b-114">C\#</span></span>

<span data-ttu-id="e5e1b-115">Közvetett viszonteladói Microsoft partneri szerződés aláírási állapotának beszerzése:</span><span class="sxs-lookup"><span data-stu-id="e5e1b-115">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="e5e1b-116">A **IAggregatePartner. Compliance** gyűjtemény használatával hívja meg a **AgreementSignatureStatus** tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-116">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="e5e1b-117">Hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) metódust.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-117">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="e5e1b-118">Minta: **[konzol tesztelési alkalmazás](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="e5e1b-118">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="e5e1b-119">Projekt: **PartnerCenterSDK. FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="e5e1b-119">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="e5e1b-120">Osztály: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="e5e1b-120">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="e5e1b-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="e5e1b-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e5e1b-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="e5e1b-122">Request syntax</span></span>

| <span data-ttu-id="e5e1b-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="e5e1b-123">Method</span></span> | <span data-ttu-id="e5e1b-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="e5e1b-124">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="e5e1b-125">**GET**</span><span class="sxs-lookup"><span data-stu-id="e5e1b-125">**GET**</span></span> | <span data-ttu-id="e5e1b-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/Compliance/{ProgramName}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId}</span><span class="sxs-lookup"><span data-stu-id="e5e1b-126">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="e5e1b-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="e5e1b-127">URI parameters</span></span>

<span data-ttu-id="e5e1b-128">A partner azonosításához a következő két lekérdezési paraméter egyikét kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-128">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="e5e1b-129">Ha nem adja meg a két lekérdezési paraméter egyikét sem, a rendszer **400 (hibás kérés)** hibaüzenetet kap.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-129">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="e5e1b-130">Név</span><span class="sxs-lookup"><span data-stu-id="e5e1b-130">Name</span></span> | <span data-ttu-id="e5e1b-131">Típus</span><span class="sxs-lookup"><span data-stu-id="e5e1b-131">Type</span></span> | <span data-ttu-id="e5e1b-132">Kötelező</span><span class="sxs-lookup"><span data-stu-id="e5e1b-132">Required</span></span> | <span data-ttu-id="e5e1b-133">Leírás</span><span class="sxs-lookup"><span data-stu-id="e5e1b-133">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="e5e1b-134">**MpnId**</span><span class="sxs-lookup"><span data-stu-id="e5e1b-134">**MpnId**</span></span> | <span data-ttu-id="e5e1b-135">int</span><span class="sxs-lookup"><span data-stu-id="e5e1b-135">int</span></span> | <span data-ttu-id="e5e1b-136">Nem</span><span class="sxs-lookup"><span data-stu-id="e5e1b-136">No</span></span> | <span data-ttu-id="e5e1b-137">A közvetett viszonteladót azonosító Microsoft Partner Network azonosító (PGA/PLA).</span><span class="sxs-lookup"><span data-stu-id="e5e1b-137">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="e5e1b-138">**TenantId**</span><span class="sxs-lookup"><span data-stu-id="e5e1b-138">**TenantId**</span></span> | <span data-ttu-id="e5e1b-139">GUID</span><span class="sxs-lookup"><span data-stu-id="e5e1b-139">GUID</span></span> | <span data-ttu-id="e5e1b-140">Nem</span><span class="sxs-lookup"><span data-stu-id="e5e1b-140">No</span></span> | <span data-ttu-id="e5e1b-141">Egy Microsoft-azonosító, amely azonosítja a közvetett viszonteladó CSP-fiókját.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-141">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e5e1b-142">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="e5e1b-142">Request headers</span></span>

<span data-ttu-id="e5e1b-143">További információ: a [partner Center Rest](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e5e1b-143">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="e5e1b-144">Példák kérése</span><span class="sxs-lookup"><span data-stu-id="e5e1b-144">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="e5e1b-145">Kérelem az MPN-AZONOSÍTÓval (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="e5e1b-145">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="e5e1b-146">A következő példa a közvetett viszonteladói Microsoft partneri szerződés aláírási állapotát a közvetett viszonteladó Microsoft Partner Network AZONOSÍTÓjának használatával kéri le.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="e5e1b-147">A CSP-bérlő AZONOSÍTÓját használó kérelem</span><span class="sxs-lookup"><span data-stu-id="e5e1b-147">Request using CSP tenant ID</span></span>

<span data-ttu-id="e5e1b-148">A következő példa lekéri a közvetett viszonteladó Microsoft partneri szerződésének aláírása állapotát a közvetett viszonteladó CSP-bérlői AZONOSÍTÓjának (Microsoft ID) használatával.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-148">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e5e1b-149">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="e5e1b-149">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e5e1b-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="e5e1b-150">Response success and error codes</span></span>

<span data-ttu-id="e5e1b-151">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e5e1b-152">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e5e1b-153">A teljes listát lásd: a [partneri központ Rest-hibája](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e5e1b-153">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="e5e1b-154">Válasz példa (sikeres)</span><span class="sxs-lookup"><span data-stu-id="e5e1b-154">Response example (success)</span></span>

<span data-ttu-id="e5e1b-155">A következő példában szereplő válasz sikeresen visszaadja, hogy a közvetett viszonteladó aláírta-e a Microsoft partneri szerződést.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-155">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a><span data-ttu-id="e5e1b-156">Válasz példák (hiba)</span><span class="sxs-lookup"><span data-stu-id="e5e1b-156">Response examples (failure)</span></span>

<span data-ttu-id="e5e1b-157">Az alábbi példákhoz hasonló válaszokat kaphat, ha nem lehet visszaadni a közvetett viszonteladó Microsoft partneri szerződésének aláírási állapotát.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-157">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="e5e1b-158">Nem GUID formátumú CSP-bérlő azonosítója</span><span class="sxs-lookup"><span data-stu-id="e5e1b-158">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="e5e1b-159">Az alábbi példában szereplő válasz akkor ad vissza, ha az API-nak átadott CSP-bérlő azonosítója nem GUID.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-159">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="e5e1b-160">Nem numerikus MPN-azonosító</span><span class="sxs-lookup"><span data-stu-id="e5e1b-160">Non-numeric MPN ID</span></span>

<span data-ttu-id="e5e1b-161">Az alábbi példában szereplő válasz akkor ad vissza, ha az API-nak átadott MPN-azonosító (PGA/PLA) nem numerikus.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-161">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="e5e1b-162">Nincs MPN-azonosító vagy CSP-bérlő azonosítója</span><span class="sxs-lookup"><span data-stu-id="e5e1b-162">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="e5e1b-163">Ha nem adott meg MPN-azonosítót (PGA/PLA) vagy CSP-bérlői azonosítót az API-nak, akkor a következő példa válaszát adja vissza.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-163">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="e5e1b-164">A két azonosító típus egyikét át kell adnia az API-nak.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-164">You must pass one of the two ID types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="e5e1b-165">Az MPN-azonosító és a CSP-bérlő azonosítója is át lett adva</span><span class="sxs-lookup"><span data-stu-id="e5e1b-165">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="e5e1b-166">Ha az MPN-azonosítót (PGA/PLA) és a CSP-bérlői azonosítót is átadja az API-nak, a következő példa érkezik.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-166">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="e5e1b-167">A két azonosító típusnak *csak az egyikét* kell átadnia az API-nak.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-167">You must pass *only one* of the two identifier types to the API.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="e5e1b-168">A CSP közvetett viszonteladói MPN-azonosítója (PGA/PLA) vagy érvénytelen, vagy nem települ át a partneri tagsági központból a partner központba</span><span class="sxs-lookup"><span data-stu-id="e5e1b-168">CSP Indirect Reseller MPN Id (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="e5e1b-169">A következő példa akkor ad vissza választ, ha az átadott közvetett viszonteladói MPN-azonosító (PGA/PLA) érvénytelen, vagy a partneri tagsági központból nem a partner központba lett áttelepítve.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-169">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="e5e1b-170">További információ</span><span class="sxs-lookup"><span data-stu-id="e5e1b-170">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="e5e1b-171">A CSP közvetett szolgáltató régiója és a CSP közvetett viszonteladói régiója nem egyezik</span><span class="sxs-lookup"><span data-stu-id="e5e1b-171">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="e5e1b-172">A következő példa akkor ad vissza választ, ha a közvetett viszonteladói MPN-azonosító (PGA/PLA) régiója nem egyezik a közvetett szolgáltató régiójával.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-172">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="e5e1b-173">[További](/partner-center/regional-authorization-overview) információ a CSP-régiókról.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-173">[Learn more](/partner-center/regional-authorization-overview) about CSP Regions.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/en-us/partner-center/regional-authorization-overview" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="e5e1b-174">A CSP közvetett viszonteladói fiókja létezik a partner Centerben, de nem írta alá az MPA-t</span><span class="sxs-lookup"><span data-stu-id="e5e1b-174">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="e5e1b-175">A következő példa válaszát adja vissza, ha a fiókpartner közvetett viszonteladói fiókja nem írta alá a MPA-t.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-175">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="e5e1b-176">További információ</span><span class="sxs-lookup"><span data-stu-id="e5e1b-176">Learn More</span></span>](https://partner.microsoft.com/resources/detail/verify-mpa-acceptance-status-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://partner.microsoft.com/en-gb/resources/detail/verify-mpa-acceptance-status-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="e5e1b-177">Nincs társítva CSP közvetett viszonteladói fiók a megadott MPN-AZONOSÍTÓhoz</span><span class="sxs-lookup"><span data-stu-id="e5e1b-177">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="e5e1b-178">A következő példa akkor ad vissza választ, ha a fiókpartner felismeri a kérelemben átadott MPN-azonosítót (PGA/PLA), de a megadott MPN-AZONOSÍTÓhoz (PGA/PLA) nincs társítva CSP-regisztráció.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-178">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="e5e1b-179">További információ</span><span class="sxs-lookup"><span data-stu-id="e5e1b-179">Learn More</span></span>](https://partner.microsoft.com/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://partner.microsoft.com/en-us/resources/detail/onboard-pc-csp-mpn-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a><span data-ttu-id="e5e1b-180">Érvénytelen a bérlő azonosítója</span><span class="sxs-lookup"><span data-stu-id="e5e1b-180">Invalid Tenant ID</span></span>

<span data-ttu-id="e5e1b-181">Ha a fiókpartner nem talál olyan fiókot, amely a kérelemben átadott bérlői AZONOSÍTÓhoz tartozik, akkor a következő példa érkezik.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-181">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="e5e1b-182">Nem található a megadott bérlői AZONOSÍTÓval rendelkező MPA</span><span class="sxs-lookup"><span data-stu-id="e5e1b-182">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="e5e1b-183">Ha a fiókpartner nem talál a megadott bérlői AZONOSÍTÓval rendelkező MPA-aláírást, akkor a következő példában szereplő válasz érkezik.</span><span class="sxs-lookup"><span data-stu-id="e5e1b-183">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span>

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [],
    "source": "PartnerFD"
}
```
