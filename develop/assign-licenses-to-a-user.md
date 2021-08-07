---
title: Licencek hozzárendelése egy felhasználóhoz
description: Megtudhatja, hogyan rendelhet licenceket egy ügyfélfelhasználóhoz Partnerközpont API-kon keresztül, például c vagy \# REST API-k használatával.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8263f7f274e453603305324cc7ac6e8b25820561ade3136b873c65ffa21e94fc
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989066"
---
# <a name="assign-licenses-to-a-user-via-partner-center-apis"></a>Licencek hozzárendelése egy felhasználóhoz Partnerközpont API-kon keresztül

Licencek hozzárendelése egy ügyfélfelhasználóhoz.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- Egy ügyfélazonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél azonosítóját, az irányítópulton Partnerközpont [meg.](https://partner.microsoft.com/dashboard) Válassza **a CSP** lehetőséget a Partnerközpont menüből, majd a Customers (Ügyfelek) **lehetőséget.** Válassza ki az ügyfelet az ügyféllistából, majd válassza a **Fiók lehetőséget.** Az ügyfél Fiók lapján keresse meg a **Microsoft-azonosítót** az **Ügyfélfiók adatai szakaszban.** A Microsoft-azonosító megegyezik az ügyfélazonosítóval ( `customer-tenant-id` ).

- Ügyfélfelhasználó-azonosító. Ez az azonosító azonosítja a felhasználót, akihez a licencet hozzá kell rendelni.

- A termék termékváltozat-azonosítója, amely azonosítja a terméket a licenchez.

## <a name="assigning-licenses-through-code"></a>Licencek hozzárendelése kóddal

Amikor licenceket rendel egy felhasználóhoz, ki kell választania az ügyfél előfizetéses termékkód-gyűjteményéből. Ezt követően, miután azonosította a hozzárendelni kívánt termékeket, be kell szereznie az egyes termékek termékváltozat-azonosítóját a hozzárendelések kiosztásához. Minden [**SubscribedSku példány**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku) tartalmaz egy [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.subscribedsku.productsku) tulajdonságot, amelyből hivatkozhat a [**ProductSku**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku) objektumra, és le tudja szerezni az [**azonosítót.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.productsku.id)

A licenc-hozzárendelési kérelemnek egyetlen licenccsoport licencét kell tartalmaznia. Például nem rendelhet licenceket a [**Group1**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licensegroupid) és **a Group2** csoporthoz ugyanabban a kérésben. Ha egy kérésben egynél több csoport licencét kísérelik meg hozzárendelni, az egy megfelelő hibával meghiúsul. A licenccsoport szerint elérhető licencekről az Elérhető licencek listájának lekért listája [licenccsoport szerint.](get-a-list-of-available-licenses-by-license-group.md)

A licencek kódon keresztüli hozzárendelésének lépései a következőek:

1. Egy [**LicenseAssignment objektum példányosítása.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) Ezzel az objektummal adhatja meg a hozzárendelni kívánt termékváltozatot és szolgáltatásterveket.

    ``` csharp
    LicenseAssignment license = new LicenseAssignment();
    ```

2. Töltse ki az objektum tulajdonságait az alább látható módon. Ez a kód feltételezi, hogy már rendelkezik a termék termékváltozat-azonosítójával, és hogy az összes elérhető szolgáltatás csomag hozzá lesz rendelve (ez azt jelenti, hogy egyik sem lesz kizárva).

    ```csharp
    license.SkuId = selectedProductSkuId;
    license.ExcludedPlans = null;
    ```

3. Ha nem tudja a termék termékváltozat-azonosítóját, le kellkérni az előfizetett termékváltozatok gyűjteményét, és le kell szereznie a termék termékváltozat-azonosítóját az egyikből. Példa a termékváltozat nevének nevére.

    ```csharp
    var customerSubscribedSkus = partnerOperations.Customers.ById(selectedCustomerId).SubscribedSkus.Get();
    var sku = customerSubscribedSkus.Items.Where(n => n.ProductSku.Name == "Office 365 Enterprise E3").First();
    license.SkuId = sku.ProductSku.Id;
    license.ExcludedPlans = null;
    ```

4. Ezután példányositsa a [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment)típusú új listát, és adja hozzá a licencobjektumot. Több licencet is hozzárendelhet, ha egyenként hozzáadja azokat a listához. A listában szereplő licenceknek ugyanattól a licenccsoporttól kell tartozni.

    ```csharp
    List<LicenseAssignment> licenseList = new List<LicenseAssignment>();
    licenseList.Add(license);
    ```

5. Hozzon [**létre egy LicenseUpdate példányt,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign tulajdonsághoz.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)

    ```csharp
    LicenseUpdate updateLicense = new LicenseUpdate();
    updateLicense.LicensesToAssign = licenseList;
    ```

6. Hívja meg [**a Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licencfrissítési objektumot az alább látható módon a licencek hozzárendeléséhez.

    ```csharp
    var assignLicense = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).LicenseUpdates.Create(updateLicense);
    ```

## <a name="c"></a>C\#

Ha egy licencet szeretne hozzárendelni egy ügyfélfelhasználóhoz, először példányosítenie kell egy [**LicenseAssignment**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment) objektumot, és fel kell töltve az [**Skuid**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.skuid) és [**az ExcludedPlans**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseassignment.excludedplans) tulajdonságot. Ezzel az objektummal adhatja meg a hozzárendelni kívánt termékváltozatot és a kizárni kívánt szolgáltatásterveket. Ezután példányositsa a **LicenseAssignment** típusú új listát, és adja hozzá a licencobjektumot a listához. Ezután hozzon létre [**egy LicenseUpdate példányt,**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate) és rendelje hozzá a licenc-hozzárendelések listáját a [**LicensesToAssign tulajdonsághoz.**](/dotnet/api/microsoft.store.partnercenter.models.licenses.licenseupdate.licensestoassign)

Ezután használja az [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) metódust az ügyfél azonosítójával az ügyfél azonosításához, a [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metódust pedig a felhasználói azonosítóval a felhasználó azonosításához. Ezután szerezze be az ügyfélfelhasználói licencfrissítési műveletek felületét a [**LicenseUpdates tulajdonságból.**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenseupdates)

Végül hívja meg a [**Create**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.create) vagy [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicenseupdates.createasync) metódust, és adja át a licencfrissítési objektumot a licenc hozzárendeléséhez.

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

**Minta:** [Konzoltesztalkalmazás.](console-test-app.md) **Project**: Partnerközpont SDK **Osztály:** CustomerUserAssignLicenses.cs

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérésszintaxis

| Metódus   | Kérés URI-ja                                                                                                    |
|----------|----------------------------------------------------------------------------------------------------------------|
| **Post** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{ügyfélazonosító}/users/{felhasználói azonosító}/licenseupdates HTTP/1.1 |

#### <a name="uri-parameters"></a>URI-paraméterek

Az ügyfél és a felhasználó azonosításához használja az alábbi elérésiút-paramétereket.

| Név        | Típus   | Kötelező | Leírás                                       |
|-------------|--------|----------|---------------------------------------------------|
| ügyfél-azonosító | sztring | Yes      | Egy GUID formátumú azonosító, amely azonosítja az ügyfelet. |
| felhasználói azonosító     | sztring | Yes      | A felhasználót azonosító GUID formátumú azonosító.     |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

Foglaljon bele [egy LicenseUpdate erőforrást](license-resources.md#licenseupdate) a kérelem törzsébe, amely megadja a hozzárendelni szükséges licenceket.

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

Sikeres művelet esetén a rendszer visszaad egy 201-es HTTP-válaszállapotkódot, és a válasz törzse tartalmaz egy [LicenseUpdate](license-resources.md#licenseupdate) erőforrást a licencinformációk alapján.

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hibakódok.](error-codes.md)

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

### <a name="response-example-license-isnt-available"></a>Példaválasz (a licenc nem érhető el)

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
