---
title: Konzolos tesztalkalmazás
description: Ez a konzol-tesztelési alkalmazás a partner Center API-k által támogatott összes forgatókönyvhöz tartalmaz mintakód-kódot. Teszteléshez is használhatja.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767995"
---
# <a name="console-test-app"></a>Konzolos tesztalkalmazás

**A következőkre vonatkozik:**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A konzol tesztelési alkalmazás a C# és a Java nyelven érhető el, és a partner Center API-k által támogatott összes forgatókönyvhöz tartalmaz mintakód-kódokat. Teszteléshez is használhatja.

## <a name="get-the-code"></a>A kód letöltése

Töltse le a konzol tesztelési alkalmazásának kódját.

## <a name="net"></a>.NET

[Töltse le a mintakód](https://go.microsoft.com/fwlink/p/?LinkId=746682) , és szükség szerint módosítsa.

> [!IMPORTANT]
> Az alkalmazás létrehozása előtt frissítse a *App.config* fájl értékeit, hogy azok tükrözzék a [partner Center-hitelesítésben](partner-center-authentication.md)létrehozott Azure ad-hitelesítési adatokat. A korai fejlesztés vagy az éles környezetben történő tesztelés során az integrációs munkafolyamatok fiókjának beállításait kell használnia.

A *App.config* fájl **ScenarioSettings** részén megadhatja azokat a paramétereket, amelyek automatikusan átkerülnek a futtatott forgatókönyvekben.

A futtatott forgatókönyvek listájának módosításához a **IPartnerScenario \[ \] mainScenarios** vagy a *program.cs* -fájlban található egyéni Get- **forgatókönyvek** metódusban talál megjegyzéseket.

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Töltse le a mintakód](https://go.microsoft.com/fwlink/p/?LinkId=2026887) , és szükség szerint módosítsa.

> [!IMPORTANT]
> Az alkalmazás létrehozása előtt frissítse a fájlban lévő *SamplesConfigurations.js* értékeit, hogy azok tükrözzék a [partner Center-hitelesítésben](partner-center-authentication.md)létrehozott Azure ad-hitelesítési adatokat. A korai fejlesztés vagy az éles környezetben történő tesztelés során az integrációs munkafolyamatok fiókjának beállításait kell használnia.

A fájl *SamplesConfiguration.js* **ScenarioSettings** alatt megadhatja azokat a paramétereket, amelyek automatikusan átkerülnek a futtatott forgatókönyvekben.

A futtatott forgatókönyvek listájának módosításához a **IPartnerScenario \[ \] MainScenarios** vagy a *program. Java* fájlban található egyéni **Get-forgatókönyvek** metódusban talál megjegyzéseket.

## <a name="what-to-change"></a>Mi a változás?

A következő listában megadhatja, hogy mit kell módosítani, vagy nem változik a mintakód.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

A **PartnerServiceSettings** esetében ne módosítsa a következőt:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

Ezen beállítások mindegyike szükséges ahhoz, hogy a minta API-hívások megfelelően működjenek.

### <a name="userauthentication"></a>UserAuthentication

A **UserAuthentication** esetében módosítania kell a következőt:

- **ApplicationId** (a bejelentkezéshez használt Azure Active Directory-alkalmazás azonosítója)
- **Username** (az Active Directory-beli Felhasználónév)
- **Jelszó** (az Active Directory-jelszó).

Ne módosítsa:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

A **AppAuthentication** esetében módosítania kell a következőt:

- **ApplicationId** (az alkalmazás-bejelentkezéshez használt Active Directory-alkalmazás azonosítója)
- **ApplicationSecret** (az alkalmazás-bejelentkezéshez használt Active Directory-alkalmazás titka)
- **Tartomány** (az Active Directory-tartomány, amelyen az alkalmazás fut)

### <a name="scenariosettings"></a>ScenarioSettings

A **ScenarioSettings** esetében ne módosítsa a következőt:

- **CustomerDomainSuffix** (az új ügyfél létrehozásakor használt tartomány utótagja)

Választható beállítások. Ha a mezőt üresen hagyja, akkor ezeket az információkat meg kell adni, ha szükség van a forgatókönyv futtatására:

- **CustomerIdToDelete** (a törléshez használt ügyfél azonosítója)
- **DefaultCustomerId** (az ügyfélhez kapcsolódó forgatókönyvekben használandó ügyfél-azonosító)
- **DefaultInvoiceID** (a számlázási helyzetekben használandó számlázási azonosító)
- **PartnerMpnId** (a partner MPN-azonosítóját használja a közvetett partneri forgatókönyvekben való használatra)
- **DefaultServiceRequestId** (a szolgáltatási kérelem azonosítójának használata a szolgáltatás kérelmezési forgatókönyvében)
- **DefaultSupportTopicID** (a szolgáltatási kérelemben használni kívánt támogatási témakör azonosítója)
- **DefaultOfferID** (az ajánlati forgatókönyvekben használandó ajánlat azonosítója)
- **DefaultOrderID** (a sorrendben használandó sorrend-azonosító)
- **DefaultSubscriptionID** (az ELŐfizetési azonosítók az előfizetési forgatókönyvekben használhatók)

A módosítás nem kötelező. Az összes beállítás a lapozható tartalom beolvasása során az egyes lapokon megjelenő bejegyzések mennyiségét határozza meg:

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**
