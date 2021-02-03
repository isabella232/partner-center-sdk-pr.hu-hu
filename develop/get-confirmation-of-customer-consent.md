---
title: A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősíteni a Microsoft Cloud szerződés ügyfél általi elfogadását.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: d91f70cbd8bc9b8622b8d41ab9e601e2aee2cfab
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/19/2020
ms.locfileid: "97768447"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="4bd00-103">A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése</span><span class="sxs-lookup"><span data-stu-id="4bd00-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="4bd00-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="4bd00-104">**Applies To**</span></span>

- <span data-ttu-id="4bd00-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="4bd00-105">Partner Center</span></span>

> [!NOTE]
> <span data-ttu-id="4bd00-106">A partner Center jelenleg csak a Microsoft nyilvános felhőben támogatja a **szerződési** erőforrást.</span><span class="sxs-lookup"><span data-stu-id="4bd00-106">The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only.</span></span> <span data-ttu-id="4bd00-107">Nem alkalmazható a következőre:</span><span class="sxs-lookup"><span data-stu-id="4bd00-107">It isn't applicable to:</span></span>
>
> - <span data-ttu-id="4bd00-108">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="4bd00-108">Partner Center operated by 21Vianet</span></span>
> - <span data-ttu-id="4bd00-109">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4bd00-109">Partner Center for Microsoft Cloud Germany</span></span>
> - <span data-ttu-id="4bd00-110">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="4bd00-110">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4bd00-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="4bd00-111">Prerequisites</span></span>

