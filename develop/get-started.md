---
title: Bevezetés
description: A Partnerközpont SDK tartalmaz egy felügyelt API-t és egy REST API, amelyek segítségével a partnerek kezelhetik az ügyfelek, az előfizetések és a rendelési adatokat.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 340b46978d71bdf5fa6f6795d69fe0721d808c4eb2650744e82510c208dd5b8f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989695"
---
# <a name="get-started"></a>Bevezetés

**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government

A Partnerközpont SDK tartalmaz egy felügyelt API-t és egy REST API, amelyek segítségével a partnerek kezelhetik az ügyfelek, az előfizetések és a rendelési adatokat.

## <a name="get-the-code"></a>A kód letöltése

[Töltse le a Partnerközpont SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> A közvetett viszonteladók Partnerközpont api-hozzáférése nem támogatott forgatókönyv.

## <a name="determine-your-version-of-partner-center"></a>Állapítsa meg a Partnerközpont

A Partnerközpont egyes verziói nem állnak rendelkezésre a teljes SDK-val. További információ: [Developing for Partnerközpont for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).

## <a name="get-the-samples"></a>Minták lekérte

A C#-kódrészletekkel, a REST-mintákkal és a mintaalkalmazással kapcsolatos további információkért lásd a Partnerközpont [példákat.](partner-center-samples.md)

## <a name="test-vs-production"></a>Tesztelés és éles környezet

A kód első írásakor és tesztelése közben érdemes az integrációs tesztfiókot (és a megfelelő jogkivonatokat) használnia, hogy véletlenül se legyen olyan új díj, amelyért a cége fizet. További információ erről a tesztkörnyezetről: [API-hozzáférés beállítása a Partnerközpont.](set-up-api-access-in-partner-center.md)

Amikor teszteli a megoldást, és készen áll a valódi ügyfélfiókok használatára, frissítenie kell a jogkivonatokat, hogy egy Azure AD-ügyfélalkalmazást és titkos szolgáltatásokat használjon, amelyek megfelelnek az elsődleges Partnerközpont fiókjának.

A teszteléssel és hibakereséssel kapcsolatos tippekért és javaslatokért, beleértve az éles környezetben végzett teszteléssel (TiP) és az integrációs tesztekkel kapcsolatos további információkat, lásd: [Tesztelés](test-and-debug.md)és hibakeresés.

## <a name="configure-your-authentication"></a>A hitelesítés konfigurálása

Ha az Azure AD-hitelesítést a Partnerközpont API-k használatára konfigurálja, tekintse meg a [Partnerközpont használatát.](partner-center-authentication.md)

> [!IMPORTANT]
> A Microsoft egy biztonságos, skálázható keretrendszert vezet be a felhőszolgáltató (CSP) partnerek és a vezérlőpult-szállítók (CPV) hitelesítéséhez az Microsoft Azure multi-factor authentication (MFA) architektúrán keresztül.
Partnerközpont Azure AD-t használ a hitelesítéshez, az Partnerközpont API-khoz pedig megfelelően kell konfigurálnia a hitelesítési beállításokat.
>
> További információ: [Biztonságos alkalmazásmodell engedélyezése.](enable-secure-app-model.md)

## <a name="get-help"></a>Segítség kérése

A partnerek a következő csoportban [kaphatnak Partnerközpont SDK Yammer támogatást:](https://go.microsoft.com/fwlink/p/?LinkID=717360). A fejlesztők személyre szabottabb segítséget kaphatnak, ha az MPN támogatási előnyeit vagy a Premier szintű támogatás.

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>Csatlakozzon a Partnerközpont API és az SDK korai felhasználói programjához

Ha meg szeretne tudni, hogyan működhet együtt a Microsofttal a partneri funkciók és képességek fejlesztésében, tekintse meg a Join the Partnerközpont API and SDK Early Adopter Program (Csatlakozás az Partnerközpont API-hoz és az [SDK early Adopter Programhoz) részt.](early-adopter-program.md)
