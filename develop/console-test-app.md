---
title: Konzolos tesztalkalmazás
description: Ez a konzoltesztalkalmazás mintakódot biztosít a Partnerközpont API-k által támogatott összes forgatókönyvhöz. Teszteléshez is használhatja.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974029"
---
# <a name="console-test-app"></a>Konzolos tesztalkalmazás

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A konzol tesztalkalmazása C# és Java nyelven van megtéve, és mintakódokat biztosít a Partnerközpont API-k által támogatott összes forgatókönyvhöz. Teszteléshez is használhatja.

## <a name="get-the-code"></a>A kód letöltése

Töltse le a konzoltesztalkalmazás mintakódját.

## <a name="net"></a>.NET

[Töltse le a mintakódot,](https://go.microsoft.com/fwlink/p/?LinkId=746682) és szükség szerint módosítsa.

> [!IMPORTANT]
> Az alkalmazás létrehozása előtt frissítse a App.config-fájlban található értékeket, hogy azok a hitelesítés során létrehozott Azure [AD-Partnerközpont tükrözzék.](partner-center-authentication.md) Pontosabban az integrációs tesztfiók beállításait kell használnia a fejlesztés korai szakaszában vagy éles környezetben való teszteléshez.

A **forgatókönyvfájl ScenarioSettings** *App.config* meg olyan paramétereket, amelyek automatikusan át lesznek állítva a futtatott forgatókönyvekbe.

A futtatott forgatókönyvek listájának módosításához megjegyzésbe kell tenni a sorokat az **IPartnerScenario \[ \] mainScenarios** vagy a *Program.cs* fájlban található egyedi **Forgatókönyv** lekért metódusban.

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[Töltse le a mintakódot,](https://go.microsoft.com/fwlink/p/?LinkId=2026887) és szükség szerint módosítsa.

> [!IMPORTANT]
> Az alkalmazás létrehozása előtt frissítse a fájlban *SamplesConfigurations.js* a fájlban található értékeket, hogy tükrözzék a hitelesítés során létrehozott Azure AD Partnerközpont adatokat. [](partner-center-authentication.md) Pontosabban az integrációs tesztfiók beállításait kell használnia a fejlesztés korai szakaszában vagy éles környezetben való teszteléshez.

A **Fájlon** találhatóSamplesConfiguration.js *ScenarioSettings* alatt olyan paramétereket állíthat be, amelyek automatikusan át lesznek állítva a futtatott forgatókönyvekbe.

A futtatott forgatókönyvek listájának módosításához megjegyzésbe kell tenni a sorokat az **IPartnerScenario \[ \] mainScenarios** vagy a *Program.java* fájlban található egyedi **Forgatókönyv** lekért metódusban.

## <a name="what-to-change"></a>Mi a módosítás?

Az alábbi listák segítségével meghatározhatja, hogy mit módosíthat a mintakódban.

### <a name="partnerservicesettings"></a>PartnerServiceSettings

A **PartnerServiceSettings beállításnál** ne módosítsa a következőt:

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain (Tartomány)**

Ezek a beállítások mind szükségesek a minta API-hívások megfelelő működéséhez.

### <a name="userauthentication"></a>UserAuthentication (Felhasználói hitelesítés)

A **UserAuthentication** esetén a következőt kell módosítania:

- **ApplicationId** (Azure Active Directory bejelentkezéshez használt alkalmazásazonosító)
- **Felhasználónév** (az Active Directory-felhasználóneve)
- **Jelszó** (az Active Directory-jelszó).

Ne módosítsa:

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

Az **AppAuthentication** esetén a következőt kell módosítania:

- **ApplicationId** (az alkalmazás bejelentkezéshez használt Active Directory-alkalmazásazonosítója)
- **ApplicationSecret** (az alkalmazásba való bejelentkezéshez használt Active Directory-alkalmazás titkos adatokat használ)
- **Tartomány** (az az Active Directory-tartomány, amelyen az alkalmazás üzemel)

### <a name="scenariosettings"></a>ScenarioSettings (Forgatókönyv-beállítások)

A **ScenarioSettings esetében** ne módosítsa a következőt:

- **CustomerDomainSuffix** (az új ügyfél létrehozásakor használt tartomány-utótag)

Nem kötelező beállítások. Ha üresen hagyja, akkor szükség esetén meg kell határoznia ezt az információt a forgatókönyvek futtatásakor:

- **CustomerIdToDelete** (a törléshez használt ügyfél azonosítója)
- **DefaultCustomerId** (az ügyfélhez kapcsolódó forgatókönyvekben használt ügyfélazonosító)
- **DefaultInvoiceID** (a számlázási forgatókönyvekben használt számlaazonosító)
- **PartnerMpnId** (a közvetett partneri forgatókönyvekben használt partner MPN-azonosítója)
- **DefaultServiceRequestId** (a szolgáltatáskérési forgatókönyvekben használt szolgáltatáskérés-azonosító)
- **DefaultSupportTopicID** (a támogatási témakör szolgáltatáskérési forgatókönyvekben használható azonosítója)
- **DefaultOfferID** (az ajánlati forgatókönyvekben használt ajánlatazonosító)
- **DefaultOrderID** (a megrendelési forgatókönyvekben használni szükséges rendelésazonosító)
- **DefaultSubscriptionID** (előfizetési forgatókönyvekben használni szükséges előfizetés-azonosító)

Nem kötelező módosítani. Ezek a beállítások határozzák meg az oldalankénti bejegyzések mennyiségét lapszámozási tartalom leolvasásakor:

- **CustomerPageSize (CustomerPageSize)**
- **InvoicePageSize (Számlaoldalak megszagorizálása**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize (Előfizetés lapja)**
