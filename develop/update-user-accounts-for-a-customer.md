---
title: Felhasználói fiókok frissítése egy ügyfélnél
description: Frissítse egy meglévő felhasználói fiók adatait az ügyfél számára.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ebfdbb5df1d56416835af771fd6b70190776012
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445272"
---
# <a name="update-user-accounts-for-a-customer"></a><span data-ttu-id="59316-103">Felhasználói fiókok frissítése egy ügyfélnél</span><span class="sxs-lookup"><span data-stu-id="59316-103">Update user accounts for a customer</span></span>

<span data-ttu-id="59316-104">Frissítse egy meglévő felhasználói fiók adatait az ügyfél számára.</span><span class="sxs-lookup"><span data-stu-id="59316-104">Update details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59316-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="59316-105">Prerequisites</span></span>

- <span data-ttu-id="59316-106">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="59316-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="59316-107">Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="59316-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="59316-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59316-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="59316-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="59316-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="59316-110">Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="59316-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="59316-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="59316-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="59316-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="59316-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="59316-113">A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59316-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="59316-114">C\#</span><span class="sxs-lookup"><span data-stu-id="59316-114">C\#</span></span>

<span data-ttu-id="59316-115">Egy adott ügyfélfelhasználó részleteinek frissítéséhez először le kellkérni a megadott ügyfél-azonosítót és a frissíthető felhasználót.</span><span class="sxs-lookup"><span data-stu-id="59316-115">To update the details for a specified customer user, first retrieve the specified customer ID and user to update.</span></span> <span data-ttu-id="59316-116">Ezután hozza létre a felhasználó frissített verzióját egy új **CustomerUser objektumban.**</span><span class="sxs-lookup"><span data-stu-id="59316-116">Then, create an updated version of the user in a new **CustomerUser** object.</span></span> <span data-ttu-id="59316-117">Ezután használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById() metódust.**</span><span class="sxs-lookup"><span data-stu-id="59316-117">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="59316-118">Ezután hívja **meg a Users tulajdonságot,** a **ById()** metódust, majd a **Patch() metódust.**</span><span class="sxs-lookup"><span data-stu-id="59316-118">Then call the **Users** property, the **ById()** method, followed by the **Patch()** method.</span></span>

``` csharp
// string selectedCustomerId;
// customerUser specifiedUser;
// IAggregatePartner partnerOperations;

// Updated information
var userToUpdate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "testPw@!122B" },
    DisplayName = "DisplayNameChange",
    FirstName = "FirstNameChange",
    LastName = "LastNameChange",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

// Update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="59316-119">**Minta:** [Konzoltesztalkalmazás.](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="59316-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="59316-120">**Project**: PartnerSDK.FeatureSamples **osztály:** CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="59316-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="59316-121">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="59316-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="59316-122">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="59316-122">Request syntax</span></span>

| <span data-ttu-id="59316-123">Metódus</span><span class="sxs-lookup"><span data-stu-id="59316-123">Method</span></span>    | <span data-ttu-id="59316-124">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="59316-124">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="59316-125">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="59316-125">**PATCH**</span></span> | <span data-ttu-id="59316-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="59316-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="59316-127">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="59316-127">URI parameter</span></span>

<span data-ttu-id="59316-128">A következő lekérdezési paraméterrel azonosíthatja a megfelelő ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="59316-128">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="59316-129">Név</span><span class="sxs-lookup"><span data-stu-id="59316-129">Name</span></span>                   | <span data-ttu-id="59316-130">Típus</span><span class="sxs-lookup"><span data-stu-id="59316-130">Type</span></span>     | <span data-ttu-id="59316-131">Kötelező</span><span class="sxs-lookup"><span data-stu-id="59316-131">Required</span></span> | <span data-ttu-id="59316-132">Leírás</span><span class="sxs-lookup"><span data-stu-id="59316-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="59316-133">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="59316-133">**customer-tenant-id**</span></span> | <span data-ttu-id="59316-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="59316-134">**guid**</span></span> | <span data-ttu-id="59316-135">Y</span><span class="sxs-lookup"><span data-stu-id="59316-135">Y</span></span>        | <span data-ttu-id="59316-136">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="59316-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="59316-137">**felhasználói azonosító**</span><span class="sxs-lookup"><span data-stu-id="59316-137">**user-id**</span></span>            | <span data-ttu-id="59316-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="59316-138">**guid**</span></span> | <span data-ttu-id="59316-139">Y</span><span class="sxs-lookup"><span data-stu-id="59316-139">Y</span></span>        | <span data-ttu-id="59316-140">Az érték egy GUID formátumú felhasználói **azonosító,** amely egyetlen felhasználói fiókhoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="59316-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="59316-141">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="59316-141">Request headers</span></span>

<span data-ttu-id="59316-142">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="59316-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="59316-143">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="59316-143">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="59316-144">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="59316-144">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "new country/region code",

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="59316-145">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="59316-145">REST response</span></span>

<span data-ttu-id="59316-146">Ha ez a módszer sikeres, a frissített adatokat használó felhasználói fiókot ad vissza.</span><span class="sxs-lookup"><span data-stu-id="59316-146">If successful, this method returns a user account with the updated information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="59316-147">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="59316-147">Response success and error codes</span></span>

<span data-ttu-id="59316-148">Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="59316-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="59316-149">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="59316-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="59316-150">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="59316-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="59316-151">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="59316-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "new country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "emailidchange@abcdefgh1234.ccsctp.net",
  "firstName": "FirstNameChange",
  "lastName": "LastNameChange",
  "displayName": "DisplayNameChange",
  "userDomainType": "none",
  "state": "active",
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/4b10bf41-ab11-40e3-8c53-cd67849b50de",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
