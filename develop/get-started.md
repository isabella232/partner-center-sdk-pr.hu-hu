---
title: Bevezetés
description: A Partnerközpont SDK tartalmaz egy felügyelt API-t és egy REST API, amelyek segítségével a partnerek kezelhetik az ügyfelek, az előfizetések és a rendelési adatokat.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b5d05f26d63574ef876519091dc1c33c05f36e25
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548753"
---
# <a name="get-started"></a><span data-ttu-id="22539-103">Bevezetés</span><span class="sxs-lookup"><span data-stu-id="22539-103">Get started</span></span>

<span data-ttu-id="22539-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="22539-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="22539-105">A Partnerközpont SDK tartalmaz egy felügyelt API-t és egy REST API, amelyek segítségével a partnerek kezelhetik az ügyfelek, az előfizetések és a rendelési adatokat.</span><span class="sxs-lookup"><span data-stu-id="22539-105">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="22539-106">A kód letöltése</span><span class="sxs-lookup"><span data-stu-id="22539-106">Get the code</span></span>

[<span data-ttu-id="22539-107">A Partnerközpont SDK</span><span class="sxs-lookup"><span data-stu-id="22539-107">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="22539-108">A közvetett viszonteladók Partnerközpont api-hozzáférése nem támogatott forgatókönyv.</span><span class="sxs-lookup"><span data-stu-id="22539-108">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="22539-109">Az alkalmazás verziójának Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="22539-109">Determine your version of Partner Center</span></span>

<span data-ttu-id="22539-110">A Partnerközpont egyes verziói nem érhetők el a teljes SDK-val.</span><span class="sxs-lookup"><span data-stu-id="22539-110">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="22539-111">További információ: [Developing for Partnerközpont for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="22539-111">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="22539-112">A minták lekért száma</span><span class="sxs-lookup"><span data-stu-id="22539-112">Get the samples</span></span>

<span data-ttu-id="22539-113">A C#-kódrészletekkel, a REST-mintákkal és a mintaalkalmazással kapcsolatos további információkért tekintse meg az [Partnerközpont példákat.](partner-center-samples.md)</span><span class="sxs-lookup"><span data-stu-id="22539-113">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="22539-114">Tesztelés és éles környezet</span><span class="sxs-lookup"><span data-stu-id="22539-114">Test vs. production</span></span>

<span data-ttu-id="22539-115">A kód első írásakor és tesztelése közben érdemes az integrációs tesztfiókot (és a megfelelő jogkivonatokat) használni, hogy véletlenül se legyen olyan új díj, amelyért a cég fizet.</span><span class="sxs-lookup"><span data-stu-id="22539-115">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="22539-116">További információ erről a tesztkörnyezetről: [API-hozzáférés beállítása a Partnerközpont.](set-up-api-access-in-partner-center.md)</span><span class="sxs-lookup"><span data-stu-id="22539-116">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="22539-117">Ha a megoldás tesztelve van, és készen áll a valós ügyfélfiókok használatára, frissítenie kell a jogkivonatokat, hogy az Elsődleges ügyfélfióknak megfelelő Azure AD-ügyfélalkalmazást és titkos Partnerközpont használ.</span><span class="sxs-lookup"><span data-stu-id="22539-117">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="22539-118">A teszteléssel és hibakereséssel kapcsolatos tippekért és javaslatokért, beleértve az éles környezetben végzett teszteléssel (TiP) és az integrációs tesztekkel kapcsolatos további információkat, lásd: Tesztelés és [hibakeresés.](test-and-debug.md)</span><span class="sxs-lookup"><span data-stu-id="22539-118">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="22539-119">A hitelesítés konfigurálása</span><span class="sxs-lookup"><span data-stu-id="22539-119">Configure your authentication</span></span>

<span data-ttu-id="22539-120">Ha az Azure AD-hitelesítést a Partnerközpont API-k használatára konfigurálja, [lásd: Partnerközpont hitelesítés.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="22539-120">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22539-121">A Microsoft egy biztonságos, skálázható keretrendszert vezet be a felhőszolgáltató (CSP) partnerek és a vezérlőpult-szállítók (CPV) hitelesítéséhez az Microsoft Azure többtényezős hitelesítési (MFA) architektúrán keresztül.</span><span class="sxs-lookup"><span data-stu-id="22539-121">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="22539-122">Partnerközpont Azure AD-t használ a hitelesítéshez, a Partnerközpont API-khoz pedig megfelelően kell konfigurálnia a hitelesítési beállításokat.</span><span class="sxs-lookup"><span data-stu-id="22539-122">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="22539-123">További információ: [Biztonságos alkalmazásmodell engedélyezése.](enable-secure-app-model.md)</span><span class="sxs-lookup"><span data-stu-id="22539-123">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="22539-124">Segítség kérése</span><span class="sxs-lookup"><span data-stu-id="22539-124">Get help</span></span>

<span data-ttu-id="22539-125">A partnerek a következő csoportban [kaphatnak Partnerközpont SDK Yammer támogatást:](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span><span class="sxs-lookup"><span data-stu-id="22539-125">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="22539-126">Ha személyre szabottabb segítséget szeretné kapni, a fejlesztők az MPN támogatási előnyeit vagy a Premier szintű támogatás.</span><span class="sxs-lookup"><span data-stu-id="22539-126">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="22539-127">Csatlakozzon a Partnerközpont API és az SDK korai felhasználói programjához</span><span class="sxs-lookup"><span data-stu-id="22539-127">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="22539-128">Ha meg szeretne tudni, hogyan működhet együtt a Microsofttal a partneri funkciók és képességek fejlesztésében, tekintse meg a Join the Partnerközpont API and SDK Early Adopter Program (Csatlakozás az Partnerközpont API-hoz és az [SDK early Adopter Programhoz) részt.](early-adopter-program.md)</span><span class="sxs-lookup"><span data-stu-id="22539-128">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
