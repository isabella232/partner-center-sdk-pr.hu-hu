---
title: Licencek hozzárendelése egy felhasználóhoz
description: Megtudhatja, hogyan rendelhet hozzá licenceket egy ügyfél-felhasználóhoz a partner Center API-kon keresztül, például C \# vagy REST API-k használatával.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6eb0b953b9157e48074415bb3207e2946cfb2ab4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/13/2020
ms.locfileid: "97768547"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Licencek kiosztása egy felhasználónak a partner Center API-kon keresztül

**A következőkre vonatkozik:**

- Partnerközpont

Licencek kiosztása az ügyfél felhasználói számára.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

- Felhasználói azonosító. Ez az azonosító azonosítja azt a felhasználót, akihez a licencet hozzá kell rendelni.

- A licenchez tartozó terméket azonosító termék SKU-azonosítója.

## <a name="assigning-licenses-through-code"></a>Licencek kiosztása kód használatával

Amikor licenceket rendel egy felhasználóhoz, ki kell választania az ügyfél előfizetett SKU-gyűjteményéből. Ezután, miután azonosította a hozzárendelni kívánt termékeket, minden termékhez be kell szereznie a termék SKU-AZONOSÍTÓját a hozzárendelések elvégzéséhez. Minden [**SubscribedSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) -példány tartalmaz egy [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) -tulajdonságot, amelyből hivatkozhat a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) objektumra, és lekérheti az [**azonosítót**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id).

A licenc-hozzárendelési kérelemnek egyetlen licencszerződésből származó licenceket kell tartalmaznia. Nem rendelhet hozzá például licenceket a [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) és a **Group2** alkalmazáshoz ugyanabban a kérésben. Egy adott kérelemben egynél több csoport licencének hozzárendelésére tett kísérlet a megfelelő hibával meghiúsul. Ha szeretné megtudni, hogy milyen licencek érhetők el a licencszerződésben, tekintse meg az [elérhető licencek listájának beszerzése a licencszerződés alapján](get-a-list-of-available-licenses-by-license-group.md)című témakört.

A licencek kód használatával történő hozzárendelésének lépései a következők:

1. [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) objektum példányának létrehozása. Ezzel az objektummal adhatja meg a Hozzárendelendő termékhez tartozó SKU-t és szolgáltatási terveket.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Töltse fel az objektum tulajdonságait az alább látható módon. Ez a kód feltételezi, hogy már rendelkezik a termék SKU-azonosítójával, és az összes elérhető szolgáltatáscsomag hozzá lesz rendelve (azaz a None nem lesz kizárva).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Ha nem rendelkezik a termék SKU-azonosítójával, le kell kérnie az előfizetett SKU-gyűjteményt, és be kell szereznie a termék SKU-AZONOSÍTÓját az egyik közül. Íme egy példa, ha ismeri a termék SKU-nevét.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Ezután hozza létre a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)típusú új listát, és adja hozzá a License objektumot. Több licencet is hozzárendelhet úgy, hogy mindegyiket egyenként hozzáadja a listához. A listában szereplő licenceknek ugyanabból a csoportból kell származnia.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Hozzon létre egy [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -példányt, és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) tulajdonsághoz.

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. A licencek hozzárendeléséhez hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licenc frissítése objektumot a lent látható módon.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Ahhoz, hogy licencet rendeljen egy ügyfél-felhasználóhoz, először hozza létre a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) objektumot, és töltse fel a [**SkuID**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) és a [**ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) tulajdonságait. Ezzel az objektummal adhatja meg a kizárni kívánt termék SKU-jának kiosztását és a szolgáltatási terveket. Ezután hozza létre a **LicenseAssignment** típusú új listát, és adja hozzá a licenc objektumot a listához. Ezután hozzon létre egy [**LicenseUpdate**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) -példányt, és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign) tulajdonsághoz.

