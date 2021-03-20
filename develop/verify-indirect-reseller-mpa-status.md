---
title: Közvetett viszonteladó Microsoft partneri szerződésének aláírása állapotának ellenőrzése
description: A AgreementStatus API segítségével ellenőrizheti, hogy a közvetett viszonteladó aláírta-e a Microsoft partneri szerződést.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fa9480424eccc933bc9c28c3879a195fbd5f2bb1
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711895"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Közvetett viszonteladó Microsoft partneri szerződésének aláírása állapotának ellenőrzése

**A következőkre vonatkozik:**

- Partnerközpont
- A Microsoft Cloud for US Government Partnerközpontja

Ellenőrizheti, hogy a közvetett viszonteladó aláírta-e a Microsoft partneri szerződést a Microsoft Partner Network (MPN) azonosító (PGA/PLA) vagy a Cloud Solution Provider (CSP) bérlői azonosító (Microsoft ID) használatával. Ezen azonosítók egyikével ellenőrizhető a Microsoft partneri szerződés aláírása állapota a **AgreementStatus** API használatával.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv csak az App + felhasználói hitelesítő adatokkal történő hitelesítést támogatja.

- Az MPN-azonosító (PGA/PLA) vagy a közvetett viszonteladóhoz tartozó CSP-bérlő azonosítója (Microsoft-azonosító). *A két azonosító közül egyet kell használnia.*

## <a name="c"></a>C\#

Közvetett viszonteladói Microsoft partneri szerződés aláírási állapotának beszerzése:

1. A **IAggregatePartner. Compliance** gyűjtemény használatával hívja meg a **AgreementSignatureStatus** tulajdonságot.

2. Hívja meg a [**Get ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) vagy a [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync) metódust.

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Minta: **[konzol tesztelési alkalmazás](console-test-app.md)**
- Projekt: **PartnerCenterSDK. FeaturesSamples**
- Osztály: **GetAgreementSignatureStatus. cs**

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus | Kérés URI-ja |
| ------ | ----------- |
| **GET** | *[{baseURL}](partner-center-rest-urls.md)*/v1/Compliance/{ProgramName}/agreementstatus? mpnId = {mpnId} &tenantId = {tenantId} |

#### <a name="uri-parameters"></a>URI-paraméterek

A partner azonosításához a következő két lekérdezési paraméter egyikét kell megadnia. Ha nem adja meg a két lekérdezési paraméter egyikét sem, a rendszer **400 (hibás kérés)** hibaüzenetet kap.

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | No | A közvetett viszonteladót azonosító Microsoft Partner Network azonosító (PGA/PLA). |
| **TenantId** | GUID | No | Egy Microsoft-azonosító, amely azonosítja a közvetett viszonteladó CSP-fiókját. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partner Center Rest](headers.md).

### <a name="request-examples"></a>Példák kérése

#### <a name="request-using-mpn-id-pgapla"></a>Kérelem az MPN-AZONOSÍTÓval (PGA/PLA)

A következő példa a közvetett viszonteladói Microsoft partneri szerződés aláírási állapotát a közvetett viszonteladó Microsoft Partner Network AZONOSÍTÓjának használatával kéri le.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>A CSP-bérlő AZONOSÍTÓját használó kérelem

A következő példa lekéri a közvetett viszonteladó Microsoft partneri szerződésének aláírása állapotát a közvetett viszonteladó CSP-bérlői AZONOSÍTÓjának (Microsoft ID) használatával.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?tenantId=a2898e3a-06ca-454e-a0d0-c73b0ee36bba HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST-válasz

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát lásd: a [partneri központ Rest-hibája](error-codes.md).

### <a name="response-example-success"></a>Válasz példa (sikeres)

A következő példában szereplő válasz sikeresen visszaadja, hogy a közvetett viszonteladó aláírta-e a Microsoft partneri szerződést.

```http
HTTP/1.1 200 OK
Content-Length: 29
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: jn3r+1wpE06nCt/0.0
MS-ServerId: 0000005B
Date: Tue, 15 Oct 2019 12:44:34 GMT
Connection: close
{
    "isAgreementSigned": true
}
```

### <a name="response-examples-failure"></a>Válasz példák (hiba)

Az alábbi példákhoz hasonló válaszokat kaphat, ha nem lehet visszaadni a közvetett viszonteladó Microsoft partneri szerződésének aláírási állapotát.

#### <a name="non-guid-formatted-csp-tenant-id"></a>Nem GUID formátumú CSP-bérlő azonosítója

Az alábbi példában szereplő válasz akkor ad vissza, ha az API-nak átadott CSP-bérlő azonosítója nem GUID.

