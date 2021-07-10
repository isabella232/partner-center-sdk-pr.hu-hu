---
title: Partnerközpont – REST API-változásnapló
description: Ez az oldal a REST API-k Partnerközpont sorolja fel
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: d4f7f034a36a26b6219086ca952b189f7a313ef7
ms.sourcegitcommit: 51237e7e98d71a7e0590b4d6a4034b6409542126
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/09/2021
ms.locfileid: "113571995"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>A REST API-k Partnerközpont 2020. decemberi változásai

Itt ellenőrizheti a REST API Partnerközpont módosításait.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Az oktatási díjszabás jogosultsági API- k fejlesztései



### <a name="what-has-changed"></a>Mi változott?

A Partnerközpont API jelenleg GET és PUT minősítésekkel rendelkezik az Education-ügyfelek jogosultságának ellenőrzésére. A GET Qualification API nem módosul. Hozzáadtunk azonban egy visszatérési esetet a PUT-minősítési API-hoz.

- GET – nem változik.
- PUT – a visszatérési eset hozzá lesz adva.

Ezeket az API-kat 2021 februárjától kivezetjük, és az alábbiakban leírtak szerint új API-k váltják fel őket.

### <a name="scenarios-impacted"></a>Érintett forgatókönyvek:

Az ügyfelek oktatási jogosultsága a kiválasztott termékcsomagok díjszabására

### <a name="detail-descriptions"></a>Részletek leírása

Két új GET és POST minősítési API lesz bevezetve. Az új API-k a **Minősítéseket fogják használni,** nem **a Minősítést.** Az API-k a 2. negyedévi FY21 teszteléshez lesznek elérhetők.

#### <a name="get-qualifications"></a>GET-minősítések

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

#### <a name="response-fields"></a>Válaszmezők: 

- VettingStatus-értékek: Approved (Jóváhagyva), Denied (Elutasítva), InReview (Áttekintés) stb.

- A VettingReason értékei:
   - Nem oktatási ügyfél
   - Már nem oktatási ügyfél
   - Nem oktatási ügyfél – felülvizsgálat után
   - Oktatási ügyfélként korlátozott
   - Nem tudományos tartomány
   - Nem jogosult kódtár
   - Nem jogosult a Program
 
#### <a name="post-qualifications"></a>POST-minősítések

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