- <span data-ttu-id="4bd00-112">Ha a partner Center .NET SDK-t használja, a 1,9-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="4bd00-112">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="4bd00-113">Ha a partner Center Java SDK-t használja, a 1,8-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="4bd00-113">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="4bd00-114">A [partner Center-hitelesítésben](./partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="4bd00-114">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="4bd00-115">Ez a forgatókönyv csak az App + felhasználói hitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="4bd00-115">This scenario supports only supports app + user authentication.</span></span>

- <span data-ttu-id="4bd00-116">Ügyfél-azonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4bd00-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4bd00-117">Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard).</span><span class="sxs-lookup"><span data-stu-id="4bd00-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4bd00-118">Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**.</span><span class="sxs-lookup"><span data-stu-id="4bd00-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4bd00-119">Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="4bd00-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4bd00-120">Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="4bd00-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4bd00-121">A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4bd00-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="4bd00-122">.NET (1,4-es vagy újabb verzió)</span><span class="sxs-lookup"><span data-stu-id="4bd00-122">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="4bd00-123">A korábban megadott ügyfél-elfogadás megerősítése (i) beolvasása:</span><span class="sxs-lookup"><span data-stu-id="4bd00-123">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="4bd00-124">Használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="4bd00-124">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="4bd00-125">A **ByAgreementType** metódus meghívásával olvassa be a **szerződések** tulajdonságot, és szűrje Microsoft Cloud szerződés eredményét.</span><span class="sxs-lookup"><span data-stu-id="4bd00-125">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="4bd00-126">A **Get** vagy a **GetAsync** metódus hívása.</span><span class="sxs-lookup"><span data-stu-id="4bd00-126">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="4bd00-127">Teljes minta a [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) osztályban található a [konzol tesztelése alkalmazás](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="4bd00-127">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="4bd00-128">.NET (1,9-1,13-es verzió)</span><span class="sxs-lookup"><span data-stu-id="4bd00-128">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="4bd00-129">A korábban megadott ügyfél-elfogadás megerősítésének lekérése:</span><span class="sxs-lookup"><span data-stu-id="4bd00-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="4bd00-130">Használja a **IAggregatePartner. Customs** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="4bd00-130">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="4bd00-131">Ezután szerezze be a **szerződések** tulajdonságot, majd a **Get** vagy a **GetAsync** metódus meghívásával.</span><span class="sxs-lookup"><span data-stu-id="4bd00-131">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="4bd00-132">Java</span><span class="sxs-lookup"><span data-stu-id="4bd00-132">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="4bd00-133">A korábban megadott ügyfél-elfogadás megerősítésének lekérése:</span><span class="sxs-lookup"><span data-stu-id="4bd00-133">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="4bd00-134">Használja a **IAggregatePartner. getCustomers** függvényt, és hívja meg a **byId** függvényt a megadott ügyfél-azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="4bd00-134">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="4bd00-135">Ezután szerezze be a **getAgreements** függvényt, majd a **Get** függvény meghívásával.</span><span class="sxs-lookup"><span data-stu-id="4bd00-135">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="4bd00-136">Teljes minta a [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) osztályban található a [konzol tesztelése alkalmazás](https://github.com/Microsoft/Partner-Center-Java-Samples) projektben.</span><span class="sxs-lookup"><span data-stu-id="4bd00-136">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="4bd00-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bd00-137">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="4bd00-138">A korábban megadott ügyfél-elfogadás megerősítésének lekérése:</span><span class="sxs-lookup"><span data-stu-id="4bd00-138">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="4bd00-139">Használja a [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) parancsot.</span><span class="sxs-lookup"><span data-stu-id="4bd00-139">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="4bd00-140">REST-kérelem</span><span class="sxs-lookup"><span data-stu-id="4bd00-140">REST request</span></span>

<span data-ttu-id="4bd00-141">A korábban megadott ügyfél-elfogadás megerősítésének lekéréséhez tekintse meg az alábbi utasításokat.</span><span class="sxs-lookup"><span data-stu-id="4bd00-141">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="4bd00-142">Hozzon létre egy új **szerződési** erőforrást a megfelelő minősítési információkkal.</span><span class="sxs-lookup"><span data-stu-id="4bd00-142">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4bd00-143">Kérelem szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4bd00-143">Request syntax</span></span>

| <span data-ttu-id="4bd00-144">Metódus</span><span class="sxs-lookup"><span data-stu-id="4bd00-144">Method</span></span> | <span data-ttu-id="4bd00-145">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="4bd00-145">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4bd00-146">GET</span><span class="sxs-lookup"><span data-stu-id="4bd00-146">GET</span></span>    | <span data-ttu-id="4bd00-147">[*\{ BASEURL \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Agreements http/1.1</span><span class="sxs-lookup"><span data-stu-id="4bd00-147">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="4bd00-148">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="4bd00-148">URI parameter</span></span>

<span data-ttu-id="4bd00-149">A következő lekérdezési paraméterrel adhatja meg a megerősítő ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="4bd00-149">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="4bd00-150">Név</span><span class="sxs-lookup"><span data-stu-id="4bd00-150">Name</span></span>             | <span data-ttu-id="4bd00-151">Típus</span><span class="sxs-lookup"><span data-stu-id="4bd00-151">Type</span></span> | <span data-ttu-id="4bd00-152">Kötelező</span><span class="sxs-lookup"><span data-stu-id="4bd00-152">Required</span></span> | <span data-ttu-id="4bd00-153">Leírás</span><span class="sxs-lookup"><span data-stu-id="4bd00-153">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="4bd00-154">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="4bd00-154">CustomerTenantId</span></span> | <span data-ttu-id="4bd00-155">GUID</span><span class="sxs-lookup"><span data-stu-id="4bd00-155">GUID</span></span> | <span data-ttu-id="4bd00-156">Y</span><span class="sxs-lookup"><span data-stu-id="4bd00-156">Y</span></span>        | <span data-ttu-id="4bd00-157">Az érték egy GUID formátumú **CustomerTenantId** , amely lehetővé teszi az ügyfél megadását.</span><span class="sxs-lookup"><span data-stu-id="4bd00-157">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4bd00-158">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="4bd00-158">Request headers</span></span>

<span data-ttu-id="4bd00-159">További információ: a [partneri központ Rest-fejlécei](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4bd00-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4bd00-160">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="4bd00-160">Request body</span></span>

<span data-ttu-id="4bd00-161">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="4bd00-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4bd00-162">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="4bd00-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="4bd00-163">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="4bd00-163">REST response</span></span>

<span data-ttu-id="4bd00-164">Ha ez sikeres, ez a metódus a válasz törzsében a **Szerződés** erőforrásainak gyűjteményét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="4bd00-164">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4bd00-165">Válasz sikeres és hibakódok</span><span class="sxs-lookup"><span data-stu-id="4bd00-165">Response success and error codes</span></span>

<span data-ttu-id="4bd00-166">Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi.</span><span class="sxs-lookup"><span data-stu-id="4bd00-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4bd00-167">A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt.</span><span class="sxs-lookup"><span data-stu-id="4bd00-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4bd00-168">A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.</span><span class="sxs-lookup"><span data-stu-id="4bd00-168">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4bd00-169">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="4bd00-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2018-07-28T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@Outlook.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"998b88de-aa99-4388-a42c-1b3517d49490",
            "dateAgreed":"2017-08-01T00:00:00",
            "type":"MicrosoftCloudAgreement",
            "agreementLink":"https://docs.microsoft.com/partner-center/agreements"
        }
    ]
}
```
