---
title: Partnerközpont – REST API-referencia
description: Ismerje meg, hogy a CSP-partnerek hogyan használhatják a partner Center REST API-kat a CRM-és számlázási szoftverek Microsoft-rendszerekkel való integrálásához, hogy jobban kezeljék az ügyfelek fiókjait
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 3f83b2b73c3480f76646cae4fcbbcbacd31d4b3f
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/11/2020
ms.locfileid: "97768503"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="ed9ec-103">A partner Center REST API a REST URL-címekre, a REST-fejlécekre, a REST-erőforrásokra és a REST-eseményekre</span><span class="sxs-lookup"><span data-stu-id="ed9ec-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="ed9ec-104">**A következőkre vonatkozik:**</span><span class="sxs-lookup"><span data-stu-id="ed9ec-104">**Applies to:**</span></span>

- <span data-ttu-id="ed9ec-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="ed9ec-105">Partner Center</span></span>
- <span data-ttu-id="ed9ec-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="ed9ec-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ed9ec-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ed9ec-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ed9ec-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="ed9ec-108">Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="ed9ec-109">Partner Center REST API</span><span class="sxs-lookup"><span data-stu-id="ed9ec-109">Partner Center REST API</span></span>

<span data-ttu-id="ed9ec-110">A partner Center REST API segíti a Cloud Solution Provider (CSP) partnerei számára a meglévő CRM-vagy számlázási szoftverek integrálását a felhasználói fiókokat kezelő Microsoft-rendszerekkel, a megrendelések megrendelésével, az előfizetések kezelésével és a támogatási kérelmek kezelésével.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-110">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="ed9ec-111">További információ arról, hogy mit tehet az API, beleértve a mintakódt is, a [forgatókönyvek](scenarios.md) témakörben, beleértve a háttér áttekintését.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-111">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="ed9ec-112">A kódolás megkezdése előtt olvassa el az [első lépések](get-started.md) témakört.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-112">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="ed9ec-113">Ez a cikk a tesztelési és üzemi fiókok beállításával, a hitelesítés működésének beszerzésével és a mintakód megkeresésével kapcsolatos információkat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-113">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

## <a name="topics"></a><span data-ttu-id="ed9ec-114">Témakörök</span><span class="sxs-lookup"><span data-stu-id="ed9ec-114">Topics</span></span>

| <span data-ttu-id="ed9ec-115">Témakör</span><span class="sxs-lookup"><span data-stu-id="ed9ec-115">Topic</span></span> | <span data-ttu-id="ed9ec-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="ed9ec-116">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="ed9ec-117">Partnerközpont – REST URL-címek</span><span class="sxs-lookup"><span data-stu-id="ed9ec-117">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="ed9ec-118">Meghatározza a partner központ különböző verzióihoz REST API végpontokat.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-118">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="ed9ec-119">Partnerközpont – REST-fejlécek</span><span class="sxs-lookup"><span data-stu-id="ed9ec-119">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="ed9ec-120">Meghatározza a REST API által használt kérelem és válasz fejléceit.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-120">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="ed9ec-121">Partnerközpont – REST-erőforrások</span><span class="sxs-lookup"><span data-stu-id="ed9ec-121">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="ed9ec-122">Azokat a JSON-szerkezeteket határozza meg, amelyek a REST API használatához szükséges objektumokat jelölik.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-122">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="ed9ec-123">Partnerközpont – REST-események</span><span class="sxs-lookup"><span data-stu-id="ed9ec-123">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="ed9ec-124">Meghatározza a partner Center webhookok által támogatott REST-erőforrás-módosítási eseményeket.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-124">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="ed9ec-125">Partnerközpont – támogatott nyelvek és területi beállítások</span><span class="sxs-lookup"><span data-stu-id="ed9ec-125">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="ed9ec-126">Felsorolja a partner Center API-k által támogatott területi beállításokat, nyelveket és ország/régió kódokat.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-126">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="ed9ec-127">Partnerközpont – webhookok</span><span class="sxs-lookup"><span data-stu-id="ed9ec-127">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="ed9ec-128">Események fogadása, visszahívás hitelesítése és a partner Center webhook API-k használata egy esemény regisztrációjának létrehozásához, megtekintéséhez és frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="ed9ec-128">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |