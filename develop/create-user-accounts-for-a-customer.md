---
title: Felhasználói fiókok létrehozása egy ügyfélnél
description: Hozzon létre egy új felhasználói fiókot az ügyfél számára.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d086d7ba72c9d9e42dc88684ddeafc9a597bfd7c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973383"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="34987-103">Felhasználói fiókok létrehozása egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="34987-103">Create user accounts for a customer</span></span>

<span data-ttu-id="34987-104">Hozzon létre egy új felhasználói fiókot az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="34987-104">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34987-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="34987-105">Prerequisites</span></span>

- <span data-ttu-id="34987-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="34987-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="34987-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="34987-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="34987-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="34987-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="34987-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="34987-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="34987-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="34987-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="34987-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="34987-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="34987-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="34987-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="34987-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="34987-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="34987-114">C\#</span><span class="sxs-lookup"><span data-stu-id="34987-114">C\#</span></span>

<span data-ttu-id="34987-115">Új felhasználói fiók beszerzése egy ügyfél számára:</span><span class="sxs-lookup"><span data-stu-id="34987-115">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="34987-116">Hozzon létre egy **új CustomerUser** objektumot a megfelelő felhasználói adatokkal.</span><span class="sxs-lookup"><span data-stu-id="34987-116">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="34987-117">Használja az **IAggregatePartner.Customers gyűjteményt,** és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="34987-117">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="34987-118">Hívja meg **a Users tulajdonságot,** majd a **Create metódust.**</span><span class="sxs-lookup"><span data-stu-id="34987-118">Call the **Users** property, followed by the **Create** method.</span></span>

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

<span data-ttu-id="34987-119">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="34987-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="34987-120">**Project:** PartnerSDK.FeatureSamples **osztály:** CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="34987-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="34987-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="34987-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="34987-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="34987-122">Request syntax</span></span>

| <span data-ttu-id="34987-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="34987-123">Method</span></span>   | <span data-ttu-id="34987-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="34987-124">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="34987-125">**Post**</span><span class="sxs-lookup"><span data-stu-id="34987-125">**POST**</span></span> | <span data-ttu-id="34987-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="34987-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="34987-127">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="34987-127">URI parameters</span></span>

<span data-ttu-id="34987-128">Az alábbi lekérdezési paraméterekkel azonosíthatja a megfelelő ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="34987-128">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="34987-129">Név</span><span class="sxs-lookup"><span data-stu-id="34987-129">Name</span></span> | <span data-ttu-id="34987-130">Típus</span><span class="sxs-lookup"><span data-stu-id="34987-130">Type</span></span> | <span data-ttu-id="34987-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="34987-131">Required</span></span> | <span data-ttu-id="34987-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="34987-132">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="34987-133">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="34987-133">**customer-tenant-id**</span></span> | <span data-ttu-id="34987-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="34987-134">**guid**</span></span> | <span data-ttu-id="34987-135">Y</span><span class="sxs-lookup"><span data-stu-id="34987-135">Y</span></span> | <span data-ttu-id="34987-136">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító.** Lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfélre szűrje az eredményeket.</span><span class="sxs-lookup"><span data-stu-id="34987-136">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="34987-137">**felhasználóazonosító**</span><span class="sxs-lookup"><span data-stu-id="34987-137">**user-id**</span></span> | <span data-ttu-id="34987-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="34987-138">**guid**</span></span> | <span data-ttu-id="34987-139">N</span><span class="sxs-lookup"><span data-stu-id="34987-139">N</span></span> | <span data-ttu-id="34987-140">Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="34987-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="34987-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="34987-141">Request headers</span></span>

<span data-ttu-id="34987-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="34987-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="34987-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="34987-143">Request body</span></span>

<span data-ttu-id="34987-144">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="34987-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="34987-145">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="34987-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="34987-146">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="34987-146">REST response</span></span>

<span data-ttu-id="34987-147">Sikeres művelet esetén ez a metódus egy felhasználói fiókot ad vissza, a GUID azonosítóval együtt.</span><span class="sxs-lookup"><span data-stu-id="34987-147">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="34987-148">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="34987-148">Response success and error codes</span></span>

<span data-ttu-id="34987-149">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="34987-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="34987-150">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="34987-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="34987-151">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="34987-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="34987-152">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="34987-152">Response example</span></span>

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