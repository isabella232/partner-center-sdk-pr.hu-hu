---
title: Közvetett viszonteladó aláírási állapotának Microsoft Partnerszerződés ellenőrzése
description: Az AgreementStatus API használatával ellenőrizheti, hogy egy közvetett viszonteladó írta-e alá a Microsoft Partnerszerződés.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f83acc61624a72354c390905b1250bc021dd39aa
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529834"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a><span data-ttu-id="3ee41-103">Közvetett viszonteladó aláírási állapotának Microsoft Partnerszerződés ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="3ee41-103">Verify an indirect reseller's Microsoft Partner Agreement signing status</span></span>

<span data-ttu-id="3ee41-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3ee41-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3ee41-105">Ellenőrizheti, hogy egy közvetett viszonteladó írta-e alá a Microsoft Partnerszerződés-t az Microsoft Partner Network(MPN) azonosítójával (PGA/PLA) vagy Felhőszolgáltató (CSP) bérlőazonosítójával (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="3ee41-105">You can verify whether an indirect reseller has signed the Microsoft Partner Agreement using their Microsoft Partner Network (MPN) ID (PGA/PLA) or Cloud Solution Provider (CSP) tenant ID (Microsoft ID).</span></span> <span data-ttu-id="3ee41-106">Ezen azonosítók egyikének használatával ellenőrizheti a Microsoft Partnerszerződés állapotát az **AgreementStatus** API-val.</span><span class="sxs-lookup"><span data-stu-id="3ee41-106">You can use one of these identifiers to check the Microsoft Partner Agreement signing status using the **AgreementStatus** API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ee41-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3ee41-107">Prerequisites</span></span>

- <span data-ttu-id="3ee41-108">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3ee41-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3ee41-109">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="3ee41-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3ee41-110">A közvetett viszonteladó MPN-azonosítója (PGA/PLA) vagy CSP-bérlőazonosítója (Microsoft ID).</span><span class="sxs-lookup"><span data-stu-id="3ee41-110">The MPN ID (PGA/PLA) or the CSP tenant ID (Microsoft ID) of the indirect reseller.</span></span> <span data-ttu-id="3ee41-111">*A két azonosító egyikét kell használnia.*</span><span class="sxs-lookup"><span data-stu-id="3ee41-111">*You must use one of these two identifiers.*</span></span>

## <a name="c"></a><span data-ttu-id="3ee41-112">C\#</span><span class="sxs-lookup"><span data-stu-id="3ee41-112">C\#</span></span>

<span data-ttu-id="3ee41-113">Közvetett viszonteladó Microsoft Partnerszerződés aláírási állapotának legyűjtése:</span><span class="sxs-lookup"><span data-stu-id="3ee41-113">To get the Microsoft Partner Agreement signature status of an indirect reseller:</span></span>

1. <span data-ttu-id="3ee41-114">Az **AgreementSignatureStatus** tulajdonságot az **IAggregatePartner.Compliance** gyűjtemény használatával hívható meg.</span><span class="sxs-lookup"><span data-stu-id="3ee41-114">Use your **IAggregatePartner.Compliance** collection to call the **AgreementSignatureStatus** property.</span></span>

2. <span data-ttu-id="3ee41-115">Hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)</span><span class="sxs-lookup"><span data-stu-id="3ee41-115">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- <span data-ttu-id="3ee41-116">Minta: **[Konzoltesztalkalmazás](console-test-app.md)**</span><span class="sxs-lookup"><span data-stu-id="3ee41-116">Sample: **[Console test app](console-test-app.md)**</span></span>
- <span data-ttu-id="3ee41-117">Project: **PartnerCenterSDK.FeaturesSamples**</span><span class="sxs-lookup"><span data-stu-id="3ee41-117">Project: **PartnerCenterSDK.FeaturesSamples**</span></span>
- <span data-ttu-id="3ee41-118">Osztály: **GetAgreementSignatureStatus.cs**</span><span class="sxs-lookup"><span data-stu-id="3ee41-118">Class: **GetAgreementSignatureStatus.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3ee41-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="3ee41-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3ee41-120">Kérésszintaxis</span><span class="sxs-lookup"><span data-stu-id="3ee41-120">Request syntax</span></span>

| <span data-ttu-id="3ee41-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="3ee41-121">Method</span></span> | <span data-ttu-id="3ee41-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="3ee41-122">Request URI</span></span> |
| ------ | ----------- |
| <span data-ttu-id="3ee41-123">**Kap**</span><span class="sxs-lookup"><span data-stu-id="3ee41-123">**GET**</span></span> | <span data-ttu-id="3ee41-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span><span class="sxs-lookup"><span data-stu-id="3ee41-124">*[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId}</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3ee41-125">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="3ee41-125">URI parameters</span></span>

