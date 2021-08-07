---
title: Közvetett viszonteladó aláírási állapotának Microsoft Partnerszerződés ellenőrzése
description: Az AgreementStatus API használatával ellenőrizheti, hogy egy közvetett viszonteladó írta-e alá a Microsoft Partnerszerződés.
ms.date: 07/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 517c99356a4b623b5b46bc3d33f2355cd569f97326e7d9596cff551329d10da7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989848"
---
# <a name="verify-an-indirect-resellers-microsoft-partner-agreement-signing-status"></a>Közvetett viszonteladó aláírási állapotának Microsoft Partnerszerződés ellenőrzése

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont a Microsoft Cloud for US Government

Annak ellenőrzéséhez, hogy egy közvetett viszonteladó írta-e alá a Microsoft Partnerszerződés-t az Microsoft Partner Network(MPN) azonosítójával (PGA/PLA) vagy Felhőszolgáltató (CSP) bérlőazonosítójával (Microsoft ID). Ezen azonosítók egyikének használatával ellenőrizheti a Microsoft Partnerszerződés állapotát az **AgreementStatus** API-val.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv csak az App+User hitelesítő adatokkal történő hitelesítést támogatja.

- A közvetett viszonteladó MPN-azonosítója (PGA/PLA) vagy CSP-bérlőazonosítója (Microsoft ID). *A két azonosító egyikét kell használnia.*

## <a name="c"></a>C\#

Közvetett viszonteladó Microsoft Partnerszerződés aláírási állapotának legyűjtése:

1. Az **AgreementSignatureStatus** tulajdonságot az **IAggregatePartner.Compliance** gyűjtemény használatával hívható meg.

2. Hívja meg a [**Get() vagy**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.get) [**a GetAsync() metódust.**](/dotnet/api/microsoft.store.partnercenter.compliance.iagreementsignaturestatus.getasync)

``` csharp
// IAggregatePartner partnerOperations;

var agreementSignatureStatusByMpnId = partnerOperations.Compliance.AgreementSignatureStatus.Get(mpnId:"Enter MPN Id (PGA/PLA)");

var agreementSignatureStatusByTenantId = partnerOperations.Compliance.AgreementSignatureStatus.Get(tenantId: "Enter Tenant Id");
```

- Minta: **[Konzoltesztalkalmazás](console-test-app.md)**
- Project: **PartnerCenterSDK.FeaturesSamples**
- Osztály: **GetAgreementSignatureStatus.cs**

## <a name="rest-request"></a>REST-kérés

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus | Kérés URI-ja |
| ------ | ----------- |
| **Kap** | *[{baseURL}](partner-center-rest-urls.md)*/v1/compliance/{ProgramName}/agreementstatus?mpnId={MpnId}&tenantId={TenantId} |

#### <a name="uri-parameters"></a>URI-paraméterek

A partner azonosításához meg kell adnia az alábbi két lekérdezési paraméter egyikét. Ha nem adja meg a két lekérdezési paraméter valamelyikét, **400-as (Hibás kérés) hibaüzenetet kap.**

| Név | Típus | Kötelező | Leírás |
| ---- | ---- | -------- | ----------- |
| **MpnId** | int | No | Egy Microsoft Partner Network (PGA/PLA) azonosító, amely azonosítja a közvetett viszonteladót. |
| **TenantId (Bérlőazonosító)** | GUID | No | Egy Microsoft-azonosító, amely azonosítja a közvetett viszonteladó CSP-fiókját. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: REST [Partnerközpont.](headers.md)

### <a name="request-examples"></a>Példák kérésre

#### <a name="request-using-mpn-id-pgapla"></a>Kérés MPN-azonosítóval (PGA/PLA)

A következő példakérés a közvetett viszonteladó aláírási állapotát Microsoft Partnerszerződés le a közvetett viszonteladó Microsoft Partner Network azonosítójával.

