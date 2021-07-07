---
title: Jogosultságok gyűjteményének lekérése
description: Jogosultságok gyűjteményének begyűjtése.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7bb8d3aefb11fae0af4bce790b41598d935de57c
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906422"
---
# <a name="get-a-collection-of-entitlements"></a><span data-ttu-id="ec06d-103">Jogosultságok gyűjteményének lekérése</span><span class="sxs-lookup"><span data-stu-id="ec06d-103">Get a collection of entitlements</span></span>

<span data-ttu-id="ec06d-104">Jogosultságok gyűjteményének begyűjtése.</span><span class="sxs-lookup"><span data-stu-id="ec06d-104">How to get a collection of entitlements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec06d-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="ec06d-105">Prerequisites</span></span>

- <span data-ttu-id="ec06d-106">Hitelesítő adatok a Partnerközpont [leírtak szerint.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ec06d-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ec06d-107">Ez a forgatókönyv támogatja az App+User hitelesítő adatokkal történő hitelesítést.</span><span class="sxs-lookup"><span data-stu-id="ec06d-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="ec06d-108">Egy ügyfélazonosító ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec06d-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ec06d-109">Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="ec06d-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ec06d-110">Válassza **ki a CSP** elemet Partnerközpont menüből, majd válassza az **Ügyfelek lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ec06d-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ec06d-111">Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.**</span><span class="sxs-lookup"><span data-stu-id="ec06d-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ec06d-112">Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.**</span><span class="sxs-lookup"><span data-stu-id="ec06d-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ec06d-113">A Microsoft-azonosító megegyezik az ügyfél-azonosítóval ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ec06d-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="ec06d-114">C\#</span><span class="sxs-lookup"><span data-stu-id="ec06d-114">C\#</span></span>

<span data-ttu-id="ec06d-115">Az ügyfél jogosultsággyűjteményének beszerzéséhez szerezze [](entitlement-resources.md#entitlement) be a jogosultsági műveletek felületét az [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódus az ügyfél azonosítójával való hívásával az ügyfél azonosításához.</span><span class="sxs-lookup"><span data-stu-id="ec06d-115">To get an entitlements collection for a customer, obtain an interface to [**Entitlement**](entitlement-resources.md#entitlement) operations by calling the  [**IAggregatePartner.Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="ec06d-116">Ezután olvassa be a felületet a **Jogosultságok** tulajdonságból, és hívja meg a **Get() vagy** **a GetAsync()** metódust a jogosultságok gyűjteményének lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="ec06d-116">Then, retrieve the interface from the **Entitlements** property and call the **Get()** or **GetAsync()** method to retrieve the collection of entitlements.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;

// Get the collection of entitlements.
var entitlements = partnerOperations.Customers.ById(customerId).Entitlements.Get();
```

<span data-ttu-id="ec06d-117">A lekért jogosultságok lejárati dátumának feltöltéséhez hívja meg ugyanezeket a fenti metódusokat, és állítsa a **showExpiry** opcionális logikai paramétert true **Get(true)** vagy **GetAsync(true) (igaz) értékre.**</span><span class="sxs-lookup"><span data-stu-id="ec06d-117">To populate expiry dates for the entitlements to be retrieved, call the same methods above and set the optional boolean parameter **showExpiry** to true **Get(true)** or **GetAsync(true)**.</span></span> <span data-ttu-id="ec06d-118">Ez azt jelzi, hogy a jogosultság lejárati dátumai kötelezőek (ha vannak).</span><span class="sxs-lookup"><span data-stu-id="ec06d-118">This indicates that entitlement expiry dates are required (when applicable).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec06d-119">A saját jogosultságtípusok nem lejárati dátumokkal.</span><span class="sxs-lookup"><span data-stu-id="ec06d-119">On-premise entitlement types do not have expiry dates.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ec06d-120">REST-kérés</span><span class="sxs-lookup"><span data-stu-id="ec06d-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ec06d-121">Kérés szintaxisa</span><span class="sxs-lookup"><span data-stu-id="ec06d-121">Request syntax</span></span>

| <span data-ttu-id="ec06d-122">Metódus</span><span class="sxs-lookup"><span data-stu-id="ec06d-122">Method</span></span> | <span data-ttu-id="ec06d-123">Kérés URI-ja</span><span class="sxs-lookup"><span data-stu-id="ec06d-123">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="ec06d-124">**Kap**</span><span class="sxs-lookup"><span data-stu-id="ec06d-124">**GET**</span></span> | <span data-ttu-id="ec06d-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ec06d-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/entitlements HTTP/1.1</span></span>                            |

### <a name="uri-parameters"></a><span data-ttu-id="ec06d-126">URI-paraméterek</span><span class="sxs-lookup"><span data-stu-id="ec06d-126">URI parameters</span></span>

<span data-ttu-id="ec06d-127">A kérelem létrehozásakor használja a következő elérési utat és lekérdezési paramétereket.</span><span class="sxs-lookup"><span data-stu-id="ec06d-127">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="ec06d-128">Név</span><span class="sxs-lookup"><span data-stu-id="ec06d-128">Name</span></span> | <span data-ttu-id="ec06d-129">Típus</span><span class="sxs-lookup"><span data-stu-id="ec06d-129">Type</span></span> | <span data-ttu-id="ec06d-130">Kötelező</span><span class="sxs-lookup"><span data-stu-id="ec06d-130">Required</span></span> | <span data-ttu-id="ec06d-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="ec06d-131">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="ec06d-132">customerId</span><span class="sxs-lookup"><span data-stu-id="ec06d-132">customerId</span></span> | <span data-ttu-id="ec06d-133">sztring</span><span class="sxs-lookup"><span data-stu-id="ec06d-133">string</span></span> | <span data-ttu-id="ec06d-134">Igen</span><span class="sxs-lookup"><span data-stu-id="ec06d-134">Yes</span></span> | <span data-ttu-id="ec06d-135">Egy GUID formátumú customerId, amely azonosítja az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="ec06d-135">A GUID formatted customerId that identifies the customer.</span></span> |
| <span data-ttu-id="ec06d-136">entitlementType (jogosultságtípus)</span><span class="sxs-lookup"><span data-stu-id="ec06d-136">entitlementType</span></span> | <span data-ttu-id="ec06d-137">sztring</span><span class="sxs-lookup"><span data-stu-id="ec06d-137">string</span></span> | <span data-ttu-id="ec06d-138">No</span><span class="sxs-lookup"><span data-stu-id="ec06d-138">No</span></span> | <span data-ttu-id="ec06d-139">A lekérni kívánt jogosultságok típusának megadására használható (**szoftver** vagy **reservedInstance** ).</span><span class="sxs-lookup"><span data-stu-id="ec06d-139">Can be used to specify the type of entitlements to be retrieved (**software** or **reservedInstance** ).</span></span> <span data-ttu-id="ec06d-140">Ha nincs beállítva, a program minden típust lekér</span><span class="sxs-lookup"><span data-stu-id="ec06d-140">If not set, all types will be retrieved</span></span> |
| <span data-ttu-id="ec06d-141">showExpiry</span><span class="sxs-lookup"><span data-stu-id="ec06d-141">showExpiry</span></span> | <span data-ttu-id="ec06d-142">boolean</span><span class="sxs-lookup"><span data-stu-id="ec06d-142">boolean</span></span> | <span data-ttu-id="ec06d-143">Nem</span><span class="sxs-lookup"><span data-stu-id="ec06d-143">No</span></span> | <span data-ttu-id="ec06d-144">Nem kötelező jelző, amely jelzi, hogy szükség van-e a jogosultságok lejárati dátumokra.</span><span class="sxs-lookup"><span data-stu-id="ec06d-144">Optional flag that indicates if entitlements expiry dates are required.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ec06d-145">Kérésfejlécek</span><span class="sxs-lookup"><span data-stu-id="ec06d-145">Request headers</span></span>

<span data-ttu-id="ec06d-146">További információ: [REST Partnerközpont fejlécek.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ec06d-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ec06d-147">A kérés törzse</span><span class="sxs-lookup"><span data-stu-id="ec06d-147">Request body</span></span>

<span data-ttu-id="ec06d-148">Nincsenek.</span><span class="sxs-lookup"><span data-stu-id="ec06d-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ec06d-149">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ec06d-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/entitlements HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="ec06d-150">REST-válasz</span><span class="sxs-lookup"><span data-stu-id="ec06d-150">REST response</span></span>

<span data-ttu-id="ec06d-151">Ha ez sikeres, a válasz törzse jogosultság-erőforrások [gyűjteményét](entitlement-resources.md#entitlement) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ec06d-151">If successful, the response body contains a collection of [Entitlement](entitlement-resources.md#entitlement) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ec06d-152">Sikeres válasz és hibakódok</span><span class="sxs-lookup"><span data-stu-id="ec06d-152">Response success and error codes</span></span>

<span data-ttu-id="ec06d-153">Minden válaszhoz egy HTTP-állapotkód is jár, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat.</span><span class="sxs-lookup"><span data-stu-id="ec06d-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ec06d-154">Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be.</span><span class="sxs-lookup"><span data-stu-id="ec06d-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ec06d-155">A teljes listát lásd: [Hibakódok.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ec06d-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ec06d-156">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ec06d-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 103778
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: EjFdw8fCpkKyMyza.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:42:51 GMT

{
  "totalCount": 2,
  "items": [
    {
      "includedEntitlements": [],
      "referenceOrder": {
        "id": "KaJ8XvkKc_GoNZOUyjVaRJalTBN5MWdV1",
        "lineItemId": "0"
      },
      "productId": "DZH318Z0BQ3W",
      "quantity": 1,
      "entitledArtifacts": [
        {
          "link": {
            "uri": "/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336",
            "method": "GET",
            "headers": []
          },
          "resourceId": "ebf2e74b-630e-4a09-857d-a1f6c6351336",
          "artifactType": "reservedinstance"
        }
      ],
      "skuId": "007J",
      "entitlementType": "reservedinstance"
      "dynamicAttributes": {
               "reservationType": "virtualmachines"
        }
    },
    {
      "includedEntitlements": [
        {
          "includedEntitlements": [],
          "referenceOrder": {
              "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
              "lineItemId": "0"
          },
          "productId": "DG7GMGF0DWTJ",
          "quantity": 1,
          "entitledArtifacts": [],
          "skuId": "0001",
          "entitlementType": "software"
        },
        {
          "includedEntitlements": [],
          "referenceOrder": {
            "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
            "lineItemId": "0"
          },
            "productId": "DG7GMGF0DWLG",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
          }
        ],
        "referenceOrder": {
          "id": "NUXMSvmS20EQ4kFsZmzkSqb747fqKmNk1",
          "lineItemId": "0"
        },
        "productId": "DG7GMGF0DWTK",
        "quantity": 1,
        "entitledArtifacts": [],
        "skuId": "0002",
        "entitlementType": "software"
    }
  ],
  "attributes": {
    "objectType": "Collection"
  }
}
```

## <a name="additional-examples"></a><span data-ttu-id="ec06d-157">További példák</span><span class="sxs-lookup"><span data-stu-id="ec06d-157">Additional Examples</span></span>

<span data-ttu-id="ec06d-158">Az alábbi példa bemutatja, hogyan lehet lekérni egy adott típusú jogosultságot és lejárati dátumokat (ha van)</span><span class="sxs-lookup"><span data-stu-id="ec06d-158">The following example shows you how to retrieve a specific type of entitlements along with expiry dates (when applicable)</span></span>

### <a name="c-example"></a><span data-ttu-id="ec06d-159">C \# példa</span><span class="sxs-lookup"><span data-stu-id="ec06d-159">C\# example</span></span>

<span data-ttu-id="ec06d-160">Egy adott típusú jogosultság lekérése érdekében szerezze be a **ByEntitlementType** felületet a **Jogosultságok** felületről, és használja a **Get() vagy** **GetAsync() metódusokat.**</span><span class="sxs-lookup"><span data-stu-id="ec06d-160">To retrieve a specific type of entitlements, obtain the **ByEntitlementType** interface from the **Entitlements** interface and use the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("software").Get(true);
```

### <a name="request-example"></a><span data-ttu-id="ec06d-161">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ec06d-161">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/de3dcef9-9991-459c-ac71-2903d1127414/entitlements?entitlementtype=software&showExpiry=true
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="ec06d-162">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ec06d-162">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1791
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d9eb8194-9b99-4057-a2fe-98bdf05f013c
MS-RequestId: 6517a410-67ce-4995-9bb7-116a52179f92
X-Locale: en-US
MS-CV: yD+4LBKePUSp/vqJ.0
MS-ServerId: 000002
Date: Mon, 28 Jan 2019 18:31:43 GMT

{
    "totalCount": 2,
    "items": [
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWM2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "0",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWMK",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0001",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "0",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWM3",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0002",
            "entitlementType": "software"
        },
        {
            "includedEntitlements": [
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV1",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                },
                {
                    "includedEntitlements": [],
                    "referenceOrder": {
                        "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                        "lineItemId": "1",
                        "alternateId": "8f3af3dea1ea"
                    },
                    "productId": "DG7GMGF0DWV2",
                    "quantity": 1,
                    "entitledArtifacts": [],
                    "skuId": "0002",
                    "entitlementType": "software"
                }
            ],
            "referenceOrder": {
                "id": "4teYMtWYEeKM77JftGLIQYMOZPTwyOEV1",
                "lineItemId": "1",
                "alternateId": "8f3af3dea1ea"
            },
            "productId": "DG7GMGF0DWBQ",
            "quantity": 1,
            "entitledArtifacts": [],
            "skuId": "0003",
            "entitlementType": "software",
            "expiryDate": "2022-01-28T00:00:00Z"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

<span data-ttu-id="ec06d-163">Az alábbi példák bemutatják, hogyan lehet lekérni a termékekkel és foglalásokkal kapcsolatos információkat egy jogosultságból.</span><span class="sxs-lookup"><span data-stu-id="ec06d-163">The following examples show you how to retrieve information about products and reservations from an entitlement.</span></span>

### <a name="retrieve-virtual-machine-reservation-details-from-an-entitlement-by-using-sdk-v18"></a><span data-ttu-id="ec06d-164">Virtuális gép foglalási részleteinek lekérése jogosultságból az SDK 1.8-as verziójával</span><span class="sxs-lookup"><span data-stu-id="ec06d-164">Retrieve virtual machine reservation details from an entitlement by using SDK V1.8</span></span>

### <a name="c-example"></a><span data-ttu-id="ec06d-165">C \# példa</span><span class="sxs-lookup"><span data-stu-id="ec06d-165">C\# example</span></span>

<span data-ttu-id="ec06d-166">A virtuális gépek foglalásával kapcsolatos további részletek jogosultságból való lekérése érdekében hívja meg az összetevőtípus = entitledArtifacts.link alatt elérhetővé virtual_machine_reserved_instance.</span><span class="sxs-lookup"><span data-stu-id="ec06d-166">To retrieve more details related to the virtual machine reservations from an entitlement, invoke the URI exposed under entitledArtifacts.link with artifactType = virtual_machine_reserved_instance.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("VirtualMachineReservedInstance").Get();

((VirtualMachineReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.VirtualMachineReservedInstance)).Link.InvokeAsync<VirtualMachineReservedInstanceArtifactDetails>(partnerOperations)
```

### <a name="request-example"></a><span data-ttu-id="ec06d-167">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ec06d-167">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/virtualmachinereservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="ec06d-168">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ec06d-168">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "virtual_machine_reserved_instance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="retrieve-reservation-details-from-an-entitlement-by-using-sdk-v19"></a><span data-ttu-id="ec06d-169">Foglalás részleteinek lekérése jogosultságból az SDK 1.9-es verziójával</span><span class="sxs-lookup"><span data-stu-id="ec06d-169">Retrieve reservation details from an entitlement by using SDK V1.9</span></span>

### <a name="c-example"></a><span data-ttu-id="ec06d-170">C \# példa</span><span class="sxs-lookup"><span data-stu-id="ec06d-170">C\# example</span></span>

<span data-ttu-id="ec06d-171">A foglalásokkal kapcsolatos további részletek fenntartott példány jogosultságból való lekérésére hívja meg az alatt elérhetővé téve az URI-t a ```entitledArtifacts.link``` ```artifactType = reservedinstance``` következővel: .</span><span class="sxs-lookup"><span data-stu-id="ec06d-171">To retrieve more details related to the reservations from a reserved instance entitlement, invoke the URI exposed under ```entitledArtifacts.link``` with ```artifactType = reservedinstance```.</span></span>

``` csharp
ResourceCollection<Entitlement> entitlements = partnerOperations.Customers.ById(selectedCustomerId).Entitlements.ByEntitlementType("ReservedInstance").Get();

((ReservedInstanceArtifact)entitlements.First().EntitledArtifacts.First(x => x.Type == ArtifactType.ReservedInstance)).Link.InvokeAsync<ReservedInstanceArtifactDetails>(partnerOperations);
```

### <a name="request-example"></a><span data-ttu-id="ec06d-172">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="ec06d-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/artifacts/reservedinstance/groups/2caf524395724e638ef64e109f1f79ca/lineitems/03500b1b-f2d6-4e23-ab4b-9fd67b917012/resource/ebf2e74b-630e-4a09-857d-a1f6c6351336 HTTP/1.1
Authorization: Bearer <Token>
Accept: application/json
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="ec06d-173">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="ec06d-173">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 368
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 799eee8d-07d1-452a-a035-388259df137c
MS-RequestId: cdc428d2-035b-41c4-9a32-e643c4471cbd
X-Locale: en-US
MS-CV: yrdTGsZ7IU2v9okv.0
MS-ServerId: 000002
Date: Mon, 19 Mar 2018 07:45:14 GMT

{
  "type": "reservedinstance",
  "virtualMachineReservations": [
    {
      "reservationId": "99f320db-c029-4c1b-a157-dad76e4481b6",
      "scopeType": "Shared",
      "quantity": 1,
      "expiryDateTime": "2019-02-23T00:00:00",
      "effectiveDateTime": "2018-02-23T18:15:24.6724884Z",
      "provisioningState": "Created"
    }
  ]
}
```

### <a name="api-consumers"></a><span data-ttu-id="ec06d-174">API-felhasználók</span><span class="sxs-lookup"><span data-stu-id="ec06d-174">API Consumers</span></span>

<span data-ttu-id="ec06d-175">Azok a partnerek, akik az API-val kérik le a virtuális gép fenntartott példányai jogosultságát – Frissítse a kérés URI-ját **a /customers/{customerId}/jogosultságok esetében a /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** címről a visszamenőleges kompatibilitás fenntartása érdekében.</span><span class="sxs-lookup"><span data-stu-id="ec06d-175">Partners who are using the API to query virtual machine reserved instance entitlements - Update the request URI from **/customers/{customerId}/entitlements to /customers/{customerId}/entitlements?entitlementType=virtualmachinereservedinstance** to maintain backward compatibility.</span></span> <span data-ttu-id="ec06d-176">A virtuális gép vagy az Azure SQL szerződéssel való használathoz frissítse a kérés URI-ját **a következőre: /customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span><span class="sxs-lookup"><span data-stu-id="ec06d-176">To consume virtual machine or Azure SQL with enhanced contract, update the request URI to **/customers/{customerId}/entitlements?entitlementType=reservedinstance**.</span></span>
