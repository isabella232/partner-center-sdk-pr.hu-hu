---
title: A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése
description: Ez a cikk azt ismerteti, hogyan lehet megerősítést kapni az ügyfelek általi Microsoft Cloud szerződés.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
aauthor: khakiali
ms.author: alikhaki
ms.openlocfilehash: 1b1a8cbacb667e579bcd218a29c3f553afce26c2
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549263"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-cloud-agreement"></a><span data-ttu-id="80359-103">A Microsoft Cloud szerződés ügyfél általi elfogadási megerősítésének lekérése</span><span class="sxs-lookup"><span data-stu-id="80359-103">Get confirmation of customer acceptance of Microsoft Cloud Agreement</span></span>

<span data-ttu-id="80359-104">**A következőkre vonatkozik:** Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="80359-104">**Applies to**: Partner Center</span></span>

<span data-ttu-id="80359-105">**Nem vonatkozik a következőre:** Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="80359-105">**Does not apply to**: Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="80359-106">A **Szerződés** erőforrást jelenleg csak a Microsoft Partnerközpont támogatja.</span><span class="sxs-lookup"><span data-stu-id="80359-106">The **Agreement** resource is currently supported by Partner Center only in the Microsoft public cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80359-107">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="80359-107">Prerequisites</span></span>

- <span data-ttu-id="80359-108">Ha az Partnerközpont .NET SDK-t használja, 1.9-es vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="80359-108">If you are using the Partner Center .NET SDK, version 1.9 or newer is required.</span></span>

- <span data-ttu-id="80359-109">Ha az Partnerközpont Java SDK-t használja, 1.8-as vagy újabb verzió szükséges.</span><span class="sxs-lookup"><span data-stu-id="80359-109">If you are using the Partner Center Java SDK, version 1.8 or newer is required.</span></span>

