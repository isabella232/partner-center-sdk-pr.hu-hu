---
title: Ügyfél képzettségének frissítése
description: Megtudhatja, hogyan frissítheti az ügyfél képzettségét aszinkron szűréssel vagy átvilágítással, beleértve a profilhoz társított címeket is.
ms.date: 12/07/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: e0390e8a9c2a277dcb9e18b026f12625400ae176
ms.sourcegitcommit: 0c98496e972aebe10eba23822aa229125bfc035d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/07/2020
ms.locfileid: "97768648"
---
# <a name="update-a-customers-qualifications-asynchronously"></a>Ügyfél-képesítések aszinkron frissítése

**A következőkre vonatkozik**

- Partnerközpont

Ismerje meg, hogyan frissítheti az ügyfeleket a partner Center API-kon keresztül aszinkron módon. Ha szeretné megtudni, hogyan teheti meg ezt a szinkron módon, tekintse meg az [ügyfél minősítésének frissítése szinkron ellenőrzésen keresztül](update-customer-qualification-synchronous.md)című témakört.

Egy partner aszinkron módon frissítheti az ügyfél képzettségét "Education" vagy "GovernmentCommunityCloud". Más értékek, "None" és "nonprofit" nem állíthatók be.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{customer_id}/Qualifications? kód = {VALIDATIONCODE} http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

A minősítés frissítéséhez használja a következő lekérdezési paramétert.

| Név                   | Típus | Kötelező | Leírás                                                                                                                                            |
|------------------------|------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | GUID | Igen      | Az érték egy GUID formátumú **ügyfél-bérlői azonosító** , amely lehetővé teszi, hogy a viszonteladó a viszonteladóhoz tartozó adott ügyfél eredményeit szűrheti. |
| **validationCode**     | int  | Nem       | Csak a kormányzati közösségi felhőhöz szükséges.                                                                                                            |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

A [**CustomerQualification**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerqualification) enumerálás egész értékének értéke.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications?code=<validation-code> HTTP/1.1
Accept: application/json
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68

```

## <a name="rest-response"></a>REST-válasz

Ha ez sikeres, ez a metódus egy minősítési objektumot ad vissza a válasz törzsében. Alább látható egy példa arra, hogy a **post** hívása egy ügyfélen (a **none** korábbi minősítésével) az **oktatási** minősítéssel.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: [hibakódok](error-codes.md).

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 201 CREATED
Content-Length: 29
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualification": "Education",
    "vettingStatus": "InReview",
    "vettingCreateDate": "2020-12-04T20:54:24Z" // UTC
}
```

## <a name="related-articles"></a>Kapcsolódó cikkek

- [Ügyfél képzettségének beszerzése](get-a-customer-s-qualifications.md)
- [Egy partner ellenőrzési kódjainak lekérése](get-a-partner-s-validation-codes.md)