```http
HTTP/1.1 400 Bad Request
Content-Length: 105
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: rbuZl5lbAkyq8WGK.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 08:55:23 GMT
Connection: close
{
    "code": 2000,
    "description": "Tenant Id must be a GUID.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="non-numeric-mpn-id"></a>Nem numerikus MPN-azonosító

Az alábbi példában szereplő válasz akkor ad vissza, ha az API-nak átadott MPN-azonosító (PGA/PLA) nem numerikus.

```http
HTTP/1.1 400 Bad Request
Content-Length: 103
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: cP5JiS4sv0GJxlJ9.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 08:58:45 GMT
Connection: close
{
    "code": 2000,
    "description": "MPN Id must be numeric.",
    "data": [],
    "source": "PartnerApiServiceControllers"
}
```

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Nincs MPN-azonosító vagy CSP-bérlő azonosítója

Ha nem adott meg MPN-azonosítót (PGA/PLA) vagy CSP-bérlői azonosítót az API-nak, akkor a következő példa válaszát adja vissza. A két azonosító típus egyikét át kell adnia az API-nak.

```http
HTTP/1.1 400 Bad Request
Content-Length: 114
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: hEV736v4qk6joDMR.0
MS-ServerId: 00000055
Date: Wed, 16 Oct 2019 09:00:30 GMT
Connection: close
{
    "code": 2001,
    "description": "Both MPN Id and Tenant Id cannot be empty.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Az MPN-azonosító és a CSP-bérlő azonosítója is át lett adva

Ha az MPN-azonosítót (PGA/PLA) és a CSP-bérlői azonosítót is átadja az API-nak, a következő példa érkezik. A két azonosító típusnak *csak az egyikét* kell átadnia az API-nak.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2000,
    "description": "Both MPN Id and Tenant Id should not be passed.",
    "data": [],
    "source": "ComplianceController"
}
```

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>A CSP közvetett viszonteladói MPN-azonosítója (PGA/PLA) vagy érvénytelen, vagy nem települ át a partneri tagsági központból a partner központba

A következő példa akkor ad vissza választ, ha az átadott közvetett viszonteladói MPN-azonosító (PGA/PLA) érvénytelen, vagy a partneri tagsági központból nem a partner központba lett áttelepítve. [További információ](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2200,
    "description": "MPN Id 123456 is either invalid or not yet migrated to Partner Center. Please advise your reseller to migrate the reseller MPN ID to Partner Center to continue with this order.",
    "data": [
        "https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx"
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>A CSP közvetett szolgáltató régiója és a CSP közvetett viszonteladói régiója nem egyezik

A következő példa akkor ad vissza választ, ha a közvetett viszonteladói MPN-azonosító (PGA/PLA) régiója nem egyezik a közvetett szolgáltató régiójával. [További](/partner-center/mpa-indirect-provider-faq) információ a CSP-régiókról.

```http
HTTP/1.1 400 Bad Request
Content-Length: 119
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: WTsLWK5UlUW9sZjH.0
MS-ServerId: 0000005B
Date: Wed, 16 Oct 2019 09:02:30 GMT
Connection: close
{
    "code": 2201,
    "description": "The CSP region of the MPN ID 1234567 doesn’t match the CSP region from where you are placing the order. Provide the MPN ID for the CSP region where you are placing the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq" 
    ],
    "source": "PartnerFD"
}
```

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>A CSP közvetett viszonteladói fiókja létezik a partner Centerben, de nem írta alá az MPA-t

A következő példa válaszát adja vissza, ha a fiókpartner közvetett viszonteladói fiókja nem írta alá a MPA-t. [További információ](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2203,
    "description": "MPN Id 123456 has not signed Microsoft Partner Agreement (MPA) for the CSP region where the order is being placed. Please advise your reseller to sign MPA to continue with the order.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Nincs társítva CSP közvetett viszonteladói fiók a megadott MPN-AZONOSÍTÓhoz

A következő példa akkor ad vissza választ, ha a fiókpartner felismeri a kérelemben átadott MPN-azonosítót (PGA/PLA), de a megadott MPN-AZONOSÍTÓhoz (PGA/PLA) nincs társítva CSP-regisztráció. [További információ](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2204,
    "description": "MPN Id 123456 is not associated with a CSP Indirect Reseller account in Partner Center. Please advise your reseller to enroll into the CSP program as an indirect reseller in Partner Center.",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```

#### <a name="invalid-tenant-id"></a>Érvénytelen a bérlő azonosítója

Ha a fiókpartner nem talál olyan fiókot, amely a kérelemben átadott bérlői AZONOSÍTÓhoz tartozik, akkor a következő példa érkezik.

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2205,
    "description": "Partner Center doesn't find any account associated to the Tenant ID 12345678-ACBD-1234-ABCD-123456789ABC",
    "data": [],
    "source": "PartnerFD"
}
```

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Nem található a megadott bérlői AZONOSÍTÓval rendelkező MPA

Ha a fiókpartner nem talál a megadott bérlői AZONOSÍTÓval rendelkező MPA-aláírást, akkor a következő példában szereplő válasz érkezik. [További információ](/partner-center/mpa-indirect-provider-faq)

```http
HTTP/1.1 400 Bad Request
Content-Length: 321
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9240230a-413f-4880-acbd-96d59a165474
MS-RequestId: 92caacb1-8c9e-49af-8f85-83f271c85056
MS-CV: V8eVMXvaBE6LHyq6.0
MS-ServerId: 0000005B
Date: Fri, 24 Jul 2020 11:56:46 GMT
Connection: close
{
    "code": 2206,
    "description": "Parnter Center Account associated to Tenant Id 12345678-ACBD-1234-ABCD-123456789ABC hasn't signed the agreement",
    "data": [
        "https://docs.microsoft.com/partner-center/mpa-indirect-provider-faq"
    ],
    "source": "PartnerFD"
}
```