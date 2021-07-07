---
title: Tartomány rendelkezésre állásának ellenőrzése
description: Annak meghatározása, hogy egy tartomány használható-e.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530276"
---
# <a name="verify-domain-availability"></a><span data-ttu-id="f7363-103">Tartomány rendelkezésre állásának ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="f7363-103">Verify domain availability</span></span>

<span data-ttu-id="f7363-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f7363-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f7363-105">Annak meghatározása, hogy egy tartomány használható-e.</span><span class="sxs-lookup"><span data-stu-id="f7363-105">How to determine if a domain is available for use.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7363-106">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="f7363-106">Prerequisites</span></span>

- <span data-ttu-id="f7363-107">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f7363-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f7363-108">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="f7363-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f7363-109">Egy tartomány (például `contoso.onmicrosoft.com` ).</span><span class="sxs-lookup"><span data-stu-id="f7363-109">A domain (for example `contoso.onmicrosoft.com`).</span></span>

## <a name="c"></a><span data-ttu-id="f7363-110">C\#</span><span class="sxs-lookup"><span data-stu-id="f7363-110">C\#</span></span>

<span data-ttu-id="f7363-111">Annak ellenőrzéséhez, hogy egy tartomány elérhető-e, először hívja meg az [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) nevet a tartományi műveletek interfészének beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="f7363-111">To verify if a domain is available, first call [**IAggregatePartner.Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) to obtain an interface to domain operations.</span></span> <span data-ttu-id="f7363-112">Ezután hívja meg [**a ByDomain metódust**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) az ellenőrzéshez használt tartománnyal.</span><span class="sxs-lookup"><span data-stu-id="f7363-112">Then call the [**ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) method with the domain to check.</span></span> <span data-ttu-id="f7363-113">Ez a metódus lekér egy felületet az adott tartományhoz elérhető műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="f7363-113">This method retrieves an interface to the operations available for a specific domain.</span></span> <span data-ttu-id="f7363-114">Végül hívja meg az [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) metódust, hogy lássa, létezik-e már a tartomány.</span><span class="sxs-lookup"><span data-stu-id="f7363-114">Finally, call the [**Exists**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) method to see if the domain already exists.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

<span data-ttu-id="f7363-115">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f7363-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f7363-116">**Project**: Partnerközpont SDK **Osztály:** CheckDomainAvailability.cs</span><span class="sxs-lookup"><span data-stu-id="f7363-116">**Project**: Partner Center SDK Samples **Class**: CheckDomainAvailability.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f7363-117">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="f7363-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f7363-118">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="f7363-118">Request syntax</span></span>

| <span data-ttu-id="f7363-119">Metódus</span><span class="sxs-lookup"><span data-stu-id="f7363-119">Method</span></span>   | <span data-ttu-id="f7363-120">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="f7363-120">Request URI</span></span>                                                              |
|----------|--------------------------------------------------------------------------|
| <span data-ttu-id="f7363-121">**Fej**</span><span class="sxs-lookup"><span data-stu-id="f7363-121">**HEAD**</span></span> | <span data-ttu-id="f7363-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f7363-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f7363-123">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="f7363-123">URI parameter</span></span>

<span data-ttu-id="f7363-124">A tartomány rendelkezésre állásának ellenőrzéséhez használja a következő lekérdezési paramétert.</span><span class="sxs-lookup"><span data-stu-id="f7363-124">Use the following query parameter to verify domain availability.</span></span>

| <span data-ttu-id="f7363-125">Név</span><span class="sxs-lookup"><span data-stu-id="f7363-125">Name</span></span>       | <span data-ttu-id="f7363-126">Típus</span><span class="sxs-lookup"><span data-stu-id="f7363-126">Type</span></span>       | <span data-ttu-id="f7363-127">Kötelező</span><span class="sxs-lookup"><span data-stu-id="f7363-127">Required</span></span> | <span data-ttu-id="f7363-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="f7363-128">Description</span></span>                                   |
|------------|------------|----------|-----------------------------------------------|
| <span data-ttu-id="f7363-129">**Tartomány**</span><span class="sxs-lookup"><span data-stu-id="f7363-129">**domain**</span></span> | <span data-ttu-id="f7363-130">**sztring**</span><span class="sxs-lookup"><span data-stu-id="f7363-130">**string**</span></span> | <span data-ttu-id="f7363-131">Y</span><span class="sxs-lookup"><span data-stu-id="f7363-131">Y</span></span>        | <span data-ttu-id="f7363-132">Egy sztring, amely azonosítja az ellenőriznie kell a tartományt.</span><span class="sxs-lookup"><span data-stu-id="f7363-132">A string that identifies the domain to check.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f7363-133">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="f7363-133">Request headers</span></span>

<span data-ttu-id="f7363-134">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f7363-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f7363-135">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="f7363-135">Request body</span></span>

<span data-ttu-id="f7363-136">None</span><span class="sxs-lookup"><span data-stu-id="f7363-136">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f7363-137">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="f7363-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f7363-138">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="f7363-138">REST response</span></span>

<span data-ttu-id="f7363-139">Ha a tartomány létezik, nem használható, és a 200 OK válaszállapotkódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="f7363-139">If the domain exists, it isn't available for use and a response status code 200 OK is returned.</span></span> <span data-ttu-id="f7363-140">Ha a tartomány nem található, használható, és a 404 Not Found válaszállapotkódot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="f7363-140">If the domain isn't found, it's available for use and a response status code 404 Not Found is returned.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f7363-141">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="f7363-141">Response success and error codes</span></span>

<span data-ttu-id="f7363-142">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="f7363-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f7363-143">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="f7363-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f7363-144">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f7363-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-for-when-the-domain-is-already-in-use"></a><span data-ttu-id="f7363-145">Példa válaszra, ha a tartomány már használatban van</span><span class="sxs-lookup"><span data-stu-id="f7363-145">Response example for when the domain is already in use</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a><span data-ttu-id="f7363-146">Példa a tartomány rendelkezésre áll-e válaszra</span><span class="sxs-lookup"><span data-stu-id="f7363-146">Response example for when the domain is available</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
