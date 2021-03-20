---
title: Partnerközpont – REST API-változásnapló
description: Ez az oldal a partner Center REST API-k változásait sorolja fel
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: b2c2cac36a8bd1bec7aa5bf6e5d1aa73b4779535
ms.sourcegitcommit: 717e483a6eec23607b4e31ddfaa3e2691f3043e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/20/2021
ms.locfileid: "104711848"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>December 2020 a partner Center REST API-k változásai

Tekintse át a partner Center REST API-k módosításait.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Fejlesztés az oktatási árképzés támogathatósági API-jai számára



### <a name="what-has-changed"></a>Mi változott?

A partner Center API jelenleg az oktatási ügyfelek jogosultságának ellenőrzéséhez és a képesítések beszerzéséhez szükséges. A GET minősítési API-t nem változtatja meg. Azonban a PUT minősítési API-hoz hozzáadott egy visszatérési esetet.

- A GET-nem változik. [Aktuális API-cikk](./get-customer-qualification-synchronous.md)
- A rendszer felveszi a visszaküldési esetet. [Aktuális API-cikk](./update-customer-qualification-synchronous.md)

Ezek az API-k február 2021 végén megszűnnek, és az alább leírtak szerint új API-kat kell cserélni.

### <a name="scenarios-impacted"></a>Érintett forgatókönyvek:

Ügyfél-jogosultság az oktatási díjszabáshoz a Select SKUs esetében

### <a name="detail-descriptions"></a>Részletes leírások

A rendszer két új GET és POST minősítési API-t fog bevezetni. Az új API-k **képesítéseket** és nem **minősítést** használnak. Az API-k a FY21 Q2-ben való teszteléshez lesznek elérhetők.

#### <a name="get-qualifications"></a>Végzettség beszerzése

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a>Példa a válaszra:

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a>Válasz mezői: 

- VettingStatus-értékek: jóváhagyva, megtagadva, inreview stb.

- VettingReason értékek:
   - Nem oktatási ügyfél
   - Már nem oktatási ügyfél
   - Nem oktatási ügyfél – felülvizsgálat után
   - Korlátozott oktatási ügyfél
   - Nem akadémiai tartomány
   - Nem jogosult könyvtár
   - Nem jogosult Múzeum
 
#### <a name="post-qualifications"></a>POST minősítések

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a>Példa a válaszra:

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a>Következő lépések

[Partnerközpont – REST API-referencia](partner-center-rest-api-reference.md)