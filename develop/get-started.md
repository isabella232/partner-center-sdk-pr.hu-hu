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
# <a name="get-started"></a><span data-ttu-id="f858a-103">Bevezetés</span><span class="sxs-lookup"><span data-stu-id="f858a-103">Get started</span></span>

<span data-ttu-id="f858a-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="f858a-104">**Applies To**</span></span>

- <span data-ttu-id="f858a-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="f858a-105">Partner Center</span></span>
- <span data-ttu-id="f858a-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="f858a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f858a-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f858a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f858a-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="f858a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f858a-109">A partner Center SDK egy felügyelt API-t és egy REST API biztosít a partnerek számára az ügyfelek, az előfizetések és a megrendelések kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="f858a-109">The Partner Center SDK includes a managed API and a REST API for partners to use to manage customer, subscription, and order data.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="f858a-110">A kód letöltése</span><span class="sxs-lookup"><span data-stu-id="f858a-110">Get the code</span></span>

[<span data-ttu-id="f858a-111">A partner Center SDK letöltése</span><span class="sxs-lookup"><span data-stu-id="f858a-111">Download the Partner Center SDK</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> <span data-ttu-id="f858a-112">Az API-hozzáférés a közvetett viszonteladók számára nem támogatott forgatókönyv.</span><span class="sxs-lookup"><span data-stu-id="f858a-112">API access to Partner Center for indirect resellers isn't a supported scenario.</span></span>

## <a name="determine-your-version-of-partner-center"></a><span data-ttu-id="f858a-113">A partner központ verziójának meghatározása</span><span class="sxs-lookup"><span data-stu-id="f858a-113">Determine your version of Partner Center</span></span>

<span data-ttu-id="f858a-114">A partner központ egyes verziói nem rendelkeznek a teljes SDK-val.</span><span class="sxs-lookup"><span data-stu-id="f858a-114">Some versions of Partner Center do not have the entire SDK available.</span></span> <span data-ttu-id="f858a-115">További információ: [a Microsoft nemzeti felhőhöz készült partneri központ fejlesztése](developing-for-partner-center-for-microsoft-national-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-115">For more information, see [Developing for Partner Center for Microsoft National Cloud](developing-for-partner-center-for-microsoft-national-cloud.md).</span></span>

## <a name="get-the-samples"></a><span data-ttu-id="f858a-116">A minták beszerzése</span><span class="sxs-lookup"><span data-stu-id="f858a-116">Get the samples</span></span>

<span data-ttu-id="f858a-117">További információ a C# kódrészletekről, a REST-mintákról és a minta alkalmazásról: [partner Center-minták](partner-center-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-117">For more information about C# snippets, REST samples, and the sample app, see [Partner Center samples](partner-center-samples.md).</span></span>

## <a name="test-vs-production"></a><span data-ttu-id="f858a-118">Tesztelés és éles üzem</span><span class="sxs-lookup"><span data-stu-id="f858a-118">Test vs. production</span></span>

<span data-ttu-id="f858a-119">A kód első írásakor és tesztelésekor az Integration sandbox-fiókot (és a hozzá tartozó jogkivonatokat) kell használnia, így nem kell véletlenül új díjakat fizetnie, amelyeket a vállalata fizet.</span><span class="sxs-lookup"><span data-stu-id="f858a-119">While you are initially writing and testing your code, you should use your integration sandbox account (and the corresponding tokens) so that you don't accidentally incur new charges that your company is responsible for paying.</span></span> <span data-ttu-id="f858a-120">További információ erről a tesztelési környezetről: [API-hozzáférés beállítása a partner Centerben](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-120">For more information about this testing environment, see [Set up API access in Partner Center](set-up-api-access-in-partner-center.md).</span></span>

<span data-ttu-id="f858a-121">Ha a megoldást tesztelik, és készen állnak a valós ügyfél-fiókokra, frissítenie kell a jogkivonatokat, hogy egy Azure AD-ügyfélalkalmazás és egy, az elsődleges partner Center-fióknak megfelelő titkos kulcsot használjon.</span><span class="sxs-lookup"><span data-stu-id="f858a-121">When your solution is tested and ready to use on real customer accounts, you'll have to update your tokens so that you're using an Azure AD client app and secret that correspond to your Primary Partner Center account.</span></span>

<span data-ttu-id="f858a-122">A teszteléssel és a hibakereséssel kapcsolatos tippeket és javaslatokat, beleértve a teszteléssel és [a hibakereséssel](test-and-debug.md)kapcsolatos további információkat is.</span><span class="sxs-lookup"><span data-stu-id="f858a-122">For tips and suggestions about testing and debugging, including more information about Test-in-Production (TiP) and the Integration Sandbox, see [Test and debug](test-and-debug.md).</span></span>

## <a name="configure-your-authentication"></a><span data-ttu-id="f858a-123">A hitelesítés konfigurálása</span><span class="sxs-lookup"><span data-stu-id="f858a-123">Configure your authentication</span></span>

<span data-ttu-id="f858a-124">Az Azure AD-hitelesítés konfigurálásához, hogy használhassa a partner Center API-kat, lásd: a [partner Center hitelesítése](partner-center-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f858a-124">To configure your Azure AD authentication so that you can use the Partner Center APIs, see [Partner Center authentication](partner-center-authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f858a-125">A Microsoft a Microsoft Azure multi-Factor Authentication (MFA) architektúrán keresztül biztonságos, méretezhető keretrendszert biztosít a Cloud Solution Provider (CSP) partnerek és a Vezérlőpult-szállítók (CPV) hitelesítéséhez.</span><span class="sxs-lookup"><span data-stu-id="f858a-125">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>
<span data-ttu-id="f858a-126">A partner Center az Azure AD-t használja a hitelesítéshez, a partner Center API-k használatához pedig helyesen kell konfigurálnia a hitelesítési beállításokat.</span><span class="sxs-lookup"><span data-stu-id="f858a-126">Partner Center uses Azure AD for authentication, and to use the Partner Center APIs you must configure your authentication settings correctly.</span></span>
>
> <span data-ttu-id="f858a-127">További információt a [biztonságos alkalmazás modelljének engedélyezése](enable-secure-app-model.md)című témakörben talál.</span><span class="sxs-lookup"><span data-stu-id="f858a-127">For more information, see [Enable secure application model](enable-secure-app-model.md).</span></span>

## <a name="get-help"></a><span data-ttu-id="f858a-128">Segítség kérése</span><span class="sxs-lookup"><span data-stu-id="f858a-128">Get help</span></span>

<span data-ttu-id="f858a-129">A partnerek támogatást kérhetnek a [partner Center SDK Yammer csoportjában](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span><span class="sxs-lookup"><span data-stu-id="f858a-129">Partners can get support at the [Partner Center SDK Yammer group](https://go.microsoft.com/fwlink/p/?LinkID=717360).</span></span> <span data-ttu-id="f858a-130">Ha további személyre szabott segítséget szeretne kapni, a fejlesztők az MPN-támogatás előnyeit vagy a Premier szintű támogatás is használhatják.</span><span class="sxs-lookup"><span data-stu-id="f858a-130">To get more personalized help, developers can use their MPN support benefits or Premier Support.</span></span>

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a><span data-ttu-id="f858a-131">Csatlakozzon a Partnerközpont API és az SDK korai felhasználói programjához</span><span class="sxs-lookup"><span data-stu-id="f858a-131">Join the Partner Center API and SDK Early Adopter Program</span></span>

<span data-ttu-id="f858a-132">Ha szeretné megtudni, hogyan dolgozhat a Microsofttal a partneri funkciók és képességek fejlesztésével kapcsolatban, tekintse meg a következő témakört: [Csatlakozás a partner Center API-hoz és az SDK korai](early-adopter-program.md)bevezetési programhoz.</span><span class="sxs-lookup"><span data-stu-id="f858a-132">To find out how you can collaborate with Microsoft on the development of Partner features and capabilities, see [Join the Partner Center API and SDK Early Adopter Program](early-adopter-program.md).</span></span>
