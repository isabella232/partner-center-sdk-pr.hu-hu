---
title: Tartomány rendelkezésre állásának ellenőrzése
description: Hogyan állapítható meg, hogy a tartomány használható-e.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 84edb5b7510642ec44dad3d4f92349e40eb10b24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768279"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="cfbac-103">Tartomány rendelkezésre állásának ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="cfbac-103">Verify domain availability</span></span>

<span data-ttu-id="cfbac-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="cfbac-104">**Applies To**</span></span>

- <span data-ttu-id="cfbac-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="cfbac-105">Partner Center</span></span>
- <span data-ttu-id="cfbac-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="cfbac-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cfbac-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="cfbac-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cfbac-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="cfbac-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cfbac-109">Hogyan állapítható meg, hogy a tartomány használható-e.</span><span class="sxs-lookup"><span data-stu-id="cfbac-109">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfbac-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="cfbac-110">Prerequisites</span></span>

- <span data-ttu-id="cfbac-111">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="cfbac-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cfbac-112">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="cfbac-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cfbac-113">Egy tartomány (például `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="cfbac-113">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="cfbac-114">C\#</span><span class="sxs-lookup"><span data-stu-id="cfbac-114">C\#</span></span>

<span data-ttu-id="cfbac-115">Annak ellenőrzéséhez, hogy a tartomány elérhető-e, először hívja meg a [**IAggregatePartner. Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) -t, és szerezzen be egy felületet a tartományi műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="cfbac-115">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="cfbac-116">Ezután hívja meg a [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) metódust a tartománnyal.</span><span class="sxs-lookup"><span data-stu-id="cfbac-116">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="cfbac-117">Ez a módszer egy adott tartományhoz elérhető műveletekhez tartozó felületet kérdez le.</span><span class="sxs-lookup"><span data-stu-id="cfbac-117">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="cfbac-118">Végül hívja meg a [**létező**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) metódust, és ellenőrizze, hogy már létezik-e a tartomány.</span><span class="sxs-lookup"><span data-stu-id="cfbac-118">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="cfbac-119">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cfbac-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cfbac-120">**Projekt**: partner Center SDK Samples **osztály**: CheckDomainAvailability.cs</span><span class="sxs-lookup"><span data-stu-id="cfbac-120">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cfbac-121">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="cfbac-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cfbac-122">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="cfbac-122">Request syntax</span></span>

| <span data-ttu-id="cfbac-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="cfbac-123">Method</span></span>   | <span data-ttu-id="cfbac-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="cfbac-124">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="cfbac-125">**FEJ**</span><span class="sxs-lookup"><span data-stu-id="cfbac-125">**HEAD**</span></span> | <span data-ttu-id="cfbac-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/Domains/{domain} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cfbac-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cfbac-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="cfbac-127">URI parameter</span></span>

<span data-ttu-id="cfbac-128">A tartomány rendelkezésre állásának ellenőrzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="cfbac-128">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="cfbac-129">Név</span><span class="sxs-lookup"><span data-stu-id="cfbac-129">Name</span></span>       | <span data-ttu-id="cfbac-130">Típus</span><span class="sxs-lookup"><span data-stu-id="cfbac-130">Type</span></span>       | <span data-ttu-id="cfbac-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="cfbac-131">Required</span></span> | <span data-ttu-id="cfbac-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="cfbac-132">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="cfbac-133">**tartományi**</span><span class="sxs-lookup"><span data-stu-id="cfbac-133">**domain**</span></span> | <span data-ttu-id="cfbac-134">**karakterlánc**</span><span class="sxs-lookup"><span data-stu-id="cfbac-134">**string**</span></span> | <span data-ttu-id="cfbac-135">Y</span><span class="sxs-lookup"><span data-stu-id="cfbac-135">Y</span></span>        | <span data-ttu-id="cfbac-136">Egy karakterlánc, amely az ellenőrzési tartományt azonosítja.</span><span class="sxs-lookup"><span data-stu-id="cfbac-136">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cfbac-137">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="cfbac-137">Request headers</span></span>

<span data-ttu-id="cfbac-138">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cfbac-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cfbac-139">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="cfbac-139">Request body</span></span>

<span data-ttu-id="cfbac-140">Nincs</span><span class="sxs-lookup"><span data-stu-id="cfbac-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="cfbac-141">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="cfbac-141">Request example</span></span>

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="cfbac-142">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="cfbac-142">REST response</span></span>

<span data-ttu-id="cfbac-143">Ha a tartomány létezik, az nem érhető el, és az 200-es válasz-állapotkód vissza lesz állítva.</span><span class="sxs-lookup"><span data-stu-id="cfbac-143">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="cfbac-144">Ha a tartomány nem található, használható, és a 404-es válasz-állapotkód nem található.</span><span class="sxs-lookup"><span data-stu-id="cfbac-144">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cfbac-145">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="cfbac-145">Response success and error codes</span></span>

<span data-ttu-id="cfbac-146">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="cfbac-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cfbac-147">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="cfbac-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cfbac-148">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="cfbac-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="cfbac-149">Válasz példa arra, ha a tartomány már használatban van</span><span class="sxs-lookup"><span data-stu-id="cfbac-149">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="cfbac-150">Válasz példa arra, ha a tartomány elérhető</span><span class="sxs-lookup"><span data-stu-id="cfbac-150">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
