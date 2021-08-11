---
title: Partnerközpont – REST API-változásnapló
description: Ez az oldal a rest Partnerközpont módosításait sorolja fel
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: f74f59969bf8d73c6e6e8b39900a53c337a2af715c168b59009792beddf43159
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993282"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>A REST API-k Partnerközpont 2020. decemberi változásai

Itt ellenőrizheti a REST API Partnerközpont módosításait.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Az oktatási jogosultsági API-k fejlesztései



### <a name="what-has-changed"></a>Mi változott?

A Partnerközpont API jelenleg GET és PUT minősítésekkel rendelkezik az oktatási ügyfelek jogosultságának ellenőrzésére. A GET Qualification API nem változik. Hozzáadtunk azonban egy visszatérési esetet a PUT Minősítés API-hoz.

- GET – nem változik.
- PUT – a visszatérési eset hozzá lesz adva.

Ezek az API-k 2021. február végén ki lesznek vezetve, és az alábbiakban leírtak szerint új API-k váltják fel őket.

### <a name="scenarios-impacted"></a>Érintett forgatókönyvek:

Az ügyfelek oktatási jogosultsága a kiválasztott termékcsomagok díjszabására

### <a name="detail-descriptions"></a>Részletek leírása

Két új GET és POST Minősítési API lesz bevezetve. Az új API-k a **Minősítéseket fogják használni,** nem **a Minősítést.** Az API-k a 21. negyedévi FY21 teszteléshez lesznek elérhetők.

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

- ÁtvizsgálásÁllapot értékei: Jóváhagyva, Megtagadva, InReview stb.

- A VettingReason értékei:
   - Nem oktatási ügyfél
   - Már nem oktatási ügyfél
   - Nem oktatási ügyfél – felülvizsgálat után
   - Korlátozott oktatási ügyfélként
   - Nem tudományos tartomány
   - Nem jogosult kódtár
   - Nem jogosult Egy
 
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
