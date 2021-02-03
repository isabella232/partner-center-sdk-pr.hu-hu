---
title: Felhasználói fiókok létrehozása egy ügyfélnél
description: Hozzon létre egy új felhasználói fiókot az ügyfél számára.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9131a1c4c37d07b1994b67379ec8361fda13a371
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767747"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="b5381-103">Felhasználói fiókok létrehozása egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="b5381-103">Create user accounts for a customer</span></span>

<span data-ttu-id="b5381-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="b5381-104">**Applies to:**</span></span>

- <span data-ttu-id="b5381-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="b5381-105">Partner Center</span></span>

<span data-ttu-id="b5381-106">Hozzon létre egy új felhasználói fiókot az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="b5381-106">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5381-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="b5381-107">Prerequisites</span></span>

- <span data-ttu-id="b5381-108">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="b5381-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b5381-109">Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="b5381-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b5381-110">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5381-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b5381-111">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="b5381-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b5381-112">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="b5381-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b5381-113">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="b5381-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b5381-114">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="b5381-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b5381-115">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b5381-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="b5381-116">C\#</span><span class="sxs-lookup"><span data-stu-id="b5381-116">C\#</span></span>

<span data-ttu-id="b5381-117">Új felhasználói fiók beszerzése az ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="b5381-117">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="b5381-118">Hozzon létre egy új **CustomerUser** -objektumot a megfelelő felhasználói adatokkal.</span><span class="sxs-lookup"><span data-stu-id="b5381-118">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="b5381-119">Használja a **IAggregatePartner. Customers** gyűjteményt, és hívja meg a **ById ()** metódust.</span><span class="sxs-lookup"><span data-stu-id="b5381-119">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="b5381-120">Hívja meg a **Users (felhasználók** ) tulajdonságot, amelyet a **create** metódus követ.</span><span class="sxs-lookup"><span data-stu-id="b5381-120">Call the **Users** property, followed by the **Create** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// var SelectedCustomer;

var userToCreate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "Password!1" },
    DisplayName = "TestDisplayName",
    FirstName = "TestFirstName",
    LastName = "TestLastName",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

User createdUser = partnerOperations.Customers.ById(selectedCustomerId).Users.Create(userToCreate);
```

<span data-ttu-id="b5381-121">**Példa**: [konzol tesztelési alkalmazás](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b5381-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b5381-122">**Projekt**: PartnerSDK. FeatureSamples **osztály**: CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="b5381-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b5381-123">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="b5381-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b5381-124">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="b5381-124">Request syntax</span></span>

| <span data-ttu-id="b5381-125">Metódus</span><span class="sxs-lookup"><span data-stu-id="b5381-125">Method</span></span>   | <span data-ttu-id="b5381-126">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="b5381-126">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="b5381-127">**UTÁNI**</span><span class="sxs-lookup"><span data-stu-id="b5381-127">**POST**</span></span> | <span data-ttu-id="b5381-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="b5381-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="b5381-129">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="b5381-129">URI parameters</span></span>

<span data-ttu-id="b5381-130">A megfelelő ügyfél azonosításához használja a következő lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="b5381-130">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="b5381-131">Név</span><span class="sxs-lookup"><span data-stu-id="b5381-131">Name</span></span> | <span data-ttu-id="b5381-132">Típus</span><span class="sxs-lookup"><span data-stu-id="b5381-132">Type</span></span> | <span data-ttu-id="b5381-133">Kötelező</span><span class="sxs-lookup"><span data-stu-id="b5381-133">Required</span></span> | <span data-ttu-id="b5381-134">Leírás</span><span class="sxs-lookup"><span data-stu-id="b5381-134">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="b5381-135">**ügyfél – bérlő – azonosító**</span><span class="sxs-lookup"><span data-stu-id="b5381-135">**customer-tenant-id**</span></span> | <span data-ttu-id="b5381-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="b5381-136">**guid**</span></span> | <span data-ttu-id="b5381-137">Y</span><span class="sxs-lookup"><span data-stu-id="b5381-137">Y</span></span> | <span data-ttu-id="b5381-138">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító**. Lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti.</span><span class="sxs-lookup"><span data-stu-id="b5381-138">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="b5381-139">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="b5381-139">**user-id**</span></span> | <span data-ttu-id="b5381-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="b5381-140">**guid**</span></span> | <span data-ttu-id="b5381-141">N</span><span class="sxs-lookup"><span data-stu-id="b5381-141">N</span></span> | <span data-ttu-id="b5381-142">Az érték egy olyan GUID formátumú **felhasználói azonosító** , amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="b5381-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b5381-143">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="b5381-143">Request headers</span></span>

<span data-ttu-id="b5381-144">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b5381-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b5381-145">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="b5381-145">Request body</span></span>

<span data-ttu-id="b5381-146">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="b5381-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b5381-147">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="b5381-147">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "country/region code",
      "userPrincipalName": "userid@domain.onmicrosoft.com",
      "firstName": "First",
      "lastName": "Last",
      "displayName": "User name",
      "immutableId": "Some unique ID",
      "passwordProfile":{
                 password: "abCD123*",
                 forceChangePassword: true
      },
      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="b5381-148">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="b5381-148">REST response</span></span>

<span data-ttu-id="b5381-149">Ha ez sikeres, a metódus egy felhasználói fiókot ad vissza, beleértve a GUID azonosítót is.</span><span class="sxs-lookup"><span data-stu-id="b5381-149">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b5381-150">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="b5381-150">Response success and error codes</span></span>

<span data-ttu-id="b5381-151">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="b5381-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b5381-152">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="b5381-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b5381-153">A teljes listát lásd: [hibakódok](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b5381-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b5381-154">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="b5381-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
  "usageLocation": "country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "userid@domain.onmicrosoft.com",
  "firstName": "First",
  "lastName": "Last",
  "displayName": "User name",
  "immutableId": "Some unique ID",
  "passwordProfile": {
    "forceChangePassword": true,
    "password": "abCD123*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```