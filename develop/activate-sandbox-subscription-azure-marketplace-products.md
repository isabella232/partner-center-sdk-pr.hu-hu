---
title: Homokozó elvű előfizetés aktiválása kereskedelmi piactér-termékekhez
description: Ismerje meg, hogyan használható a C/# és a partner Center REST API-k a kereskedelmi Piactéri termékekhez készült homokozó-előfizetés aktiválásához.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768508"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Homokozó-előfizetés aktiválása kereskedelmi Piactéri SaaS-termékekhez a számlázás engedélyezéséhez

**A következőkre vonatkozik:**

- Partnerközpont

Az előfizetések aktiválása a kereskedelmi piactéren szolgáltatott szoftverként (SaaS) származó termékekhez az integrációs sandbox-fiókoktól a számlázás engedélyezéséhez.

> [!NOTE]
> Csak a kereskedelmi piactéren elérhető SaaS-termékek előfizetését lehet aktiválni az integrációs homokozó fiókjaiból. Ha éles előfizetéssel rendelkezik, a telepítési folyamat befejezéséhez fel kell keresnie a közzétevő helyét. Az előfizetés számlázása csak a telepítés befejeződése után kezdődik.

## <a name="prerequisites"></a>Előfeltételek

- A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok. Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.

- Egy, a kereskedelmi piactér SaaS-termékekhez aktív előfizetéssel rendelkező ügyfél-integrációs munkapéldány-partneri fiók.

- A partner Center .NET SDK-t használó partnereink számára a funkció eléréséhez az SDK 1.14.0 vagy újabb verzióját kell használnia.

## <a name="c"></a>C\#

Az alábbi lépéseket követve aktiválhatja az előfizetést a kereskedelmi Marketplace SaaS-termékekhez:

1. Hozzon végre egy felületet az elérhető előfizetési műveletekhez. Azonosítania kell az ügyfelet, és meg kell adnia a próbaverziós előfizetés előfizetés-azonosítóját.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Aktiválja az előfizetést az **aktiválási** művelettel.

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST-kérelem

### <a name="request-syntax"></a>Kérelem szintaxisa

| Metódus     | Kérés URI-ja                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **UTÁNI** | [*{baseURL}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-ID}/Activate http/1.1 |

### <a name="uri-parameter"></a>URI-paraméter

| Név                   | Típus     | Kötelező | Leírás                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ügyfél – bérlő – azonosító** | **guid** | Y | Az érték egy GUID formátumú ügyfél-bérlői azonosító (**ügyfél-bérlő-azonosító**), amely lehetővé teszi az ügyfél megadását. |
| **előfizetés-azonosító** | **guid** | Y | Az érték egy GUID-formátumú előfizetés-azonosító (**előfizetés-azonosító**), amely lehetővé teszi az előfizetés megadását. |

### <a name="request-headers"></a>Kérésfejlécek

További információ: a [partneri központ Rest-fejlécei](headers.md).

### <a name="request-body"></a>A kérés törzse

Nincsenek.

### <a name="request-example"></a>Példa kérésre

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>REST-válasz

Ez a metódus az **előfizetés-azonosító** és az **állapot** tulajdonságokat adja vissza.

### <a name="response-success-and-error-codes"></a>Válasz sikeres és hibakódok

Minden válaszhoz tartozik egy HTTP-állapotkód, amely a sikeres vagy sikertelen és a további hibakeresési adatokat jelzi. A kód, a hiba típusa és a további paraméterek olvasásához használjon hálózati nyomkövetési eszközt. A teljes listát a következő témakörben tekintheti meg: [partner Center Rest](error-codes.md)-hibakódok.

### <a name="response-example"></a>Példa válaszra

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
