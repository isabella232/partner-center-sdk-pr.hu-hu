---
title: Ügyfél képzettségének beszerzése
description: Megtudhatja, hogyan használhatja az aszinkron érvényesítést az ügyfél a partner Center API-n keresztüli minősítésének beszerzéséhez. A partnerek ezt az oktatási ügyfelek ellenőrzésére használhatják.
ms.date: 01/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: JoeyBytes
ms.author: jobiesel
ms.openlocfilehash: 130ee276461e3390ac78ac7abd8baeefe6a70d7c
ms.sourcegitcommit: 97f93caa57df6c64fe19868e6b2a0f7937226b51
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/21/2021
ms.locfileid: "98636383"
---
# <a name="get-a-customers-qualification-asynchronously"></a>Ügyfél-képesítés aszinkron beszerzése

**A következőkre vonatkozik**

- Partnerközpont

Az ügyfél képzettségének aszinkron beszerzése.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Ügyfél-azonosító ( `customer-tenant-id` ). Ha nem ismeri az ügyfél AZONOSÍTÓját, megtekintheti a partner Center [irányítópultján](https://partner.microsoft.com/dashboard). Válassza a **CSP** lehetőséget a partner központ menüjében, majd az **ügyfelek**. Válassza ki az ügyfelet az ügyfél listából, majd válassza a **fiók** lehetőséget. Az ügyfél fiókja lapon keresse meg a **Microsoft ID** -t az **ügyfél fiók adatai** szakaszban. A Microsoft-azonosító megegyezik az ügyfél-AZONOSÍTÓval ( `customer-tenant-id` ).

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus  | Kérés URI-ja                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **GET** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Qualifications http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

Ez a táblázat felsorolja a szükséges lekérdezési paramétereket az összes minősítés beszerzéséhez.

| Név               | Típus   | Kötelező | Leírás                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | sztring | Igen      | Egy GUID-formázott karakterlánc, amely azonosítja az ügyfelet. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/qualifications HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
```

## <a name="rest-response"></a>REST-válasz

Ha a művelet sikeres, ez a módszer képesítések gyűjteményét adja vissza a válasz törzsében.  Az alábbi példák az **oktatási** végzettséggel rendelkező ügyfelekre vonatkozó **Get** hívásra vonatkoznak.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-examples"></a>Példák a válaszokra

#### <a name="approved"></a>Approved

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Approved",
        }
    ]
}

```

#### <a name="in-review"></a>In Review (Felülvizsgálat alatt)

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "InReview",
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

#### <a name="denied"></a>Megtagadva

```http
HTTP/1.1 200 OK
Content-Length:
Content-Type: application/json
MS-CorrelationId: 7d2456fd-2d79-46d0-9f8e-5d7ecd5f8745
MS-RequestId: 037db222-6d8e-4d7f-ba78-df3dca33fb68
{
    "qualifications": [
        {
            "qualification": "Education",
            "vettingStatus": "Denied",
            "vettingReason": "Not an Education Customer", // example Vetting Reason
            "vettingCreatedDate": "2020-12-03T10:37:38.885Z" // UTC
        }
    ]
}

```

## <a name="related-articles"></a>Kapcsolódó cikkek

- [Ügyfél képzettségének frissítése](update-a-customer-s-qualifications.md)