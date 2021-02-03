---
title: Bevezetés
description: A partner Center SDK egy felügyelt API-t és egy REST API biztosít a partnerek számára az ügyfelek, az előfizetések és a megrendelések kezeléséhez.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c2af1e11dbda19489a27e37c7f3de8ede90fd1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/08/2020
ms.locfileid: "97767912"
---
# <a name="get-started"></a>Bevezetés

**A következőkre vonatkozik**

- Partnerközpont
- A 21Vianet által üzemeltetett partneri központ
- A Microsoft Cloud Germany Partnerközpontja
- A Microsoft Cloud for US Government Partnerközpontja

A partner Center SDK egy felügyelt API-t és egy REST API biztosít a partnerek számára az ügyfelek, az előfizetések és a megrendelések kezeléséhez.

## <a name="get-the-code"></a>A kód letöltése

[A partner Center SDK letöltése](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> Az API-hozzáférés a közvetett viszonteladók számára nem támogatott forgatókönyv.

## <a name="determine-your-version-of-partner-center"></a>A partner központ verziójának meghatározása

A partner központ egyes verziói nem rendelkeznek a teljes SDK-val. További információ: [a Microsoft nemzeti felhőhöz készült partneri központ fejlesztése](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="get-the-samples"></a>A minták beszerzése

További információ a C# kódrészletekről, a REST-mintákról és a minta alkalmazásról: [partner Center-minták](partner-center-samples.md).

## <a name="test-vs-production"></a>Tesztelés és éles üzem

A kód első írásakor és tesztelésekor az Integration sandbox-fiókot (és a hozzá tartozó jogkivonatokat) kell használnia, így nem kell véletlenül új díjakat fizetnie, amelyeket a vállalata fizet. További információ erről a tesztelési környezetről: [API-hozzáférés beállítása a partner Centerben](set-up-api-access-in-partner-center.md).

Ha a megoldást tesztelik, és készen állnak a valós ügyfél-fiókokra, frissítenie kell a jogkivonatokat, hogy egy Azure AD-ügyfélalkalmazás és egy, az elsődleges partner Center-fióknak megfelelő titkos kulcsot használjon.

A teszteléssel és a hibakereséssel kapcsolatos tippeket és javaslatokat, beleértve a teszteléssel és [a hibakereséssel](test-and-debug.md)kapcsolatos további információkat is.

## <a name="configure-your-authentication"></a>A hitelesítés konfigurálása

Az Azure AD-hitelesítés konfigurálásához, hogy használhassa a partner Center API-kat, lásd: a [partner Center hitelesítése](partner-center-authentication.md).

> [!IMPORTANT]
> A Microsoft a Microsoft Azure multi-Factor Authentication (MFA) architektúrán keresztül biztonságos, méretezhető keretrendszert biztosít a Cloud Solution Provider (CSP) partnerek és a Vezérlőpult-szállítók (CPV) hitelesítéséhez.
A partner Center az Azure AD-t használja a hitelesítéshez, a partner Center API-k használatához pedig helyesen kell konfigurálnia a hitelesítési beállításokat.
>
> További információt a [biztonságos alkalmazás modelljének engedélyezése](enable-secure-app-model.md)című témakörben talál.

## <a name="get-help"></a>Segítség kérése

A partnerek támogatást kérhetnek a [partner Center SDK Yammer csoportjában](https://go.microsoft.com/fwlink/p/?LinkID=717360). Ha további személyre szabott segítséget szeretne kapni, a fejlesztők az MPN-támogatás előnyeit vagy a Premier szintű támogatás is használhatják.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Csatlakozzon a Partnerközpont API és az SDK korai felhasználói programjához

Ha szeretné megtudni, hogyan dolgozhat a Microsofttal a partneri funkciók és képességek fejlesztésével kapcsolatban, tekintse meg a következő témakört: [Csatlakozás a partner Center API-hoz és az SDK korai](early-adopter-program.md)bevezetési programhoz.
