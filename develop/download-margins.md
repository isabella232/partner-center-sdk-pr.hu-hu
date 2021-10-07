---
title: Lekérte egy adott partner margóinak vesszővel tagolt listáját.
description: Lekérte egy adott partner margóinak vesszővel tagolt listáját.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6328ab962b2f210cee76b585ce2cf883c41eac3f
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646395"
---
# <a name="download-margins"></a>Margók letöltése


**A következőkre vonatkozik:** Partnerközpont 

**Megfelelő szerepkörök:** Globális rendszergazdai | Rendszergazdai ügynök

A partnerek lekértheti egy adott partner aktív margóinak listáját. Ez a metódus a partner és az elérhető kezdő és záró dátumok alapján adja vissza a margókat. A letöltési margók vesszővel tagolt formátumban adja vissza az adatokat.

## <a name="prerequisites"></a>Előfeltételek

- Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md) Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.


## <a name="rest-request"></a>REST-kérés
[GET] /v1/margók

### <a name="request-syntax"></a>Kérés szintaxisa

| Metódus   | Kérés URI-ja                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **KAP**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/margók/HTTP/1.1 letöltése |

### <a name="request-headers"></a>Kérésfejlécek

További információ: [REST Partnerközpont fejlécek.](headers.md)

### <a name="request-body"></a>A kérés törzse

None

### <a name="request-example"></a>Példa kérésre

```http
GET https://api.partnercenter.microsoft.com/v1/margins/download HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST-válasz

Sikeres művelet esetén ez a metódus fájlstreamként adja vissza az árlistát a.csv fájlként

### <a name="response-success-and-error-codes"></a>Sikeres válasz és hibakódok

Minden válasz tartalmaz egy HTTP-állapotkódot, amely sikeres vagy sikertelen állapotot jelez, és további hibakeresési információkat tartalmaz. Ezt a kódot, hibatípust és további paramétereket egy hálózati nyomkövetési eszközzel olvashatja be. A teljes listát lásd: [Hibakódok.](error-codes.md)

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

"id","productId","publisherName","productTitle","productType"","marginPercentage","startDate","endDate","status","statusDate"
"97620c21cc32_97cdce68-cce4-42aa-9410-233fd0269502","DZH318Z08L40","Market Place Test","Software As A Service Support Preview App","SaaS","10.0","2021-08-04T23:16:22.4736653Z","2022-03-31T23:59:59Z","live","2021-08-04T23:16:22.4736653Z"

```
