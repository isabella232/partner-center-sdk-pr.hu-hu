---
title: Rendelés visszavonása az integrációs védőfalból
description: Megtudhatja, hogyan használhatja Partnerközpont API-kat az integrációs sandbox-fiókokból származó előfizetési rendelések különböző típusainak lemondására.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c4b658f406e420d8d3cd425688364fe3d440d3d
ms.sourcegitcommit: a3a78ec0f5078645b5a4f3b534165eef30f2c822
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/30/2021
ms.locfileid: "113104971"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="8ca51-103">Rendelés visszavonása az integrációs védőfalról az Partnerközpont API-k használatával</span><span class="sxs-lookup"><span data-stu-id="8ca51-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="8ca51-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8ca51-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8ca51-105">Ez a cikk azt ismerteti, hogyan használhatók Partnerközpont API-k az integrációs sandbox-fiókokból származó előfizetési rendelések különböző típusainak lemondására.</span><span class="sxs-lookup"><span data-stu-id="8ca51-105">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="8ca51-106">Ilyen rendelések lehetnek fenntartott példányok, szoftverek és kereskedelmi piactéri Szolgáltatott szoftver (SaaS) előfizetési rendelések.</span><span class="sxs-lookup"><span data-stu-id="8ca51-106">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

> [!NOTE] 
> <span data-ttu-id="8ca51-107">Vegye figyelembe, hogy a fenntartott példányok vagy a kereskedelmi piactéri SaaS-előfizetési rendelések lemondása csak az integrációs sandbox-fiókokból lehetséges.</span><span class="sxs-lookup"><span data-stu-id="8ca51-107">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span> <span data-ttu-id="8ca51-108">A 60 napnál régebbi sandbox-rendelések nem szakíthatóak meg a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="8ca51-108">Any sandbox orders which are older than 60 days cannot be cancelled from Partner Center.</span></span>

<span data-ttu-id="8ca51-109">Az API-n keresztüli szoftverrendelések lemondásához használja a [cancel-software-purchases parancsot.](cancel-software-purchases.md)</span><span class="sxs-lookup"><span data-stu-id="8ca51-109">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="8ca51-110">Az irányítópulton keresztül is visszavonhatja az éles szoftverrendeléseket [a vásárlás lemondásával.](/partner-center/csp-software-subscriptions)</span><span class="sxs-lookup"><span data-stu-id="8ca51-110">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ca51-111">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8ca51-111">Prerequisites</span></span>

- <span data-ttu-id="8ca51-112">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8ca51-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8ca51-113">Ez a forgatókönyv támogatja a különálló alkalmazással és az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="8ca51-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8ca51-114">Integrációs sandbox partnerfiók egy olyan ügyféllel, aki aktív fenntartott példányokkal/szoftverekkel/külső SaaS-előfizetési rendelésekkel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="8ca51-114">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="8ca51-115">C\#</span><span class="sxs-lookup"><span data-stu-id="8ca51-115">C\#</span></span>

<span data-ttu-id="8ca51-116">Ha le kell mondania egy rendelést az integrációs védőfalról, adja át a fiók hitelesítő adatait a metódusnak a partnerműveleteket lekért [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) felület lekért felülethez.</span><span class="sxs-lookup"><span data-stu-id="8ca51-116">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="8ca51-117">Egy adott [](order-resources.md#order)rendelés kiválasztásához használja a partnerműveleteket és a hívási metódust az ügyfél azonosítóval az ügyfél azonosítójának megadásával, majd a rendelés azonosítóját a rendelés megadásához, végül pedig a lekérési [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) **`Orders.ById()`** **`Get`** **`GetAsync`** metódust.</span><span class="sxs-lookup"><span data-stu-id="8ca51-117">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="8ca51-118">Állítsa a [**`Order.Status`**](order-resources.md#order) tulajdonságot a következőre: `cancelled` , és használja a **`Patch()`** metódust a sorrend frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="8ca51-118">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="8ca51-119">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="8ca51-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8ca51-120">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="8ca51-120">Request syntax</span></span>

| <span data-ttu-id="8ca51-121">Metódus</span><span class="sxs-lookup"><span data-stu-id="8ca51-121">Method</span></span>     | <span data-ttu-id="8ca51-122">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="8ca51-122">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="8ca51-123">**Javítás**</span><span class="sxs-lookup"><span data-stu-id="8ca51-123">**PATCH**</span></span> | <span data-ttu-id="8ca51-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{rendelésazonosító} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8ca51-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8ca51-125">URI-paraméter</span><span class="sxs-lookup"><span data-stu-id="8ca51-125">URI parameter</span></span>

<span data-ttu-id="8ca51-126">Az alábbi lekérdezési paraméterrel törölhet egy ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="8ca51-126">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="8ca51-127">Név</span><span class="sxs-lookup"><span data-stu-id="8ca51-127">Name</span></span>                   | <span data-ttu-id="8ca51-128">Típus</span><span class="sxs-lookup"><span data-stu-id="8ca51-128">Type</span></span>     | <span data-ttu-id="8ca51-129">Kötelező</span><span class="sxs-lookup"><span data-stu-id="8ca51-129">Required</span></span> | <span data-ttu-id="8ca51-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="8ca51-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8ca51-131">**ügyfél-bérlő-azonosító**</span><span class="sxs-lookup"><span data-stu-id="8ca51-131">**customer-tenant-id**</span></span> | <span data-ttu-id="8ca51-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="8ca51-132">**guid**</span></span> | <span data-ttu-id="8ca51-133">Y</span><span class="sxs-lookup"><span data-stu-id="8ca51-133">Y</span></span>        | <span data-ttu-id="8ca51-134">Az érték egy GUID formátumú **ügyfél-bérlő-azonosító,** amely lehetővé teszi a viszonteladó számára, hogy szűrje a viszonteladóhoz tartozó adott ügyfél eredményeit.</span><span class="sxs-lookup"><span data-stu-id="8ca51-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="8ca51-135">**order-id (rendelésazonosító)**</span><span class="sxs-lookup"><span data-stu-id="8ca51-135">**order-id**</span></span> | <span data-ttu-id="8ca51-136">**sztring**</span><span class="sxs-lookup"><span data-stu-id="8ca51-136">**string**</span></span> | <span data-ttu-id="8ca51-137">Y</span><span class="sxs-lookup"><span data-stu-id="8ca51-137">Y</span></span>        | <span data-ttu-id="8ca51-138">Az érték egy sztring, amely a megszakítani szükséges rendelési értékeket jegyzett meg.</span><span class="sxs-lookup"><span data-stu-id="8ca51-138">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8ca51-139">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="8ca51-139">Request headers</span></span>

<span data-ttu-id="8ca51-140">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8ca51-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8ca51-141">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="8ca51-141">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="8ca51-142">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8ca51-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a><span data-ttu-id="8ca51-143">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="8ca51-143">REST response</span></span>

<span data-ttu-id="8ca51-144">Ha a művelet sikeres, ez a metódus a megszakított rendelést adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8ca51-144">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8ca51-145">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="8ca51-145">Response success and error codes</span></span>

<span data-ttu-id="8ca51-146">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="8ca51-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8ca51-147">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="8ca51-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8ca51-148">A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8ca51-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8ca51-149">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8ca51-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
