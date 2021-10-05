---
title: Bevezetés
description: A Partnerközpont SDK tartalmaz egy felügyelt API-t és egy REST API, amelyek segítségével a partnerek kezelhetik az ügyfelek, az előfizetések és a rendelési adatokat.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.custom: intro-get-started
ms.openlocfilehash: affc19c8533fddd7212d52cf02e013531bacdcc5
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439310"
---
# <a name="get-started"></a>Bevezetés

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont SDK tartalmaz egy felügyelt API-t és egy REST API, amelyek segítségével a partnerek kezelhetik az ügyfelek, az előfizetések és a rendelési adatokat.

## <a name="get-the-code"></a>A kód letöltése

[Töltse le a Partnerközpont SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> A közvetett viszonteladók Partnerközpont api-hozzáférése nem támogatott forgatókönyv.

## <a name="determine-your-version-of-partner-center"></a>Az alkalmazás verziójának Partnerközpont

A Partnerközpont egyes verziói nem érhetők el a teljes SDK-val. További információ: [Developing for Partnerközpont for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="get-the-samples"></a>A minták lekért száma

A C#-kódrészletekkel, a REST-mintákkal és a mintaalkalmazással kapcsolatos további információkért lásd a Partnerközpont [példákat.](partner-center-samples.md)

## <a name="test-vs-production"></a>Tesztelés és éles környezet

A kód első írásakor és tesztelése közben érdemes az integrációs tesztfiókot (és a megfelelő jogkivonatokat) használni, hogy véletlenül se legyen olyan új díj, amelyért a cég fizet. További információ erről a tesztkörnyezetről: [API-hozzáférés beállítása a Partnerközpont.](set-up-api-access-in-partner-center.md)

Ha a megoldás tesztelve van, és készen áll a valós ügyfélfiókok használatára, frissítenie kell a jogkivonatokat, hogy olyan Azure AD-ügyfélalkalmazást és titkos szolgáltatásokat használjon, amelyek megfelelnek az elsődleges Partnerközpont-fiókjának.

A teszteléssel és hibakereséssel kapcsolatos tippekért és javaslatokért, beleértve az éles környezetben végzett teszteléssel (TiP) és az integrációs tesztekkel kapcsolatos további információkat, lásd: Tesztelés és [hibakeresés.](test-and-debug.md)

## <a name="configure-your-authentication"></a>A hitelesítés konfigurálása

Az Azure AD-hitelesítés konfigurálás a Partnerközpont API-k használatára: Partnerközpont [hitelesítés.](partner-center-authentication.md)

> [!IMPORTANT]
> A Microsoft egy biztonságos, skálázható keretrendszert vezet be a felhőszolgáltató (CSP) partnerek és a vezérlőpult-szállítók (CPV) hitelesítéséhez az Microsoft Azure többtényezős hitelesítési (MFA) architektúrán keresztül.
Partnerközpont Azure AD-t használ a hitelesítéshez, a Partnerközpont API-khoz pedig megfelelően kell konfigurálnia a hitelesítési beállításokat.
>
> További információ: [Biztonságos alkalmazásmodell engedélyezése.](enable-secure-app-model.md)

## <a name="get-help"></a>Segítség kérése

A partnerek a következő csoportban [kaphatnak Partnerközpont SDK Yammer támogatást:](https://go.microsoft.com/fwlink/p/?LinkID=717360). A fejlesztők személyre szabottabb segítséget kaphatnak, ha az MPN-támogatás előnyeit vagy a Premier szintű támogatás.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Csatlakozzon a Partnerközpont API és az SDK korai felhasználói programjához

Ha meg szeretne tudni, hogyan működhet együtt a Microsofttal a partneri funkciók és képességek fejlesztésében, tekintse meg a Join the Partnerközpont API and SDK Early Adopter Program (Csatlakozás az Partnerközpont API-hoz és az [SDK early Adopter Programhoz) részt.](early-adopter-program.md)