<span data-ttu-id="3ee41-126">A partner azonosításához meg kell adnia az alábbi két lekérdezési paraméter egyikét.</span><span class="sxs-lookup"><span data-stu-id="3ee41-126">You must provide one of the following two query parameters to identify the partner.</span></span> <span data-ttu-id="3ee41-127">Ha nem adja meg a két lekérdezési paraméter valamelyikét, **400-as (Hibás kérés) hibaüzenetet kap.**</span><span class="sxs-lookup"><span data-stu-id="3ee41-127">If you don't provide one of these two query parameters, you will receive a **400 (Bad request)** error.</span></span>

| <span data-ttu-id="3ee41-128">Név</span><span class="sxs-lookup"><span data-stu-id="3ee41-128">Name</span></span> | <span data-ttu-id="3ee41-129">Típus</span><span class="sxs-lookup"><span data-stu-id="3ee41-129">Type</span></span> | <span data-ttu-id="3ee41-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="3ee41-130">Required</span></span> | <span data-ttu-id="3ee41-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="3ee41-131">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="3ee41-132">**MpnId**</span><span class="sxs-lookup"><span data-stu-id="3ee41-132">**MpnId**</span></span> | <span data-ttu-id="3ee41-133">int</span><span class="sxs-lookup"><span data-stu-id="3ee41-133">int</span></span> | <span data-ttu-id="3ee41-134">Nem</span><span class="sxs-lookup"><span data-stu-id="3ee41-134">No</span></span> | <span data-ttu-id="3ee41-135">Egy Microsoft Partner Network (PGA/PLA) azonosító, amely azonosítja a közvetett viszonteladót.</span><span class="sxs-lookup"><span data-stu-id="3ee41-135">A Microsoft Partner Network ID (PGA/PLA) that identifies the indirect reseller.</span></span> |
| <span data-ttu-id="3ee41-136">**TenantId (Bérlőazonosító)**</span><span class="sxs-lookup"><span data-stu-id="3ee41-136">**TenantId**</span></span> | <span data-ttu-id="3ee41-137">GUID</span><span class="sxs-lookup"><span data-stu-id="3ee41-137">GUID</span></span> | <span data-ttu-id="3ee41-138">Nem</span><span class="sxs-lookup"><span data-stu-id="3ee41-138">No</span></span> | <span data-ttu-id="3ee41-139">A közvetett viszonteladó CSP-fiókját azonosító Microsoft-azonosító.</span><span class="sxs-lookup"><span data-stu-id="3ee41-139">A Microsoft ID that identifies the CSP account of the indirect reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3ee41-140">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="3ee41-140">Request headers</span></span>