Ezután használja a [**IAggregatePartner. Customs. ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél-azonosítóval az ügyfél azonosításához, valamint a Users [**. ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) METÓDUSt a felhasználói azonosítóval a felhasználó azonosításához. Ezután szerezzen be egy felületet az ügyfél felhasználói licencek frissítési műveleteihez a [**LicenseUpdates**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates) tulajdonságból.

Végül hívja meg a [**create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy a [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licenc frissítése objektumot a licenc hozzárendeléséhez.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerUserId;
// string selectedCustomerId;
// string selectedProductSkuId;

// Instantiate and populate a LicenseAssignment object.
LicenseAssignment license = new LicenseAssignment();
license.SkuId = selectedProductSkuId;
license.ExcludedPlans = null;

// Instantiate a list of licenses to assign and add the license to it.
List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
licenseList.Add(license);

// Instantiate a LicenseUpdate object and add the list of licenses to assign.
LicenseUpdate updateLicense = new LicenseUpdate();
updateLicense.LicensesToAssign = licenseList;

// Update the user licenses.
var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
```

**Példa**: [konzol tesztelési alkalmazás](console-test-app.md). **Projekt**: partner Center SDK Samples **osztály**: CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus   | Kérés URI-ja                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/licenseupdates http/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél és a felhasználó azonosításához használja a következő elérésiút-paramétereket.

| Név        | Típus   | Kötelező | Leírás                                       |
|-------------|--------|----------|---------------------------------------------------|
| ügyfél-azonosító | sztring | Igen      | Egy GUID formátumú azonosító, amely azonosítja az ügyfelet. |
| felhasználói azonosító     | sztring | Igen      | A felhasználó azonosítására szolgáló GUID formátumú azonosító.     |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Adjon meg egy [LicenseUpdate](license-resources.md#licenseupdate) -erőforrást a kérelem törzsében, amely meghatározza a hozzárendelni kívánt licenceket.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/554526aa-cf5e-46fa-95df-98dbc55d8a1e/licenseupdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 183
Expect: 100-continue

{
    "LicensesToAssign": [{
            "ExcludedPlans": null,
            "SkuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "LicensesToRemove": null,
    "LicenseWarnings": null,
    "Attributes": {
        "ObjectType": "LicenseUpdate"
    }
}
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, a rendszer a 201-as HTTP-válasz állapotkódot adja vissza, és a válasz törzse tartalmaz egy [LicenseUpdate](license-resources.md#licenseupdate) -erőforrást a licencelési adatokkal.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example-success"></a>Válasz példa (sikeres)

```http
HTTP/1.1 201 Created
Content-Length: 139
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: a37d3009-665d-4e12-b76e-1aa10cf80140
MS-CV: 5AnzcZQrvUqCq3kd.0
MS-ServerId: 030020525
Date: Thu, 20 Apr 2017 21:50:39 GMT

{
    "licensesToAssign": [{
            "skuId": "f8a1db68-be16-40ed-86d5-cb42ce701560"
        }
    ],
    "licenseWarnings": [],
    "attributes": {
        "objectType": "LicenseUpdate"
    }
}
```

### <a name="response-example-license-isnt-available"></a>Válasz példa (a licenc nem érhető el)

```http
HTTP/1.1 400 Bad Request
Content-Length: 341
Content-Type: application/json; charset=utf-8
MS-CorrelationId: c73c9570-c352-459e-98a3-dafe4bd8c821
MS-RequestId: f4f3b748-8b22-4d07-a5a1-dceb32824192
MS-CV: 5npA0K22CUmWPOzB.0
MS-ServerId: 102030524
Date: Thu, 20 Apr 2017 22:12:36 GMT

{
    "code": 60012,
    "description": "We&#39;re sorry, it looks like you've run out of licenses. Buy more licenses, and then try again.",
    "data": ["LicenseQuotaExceededException : Subscription with Account 0c39d6d5-c70d-4c55-bc02-f620844f3fd1 and SKU f8a1db68-be16-40ed-86d5-cb42ce701560 does not have any available licenses left."],
    "source": "PartnerFD"
}
```