```http
GET https://api.partnercenter.microsoft.com/v1/compliance/csp/agreementstatus?mpnid=1234567 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

#### <a name="request-using-csp-tenant-id"></a>Kérelem CSP-bérlőazonosító használatával

A következő példakérés lekérése a közvetett viszonteladó Microsoft Partnerszerződés aláírási állapotát a közvetett viszonteladó CSP-bérlőazonosítójának (Microsoft ID) használatával.

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

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely jelzi a sikeres vagy sikertelenséget, valamint további hibakeresési információkat. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: Partnerközpont [REST-hiba.](error-codes.md)

### <a name="response-example-success"></a>Válasz példa (sikeres)

Az alábbi példaválasz sikeresen visszaadja, hogy a közvetett viszonteladó írta-e alá a Microsoft Partnerszerződés.

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

### <a name="response-examples-failure"></a>Példák válaszra (hiba)

Előfordulhat, hogy az alábbi példákhoz hasonló válaszokat kap, ha a közvetett viszonteladói regisztráció aláírási állapota Microsoft Partnerszerződés nem lehet visszaadni.

#### <a name="non-guid-formatted-csp-tenant-id"></a>Nem GUID formátumú CSP-bérlőazonosító

A következő példaválasz akkor lesz visszaadva, ha az API-nak átadott CSP-bérlőazonosító nem GUID.

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

Az alábbi példaválasz akkor lesz visszaadva, ha az API-nak átadott MPN-azonosító (PGA/PLA) nem numerikus.

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

#### <a name="no-mpn-id-or-csp-tenant-id"></a>Nincs MPN-azonosító vagy CSP-bérlőazonosító

A következő példaválasz akkor lesz visszaadva, ha nem adott át MPN-azonosítót (PGA/PLA) vagy CSP-bérlőazonosítót az API-nak. A két azonosítótípus egyikét kell átadnia az API-nak.

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

#### <a name="both-mpn-id-and-csp-tenant-id-passed"></a>Az MPN-azonosító és a CSP-bérlőazonosító is átadott

Az alábbi példaválasz akkor lesz visszaadva, ha az MPN-azonosítót (PGA/PLA) és a CSP-bérlőazonosítót is átadhatja az API-nak. A két *azonosítótípus közül* csak egyet kell átadnia az API-nak.

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

#### <a name="csp-indirect-reseller-mpn-id-pgapla-is-either-invalid-or-not-migrated-from-partner-membership-center-to-partner-center"></a>CSP Indirect Reseller MPN-azonosító (PGA/PLA) érvénytelen, vagy nem migrálható Partner Membership Center-ről Partnerközpont

A következő példaválasz akkor ad vissza, ha a közvetett viszonteladó MPN-azonosítója (PGA/PLA) érvénytelen, vagy nem migrálva lett Partner Membership Center-ről Partnerközpont. [További információ](https://partner.microsoft.com/resources/detail/migrate-pmc-pc-mpa-guide-pptx)

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

#### <a name="csp-indirect-provider-region-and-csp-indirect-reseller-region-does-not-match"></a>CSP Indirect Provider régió és CSP Indirect Reseller régió nem egyezik

Az alábbi példaválasz akkor lesz visszaadva, ha a közvetett viszonteladó MPN-azonosítója (PGA/PLA) régiója nem egyezik meg a közvetett szolgáltató régiójával. [További információ a](/partner-center/mpa-indirect-provider-faq) CSP-régiókról.

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

#### <a name="csp-indirect-reseller-account-exists-in-partner-center-but-hasnt-signed-the-mpa"></a>CSP Indirect Reseller fiók létezik a Partnerközpont de még nem írta alá az MPA-t

Az alábbi példaválasz akkor lesz visszaadva, CSP Indirect Reseller a Partnerközpont nem írta alá az MPA-t. [További információ](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="no-csp-indirect-reseller-account-is-associated-with-the-given-mpn-id"></a>Nincs CSP Indirect Reseller fiók társítva az adott MPN-azonosítóval

Az alábbi példaválasz akkor Partnerközpont, ha a Partnerközpont felismeri a kérésben átadott MPN-azonosítót (PGA/PLA), de nincs CSP-regisztráció társítva az adott MPN-azonosítóhoz (PGA/PLA). [További információ](/partner-center/mpa-indirect-provider-faq)

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

#### <a name="invalid-tenant-id"></a>Érvénytelen bérlőazonosító

A következő példaválasz akkor lesz visszaadva Partnerközpont nem található a kérésben átadott bérlőazonosítóhoz társított fiók.

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

#### <a name="no-mpa-found-with-the-given-tenant-id"></a>Nem található MPA a megadott bérlőazonosítóval

Az alábbi példaválasz akkor lesz visszaadva, Partnerközpont nem található MPA-aláírás a megadott bérlőazonosítóval. [További információ](/partner-center/mpa-indirect-provider-faq)

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