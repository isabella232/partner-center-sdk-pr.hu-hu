---
title: Partnerközpont – REST API-referencia
description: Ismerje meg, hogy a CSP-partnerek hogyan használhatjak Partnerközpont REST API-kat CRM- és számlázási szoftvereik Microsoft-rendszerekkel való integrálásához az ügyfélfiókok jobb kezelése érdekében.
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 18621fdb94f91f066b69a11f7d557410d653787e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548039"
---
# <a name="partner-center-rest-api-reference-to-rest-urls-rest-headers-rest-resources-and-rest-events"></a><span data-ttu-id="44944-103">Partnerközpont REST API REST URL-címekre, REST-fejlécekre, REST-erőforrásokra és REST-eseményekre való hivatkozás</span><span class="sxs-lookup"><span data-stu-id="44944-103">Partner Center REST API reference to REST URLs, REST headers, REST resources, and REST events</span></span>

<span data-ttu-id="44944-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="44944-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="partner-center-rest-api"></a><span data-ttu-id="44944-105">Partnerközpont REST API</span><span class="sxs-lookup"><span data-stu-id="44944-105">Partner Center REST API</span></span>

<span data-ttu-id="44944-106">A Partnerközpont REST API segítségével Felhőszolgáltató (CSP) partnerek integrálják meglévő CRM- vagy számlázási szoftvereiket az ügyfélfiókokat kezelő, rendeléseket kezelő, előfizetéseket kezelő és támogatási kéréseket kezelő Microsoft-rendszerekkel.</span><span class="sxs-lookup"><span data-stu-id="44944-106">The Partner Center REST API helps Cloud Solution Provider (CSP) partners integrate their existing CRM or billing software with the Microsoft systems that manage customer accounts, place orders, manage subscriptions, and handle support requests.</span></span>

<span data-ttu-id="44944-107">Az API-val kapcsolatos további információkért, beleértve a mintakódot is, a [Forgatókönyvek](scenarios.md) témakörben talál, beleértve a háttér-áttekintést.</span><span class="sxs-lookup"><span data-stu-id="44944-107">For more information about what the API can do, including sample code, see the [Scenarios](scenarios.md) topic, including the background overview.</span></span>

<span data-ttu-id="44944-108">A kódolás megkezdése előtt olvassa el az [Első lépések témakört.](get-started.md)</span><span class="sxs-lookup"><span data-stu-id="44944-108">Before you begin coding, read the [Get started](get-started.md) topic.</span></span> <span data-ttu-id="44944-109">Ez a cikk a teszt- és éles fiókok beállításáról, a hitelesítés megfelelő beállításáról és a mintakód megkeresésről tartalmaz információkat.</span><span class="sxs-lookup"><span data-stu-id="44944-109">This article contains information about setting up your test and production accounts, getting authentication working, and finding the sample code.</span></span>

<span data-ttu-id="44944-110">Az egyes API-okat magyarázó referencia-útmutatóért lásd: [Partnerközpont REST API.](/rest/api/partner-center-rest/)</span><span class="sxs-lookup"><span data-stu-id="44944-110">For a reference guide explaining each API, see [Partner Center REST API](/rest/api/partner-center-rest/).</span></span>

## <a name="topics"></a><span data-ttu-id="44944-111">Témakörök</span><span class="sxs-lookup"><span data-stu-id="44944-111">Topics</span></span>

| <span data-ttu-id="44944-112">Témakör</span><span class="sxs-lookup"><span data-stu-id="44944-112">Topic</span></span> | <span data-ttu-id="44944-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="44944-113">Description</span></span> |
| ----- | ----------- |
| [<span data-ttu-id="44944-114">Partnerközpont REST API</span><span class="sxs-lookup"><span data-stu-id="44944-114">Partner Center REST API</span></span>](/rest/api/partner-center-rest/) | <span data-ttu-id="44944-115">Az egyes REST API elérhető Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="44944-115">Reference of each REST API available for Partner Center.</span></span> |
| [<span data-ttu-id="44944-116">Partnerközpont – REST URL-címek</span><span class="sxs-lookup"><span data-stu-id="44944-116">Partner Center REST URLs</span></span>](partner-center-rest-urls.md) | <span data-ttu-id="44944-117">Meghatározza a REST API különböző verzióinak végpontjainak Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="44944-117">Defines the REST API endpoints for different versions of Partner Center.</span></span> |
| [<span data-ttu-id="44944-118">Partnerközpont – REST-fejlécek</span><span class="sxs-lookup"><span data-stu-id="44944-118">Partner Center REST headers</span></span>](headers.md) | <span data-ttu-id="44944-119">Meghatározza a kérés és a válasz fejlécét, amelyet a REST API.</span><span class="sxs-lookup"><span data-stu-id="44944-119">Defines the request and response headers used by the REST API.</span></span> |
| [<span data-ttu-id="44944-120">Partnerközpont – REST-erőforrások</span><span class="sxs-lookup"><span data-stu-id="44944-120">Partner Center REST resources</span></span>](partner-center-rest-resources.md) | <span data-ttu-id="44944-121">Meghatározza azokat a JSON-szerkezeteket, amelyek a REST API.</span><span class="sxs-lookup"><span data-stu-id="44944-121">Defines the JSON constructs that represent the objects needed to use the REST API.</span></span> |
| [<span data-ttu-id="44944-122">Partnerközpont – REST-események</span><span class="sxs-lookup"><span data-stu-id="44944-122">Partner Center REST events</span></span>](partner-center-webhook-events.md) | <span data-ttu-id="44944-123">Meghatározza a webhookok által támogatott REST-Partnerközpont eseményeket.</span><span class="sxs-lookup"><span data-stu-id="44944-123">Defines the REST resource change events that are supported by Partner Center webhooks.</span></span> |
| [<span data-ttu-id="44944-124">Partnerközpont – támogatott nyelvek és területi beállítások</span><span class="sxs-lookup"><span data-stu-id="44944-124">Partner Center supported languages and locales</span></span>](partner-center-supported-languages-and-locales.md) | <span data-ttu-id="44944-125">Az API-k által támogatott területi listákat, nyelveket és ország-/régiókódokat Partnerközpont sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="44944-125">Lists the locales, languages, and country/region codes that are supported in the Partner Center APIs.</span></span> |
| [<span data-ttu-id="44944-126">Partnerközpont – webhookok</span><span class="sxs-lookup"><span data-stu-id="44944-126">Partner Center webhooks</span></span>](partner-center-webhooks.md) | <span data-ttu-id="44944-127">Események fogadása, visszahívás hitelesítése és Partnerközpont webhook API-k használata eseményregisztráció létrehozásához, megtekintéséhez és frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="44944-127">How to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration.</span></span> |