- <span data-ttu-id="80359-110">Hitelesítő adatok a Partnerközpont [leírtak szerint.](./partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="80359-110">Credentials as described in [Partner Center authentication](./partner-center-authentication.md).</span></span> <span data-ttu-id="80359-111">Ez a forgatókönyv csak az alkalmazás- és felhasználóhitelesítést támogatja.</span><span class="sxs-lookup"><span data-stu-id="80359-111">This scenario only supports app + user authentication.</span></span>

- <span data-ttu-id="80359-112">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80359-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80359-113">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="80359-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80359-114">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="80359-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80359-115">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="80359-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80359-116">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="80359-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80359-117">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80359-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="net-version-14-or-newer"></a><span data-ttu-id="80359-118">.NET (1.4-es vagy újabb verzió)</span><span class="sxs-lookup"><span data-stu-id="80359-118">.NET (version 1.4 or newer)</span></span>

<span data-ttu-id="80359-119">A korábban megadott ügyfél-elfogadás megerősítésének(i) lekérése:</span><span class="sxs-lookup"><span data-stu-id="80359-119">To retrieve confirmation(s) of customer acceptance that was previously provided:</span></span>

- <span data-ttu-id="80359-120">Használja az **IAggregatePartner.Customers gyűjteményt,** és hívja meg a **ById** metódust a megadott ügyfélazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="80359-120">Use the **IAggregatePartner.Customers** collection and call **ById** method with the specified customer identifier.</span></span>

- <span data-ttu-id="80359-121">A **ByAgreementType** metódus hívásával lekérheti a **Agreements** Microsoft Cloud szerződés, és szűrheti az eredményeket.</span><span class="sxs-lookup"><span data-stu-id="80359-121">Fetch the **Agreements** property and filter the results to Microsoft Cloud Agreement by calling **ByAgreementType** method.</span></span>

- <span data-ttu-id="80359-122">Hívja meg **a Get** vagy **a GetAsync metódust.**</span><span class="sxs-lookup"><span data-stu-id="80359-122">Call **Get** or **GetAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCloudAgreement";

var cloudAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

<span data-ttu-id="80359-123">A teljes minta megtalálható a [GetCustomerAgreements osztályban](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) a konzol tesztalkalmazás [projektjében.](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)</span><span class="sxs-lookup"><span data-stu-id="80359-123">A complete sample can be found in the [GetCustomerAgreements](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.</span></span>

## <a name="net-version-19---113"></a><span data-ttu-id="80359-124">.NET (1.9-es és 1.13-as verzió)</span><span class="sxs-lookup"><span data-stu-id="80359-124">.NET (version 1.9 - 1.13)</span></span>

<span data-ttu-id="80359-125">A korábban megadott ügyfél-elfogadás megerősítésének lekérése:</span><span class="sxs-lookup"><span data-stu-id="80359-125">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="80359-126">Használja az **IAggregatePartner.Customers** gyűjteményt, és hívja meg a **ById** metódust a megadott ügyfélazonosítóval.</span><span class="sxs-lookup"><span data-stu-id="80359-126">Use the **IAggregatePartner.Customers** collection and call the **ById** method with the specified customer's identifier.</span></span> <span data-ttu-id="80359-127">Ezután szerezze be **a Agreements** tulajdonságot, majd hívja meg a **Get** vagy **GetAsync metódusokat.**</span><span class="sxs-lookup"><span data-stu-id="80359-127">Then, get the **Agreements** property, followed by calling the **Get** or **GetAsync** methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var agreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.Get();
```

## <a name="java"></a><span data-ttu-id="80359-128">Java</span><span class="sxs-lookup"><span data-stu-id="80359-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="80359-129">A korábban megadott ügyfél-elfogadás megerősítésének lekérése:</span><span class="sxs-lookup"><span data-stu-id="80359-129">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="80359-130">Használja az **IAggregatePartner.getCustomers** függvényt, és hívja meg a **byId** függvényt a megadott ügyfél azonosítóval.</span><span class="sxs-lookup"><span data-stu-id="80359-130">Use the **IAggregatePartner.getCustomers** function and call the **byId** function with the specified customer's identifier.</span></span> <span data-ttu-id="80359-131">Ezután szerezze be a **getAgreements** függvényt, majd hívja meg a **get** függvényt.</span><span class="sxs-lookup"><span data-stu-id="80359-131">Then, get the **getAgreements** function, followed by calling the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;

ResourceCollection<Agreement> agreements = partnerOperations.getCustomers().byId(selectedCustomerId).getAgreements().get();
```

<span data-ttu-id="80359-132">A teljes minta megtalálható a [GetCustomerAgreements osztályban](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) a konzol tesztalkalmazás [projektjében.](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="80359-132">A complete sample can be found in the [GetCustomerAgreements](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetCustomerAgreements.java) class from the [console test app](https://github.com/Microsoft/Partner-Center-Java-Samples) project.</span></span>

## <a name="powershell"></a><span data-ttu-id="80359-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80359-133">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="80359-134">A korábban megadott ügyfél-elfogadás megerősítésének lekérése:</span><span class="sxs-lookup"><span data-stu-id="80359-134">To retrieve confirmation of customer acceptance provided previously:</span></span>

<span data-ttu-id="80359-135">Használja a [**Get-PartnerCustomerAgreement parancsot.**](/powershell/module/partnercenter/get-partnercustomeragreement)</span><span class="sxs-lookup"><span data-stu-id="80359-135">Use the [**Get-PartnerCustomerAgreement**](/powershell/module/partnercenter/get-partnercustomeragreement) command.</span></span>

```powershell
Get-PartnerCustomerAgreement -CustomerId '14876998-c0dc-46e6-9d0c-65a57a6c32ec'
```

## <a name="rest-request"></a><span data-ttu-id="80359-136">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="80359-136">REST request</span></span>

<span data-ttu-id="80359-137">A korábban megadott ügyfél-elfogadás megerősítésének lekérését az alábbi utasításokban láthatja.</span><span class="sxs-lookup"><span data-stu-id="80359-137">To retrieve confirmation of customer acceptance provided previously, see the following instructions.</span></span>

<span data-ttu-id="80359-138">Hozzon létre egy új **Szerződés** erőforrást a megfelelő tanúsítványinformációk alapján.</span><span class="sxs-lookup"><span data-stu-id="80359-138">Create a new **Agreement** resource with the relevant certification information.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80359-139">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="80359-139">Request syntax</span></span>

| <span data-ttu-id="80359-140">Metódus</span><span class="sxs-lookup"><span data-stu-id="80359-140">Method</span></span> | <span data-ttu-id="80359-141">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="80359-141">Request URI</span></span>                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80359-142">GET</span><span class="sxs-lookup"><span data-stu-id="80359-142">GET</span></span>    | <span data-ttu-id="80359-143">[*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="80359-143">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/agreements HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="80359-144">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="80359-144">URI parameter</span></span>

<span data-ttu-id="80359-145">A következő lekérdezési paraméterrel adhatja meg a megerősíteni kívánt ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="80359-145">Use the following query parameter to specify the customer you are confirming.</span></span>

| <span data-ttu-id="80359-146">Név</span><span class="sxs-lookup"><span data-stu-id="80359-146">Name</span></span>             | <span data-ttu-id="80359-147">Típus</span><span class="sxs-lookup"><span data-stu-id="80359-147">Type</span></span> | <span data-ttu-id="80359-148">Kötelező</span><span class="sxs-lookup"><span data-stu-id="80359-148">Required</span></span> | <span data-ttu-id="80359-149">Leírás</span><span class="sxs-lookup"><span data-stu-id="80359-149">Description</span></span>                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| <span data-ttu-id="80359-150">CustomerTenantId</span><span class="sxs-lookup"><span data-stu-id="80359-150">CustomerTenantId</span></span> | <span data-ttu-id="80359-151">GUID</span><span class="sxs-lookup"><span data-stu-id="80359-151">GUID</span></span> | <span data-ttu-id="80359-152">Y</span><span class="sxs-lookup"><span data-stu-id="80359-152">Y</span></span>        | <span data-ttu-id="80359-153">Az érték egy **CustomerTenantId** formátumú GUID, amely lehetővé teszi egy ügyfél megadását.</span><span class="sxs-lookup"><span data-stu-id="80359-153">The value is a GUID formatted **CustomerTenantId** that allows you to specify a customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80359-154">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="80359-154">Request headers</span></span>

<span data-ttu-id="80359-155">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="80359-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80359-156">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="80359-156">Request body</span></span>

<span data-ttu-id="80359-157">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="80359-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="80359-158">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="80359-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a><span data-ttu-id="80359-159">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="80359-159">REST response</span></span>

<span data-ttu-id="80359-160">Ha a művelet sikeres, ez a metódus **szerződéserőforrások** gyűjteményét adja vissza a válasz törzsében.</span><span class="sxs-lookup"><span data-stu-id="80359-160">If successful, this method returns a collection of **Agreement** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80359-161">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="80359-161">Response success and error codes</span></span>

<span data-ttu-id="80359-162">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="80359-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80359-163">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="80359-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80359-164">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="80359-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80359-165">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="80359-165">Response example</span></span>

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