<span data-ttu-id="3ee41-141">További információ: REST [Partnerközpont.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3ee41-141">For more information, see [Partner Center REST](headers.md).</span></span>

### <a name="request-examples"></a><span data-ttu-id="3ee41-142">Példák kérésre</span><span class="sxs-lookup"><span data-stu-id="3ee41-142">Request examples</span></span>

#### <a name="request-using-mpn-id-pgapla"></a><span data-ttu-id="3ee41-143">Kérés MPN-azonosítóval (PGA/PLA)</span><span class="sxs-lookup"><span data-stu-id="3ee41-143">Request using MPN ID (PGA/PLA)</span></span>

<span data-ttu-id="3ee41-144">A következő példakérés a közvetett viszonteladó aláírási állapotát Microsoft Partnerszerződés le a közvetett viszonteladó Microsoft Partner Network azonosítójával.</span><span class="sxs-lookup"><span data-stu-id="3ee41-144">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's Microsoft Partner Network ID.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a><span data-ttu-id="3ee41-145">Kérelem CSP-bérlőazonosító használatával</span><span class="sxs-lookup"><span data-stu-id="3ee41-145">Request using CSP tenant ID</span></span>

<span data-ttu-id="3ee41-146">A következő példakérés lekérése a közvetett viszonteladó Microsoft Partnerszerződés aláírási állapotát a közvetett viszonteladó CSP-bérlőazonosítójának (Microsoft ID) használatával.</span><span class="sxs-lookup"><span data-stu-id="3ee41-146">The following example request gets the indirect reseller's Microsoft Partner Agreement signing status using the indirect reseller's CSP tenant ID (Microsoft ID).</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3ee41-147">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="3ee41-147">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3ee41-148">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="3ee41-148">Response success and error codes</span></span>

<span data-ttu-id="3ee41-149">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="3ee41-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3ee41-150">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="3ee41-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3ee41-151">A teljes listát lásd: Partnerközpont [REST-hiba.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3ee41-151">For the full list, see [Partner Center REST error](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="3ee41-152">Válasz példa (sikeres)</span><span class="sxs-lookup"><span data-stu-id="3ee41-152">Response example (success)</span></span>

<span data-ttu-id="3ee41-153">Az alábbi példaválasz sikeresen visszaadja, hogy a közvetett viszonteladó írta-e alá a Microsoft Partnerszerződés.</span><span class="sxs-lookup"><span data-stu-id="3ee41-153">The following example response successfully returns whether the indirect reseller has signed the Microsoft Partner Agreement.</span></span>

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

### <a name="response-examples-failure"></a><span data-ttu-id="3ee41-154">Példák válaszra (hiba)</span><span class="sxs-lookup"><span data-stu-id="3ee41-154">Response examples (failure)</span></span>

<span data-ttu-id="3ee41-155">Előfordulhat, hogy az alábbi példákhoz hasonló válaszokat kap, ha a közvetett viszonteladói regisztráció aláírási állapota Microsoft Partnerszerződés nem lehet visszaadni.</span><span class="sxs-lookup"><span data-stu-id="3ee41-155">You may receive responses similar to the following examples when the signing status of the indirect reseller's Microsoft Partner Agreement can't be returned.</span></span>

#### <a name="non-guid-formatted-csp-tenant-id"></a><span data-ttu-id="3ee41-156">Nem GUID formátumú CSP-bérlőazonosító</span><span class="sxs-lookup"><span data-stu-id="3ee41-156">Non-GUID formatted CSP tenant ID</span></span>

<span data-ttu-id="3ee41-157">A következő példaválasz akkor lesz visszaadva, ha az API-nak átadott CSP-bérlőazonosító nem GUID.</span><span class="sxs-lookup"><span data-stu-id="3ee41-157">The following example response is returned when the CSP tenant ID that you passed to the API isn't a GUID.</span></span>

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

#### <a name="non-numeric-mpn-id"></a><span data-ttu-id="3ee41-158">Nem numerikus MPN-azonosító</span><span class="sxs-lookup"><span data-stu-id="3ee41-158">Non-numeric MPN ID</span></span>

<span data-ttu-id="3ee41-159">Az alábbi példaválasz akkor lesz visszaadva, ha az API-nak átadott MPN-azonosító (PGA/PLA) nem numerikus.</span><span class="sxs-lookup"><span data-stu-id="3ee41-159">The following example response is returned when the MPN ID (PGA/PLA) that you passed to the API is non-numeric.</span></span>

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a><span data-ttu-id="3ee41-160">Nincs MPN-azonosító vagy CSP-bérlőazonosító</span><span class="sxs-lookup"><span data-stu-id="3ee41-160">No MPN ID or CSP tenant ID</span></span>

<span data-ttu-id="3ee41-161">A következő példaválasz akkor lesz visszaadva, ha nem adott át MPN-azonosítót (PGA/PLA) vagy CSP-bérlőazonosítót az API-nak.</span><span class="sxs-lookup"><span data-stu-id="3ee41-161">The following example response is returned when you haven't passed an MPN ID (PGA/PLA) or CSP tenant ID to the API.</span></span> <span data-ttu-id="3ee41-162">A két azonosítótípus valamelyikét át kell adni az API-nak.</span><span class="sxs-lookup"><span data-stu-id="3ee41-162">You must pass one of the two ID types to the API.</span></span>

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a><span data-ttu-id="3ee41-163">Az MPN-azonosító és a CSP-bérlőazonosító is átadott</span><span class="sxs-lookup"><span data-stu-id="3ee41-163">Both MPN ID and CSP tenant ID passed</span></span>

<span data-ttu-id="3ee41-164">Az alábbi példaválasz akkor lesz visszaadva, ha az MPN-azonosítót (PGA/PLA) és a CSP-bérlőazonosítót is átadhatja az API-nak.</span><span class="sxs-lookup"><span data-stu-id="3ee41-164">The following example response is returned when you pass both the MPN ID (PGA/PLA) and CSP tenant ID to the API.</span></span> <span data-ttu-id="3ee41-165">A két *azonosítótípus közül* csak egyet kell átadnia az API-nak.</span><span class="sxs-lookup"><span data-stu-id="3ee41-165">You must pass *only one* of the two identifier types to the API.</span></span>

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a><span data-ttu-id="3ee41-166">CSP Indirect Reseller MPN-azonosító (PGA/PLA) érvénytelen, vagy nem migrálható Partner Membership Center-ről Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="3ee41-166">CSP Indirect Reseller MPN ID (PGA/PLA) is either invalid or not migrated from Partner Membership Center to Partner Center</span></span>

<span data-ttu-id="3ee41-167">A következő példaválasz akkor ad vissza, ha a közvetett viszonteladó MPN-azonosítója (PGA/PLA) érvénytelen, vagy nem migrálva lett Partner Membership Center-ről Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="3ee41-167">The following example response is returned when Indirect reseller MPN ID (PGA/PLA) passed is either invalid or it is not migrated from Partner Membership Center to Partner Center.</span></span> [<span data-ttu-id="3ee41-168">További információ</span><span class="sxs-lookup"><span data-stu-id="3ee41-168">Learn More</span></span>](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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
        "https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a><span data-ttu-id="3ee41-169">CSP Indirect Provider régió és CSP Indirect Reseller régió nem egyezik</span><span class="sxs-lookup"><span data-stu-id="3ee41-169">CSP Indirect Provider region and CSP Indirect Reseller region does not match</span></span>

<span data-ttu-id="3ee41-170">Az alábbi példaválasz akkor lesz visszaadva, ha a közvetett viszonteladó MPN-azonosítója (PGA/PLA) régiója nem egyezik meg a közvetett szolgáltató régiójával.</span><span class="sxs-lookup"><span data-stu-id="3ee41-170">The following example response is returned when region of Indirect reseller MPN ID (PGA/PLA) doesn't match with region of the Indirect Provider.</span></span> <span data-ttu-id="3ee41-171">[További információ a](/partner-center/mpa-indirect-provider-faq) CSP-régiókról.</span><span class="sxs-lookup"><span data-stu-id="3ee41-171">[Learn more](/partner-center/mpa-indirect-provider-faq) about CSP Regions.</span></span>

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
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a><span data-ttu-id="3ee41-172">CSP Indirect Reseller fiók létezik a Partnerközpont de még nem írta alá az MPA-t</span><span class="sxs-lookup"><span data-stu-id="3ee41-172">CSP Indirect Reseller account exists in Partner Center but hasn't signed the MPA</span></span>

<span data-ttu-id="3ee41-173">Az alábbi példaválasz akkor lesz visszaadva, CSP Indirect Reseller a Partnerközpont nem írta alá az MPA-t.</span><span class="sxs-lookup"><span data-stu-id="3ee41-173">The following example response is returned when CSP Indirect Reseller account in Partner Center hasn't signed the MPA.</span></span> [<span data-ttu-id="3ee41-174">További információ</span><span class="sxs-lookup"><span data-stu-id="3ee41-174">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a><span data-ttu-id="3ee41-175">Nincs CSP Indirect Reseller fiók társítva az adott MPN-azonosítóval</span><span class="sxs-lookup"><span data-stu-id="3ee41-175">No CSP Indirect Reseller account is associated with the given MPN ID</span></span>

<span data-ttu-id="3ee41-176">A következő példaválaszt a rendszer akkor ad vissza, Partnerközpont a rendszer felismeri a kérésben átadott MPN-azonosítót (PGA/PLA), de az adott MPN-azonosítóhoz (PGA/PLA) nincs CSP-regisztráció társítva.</span><span class="sxs-lookup"><span data-stu-id="3ee41-176">The following example response is returned when Partner Center can recognize the MPN ID (PGA/PLA) passed in the request but there is no CSP enrollment associated to the given MPN ID (PGA/PLA).</span></span> [<span data-ttu-id="3ee41-177">További információ</span><span class="sxs-lookup"><span data-stu-id="3ee41-177">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a><span data-ttu-id="3ee41-178">Érvénytelen bérlőazonosító</span><span class="sxs-lookup"><span data-stu-id="3ee41-178">Invalid Tenant ID</span></span>

<span data-ttu-id="3ee41-179">A következő példaválasz akkor lesz visszaadva Partnerközpont nem található a kérésben átadott bérlőazonosítóhoz társított fiók.</span><span class="sxs-lookup"><span data-stu-id="3ee41-179">The following example response is returned when Partner Center doesn't find any account associated to the Tenant ID passed in the request.</span></span>

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a><span data-ttu-id="3ee41-180">Nem található MPA a megadott bérlőazonosítóval</span><span class="sxs-lookup"><span data-stu-id="3ee41-180">No MPA found with the given Tenant ID</span></span>

<span data-ttu-id="3ee41-181">Az alábbi példaválasz akkor lesz visszaadva, Partnerközpont nem található MPA-aláírás a megadott bérlőazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="3ee41-181">The following example response is returned when Partner Center can't find any MPA signature with the given Tenant ID.</span></span> [<span data-ttu-id="3ee41-182">További információ</span><span class="sxs-lookup"><span data-stu-id="3ee41-182">Learn More</span></span>](/partner-center/mpa-indirect-provider-faq)

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
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```