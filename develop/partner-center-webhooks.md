---
title: Partnerközpont – webhookok
description: A webhookok lehetővé teszik a partnerek számára az Erőforrás-változási események regisztrálását.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8225623ade7e922ac23ebf0ed9215686b0601244
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/22/2020
ms.locfileid: "97768024"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="8da90-103">Partnerközpont – webhookok</span><span class="sxs-lookup"><span data-stu-id="8da90-103">Partner Center webhooks</span></span>

<span data-ttu-id="8da90-104">**A következőkre vonatkozik**</span><span class="sxs-lookup"><span data-stu-id="8da90-104">**Applies To**</span></span>

- <span data-ttu-id="8da90-105">Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8da90-105">Partner Center</span></span>
- <span data-ttu-id="8da90-106">A 21Vianet által üzemeltetett partneri központ</span><span class="sxs-lookup"><span data-stu-id="8da90-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8da90-107">A Microsoft Cloud Germany Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8da90-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8da90-108">A Microsoft Cloud for US Government Partnerközpontja</span><span class="sxs-lookup"><span data-stu-id="8da90-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8da90-109">A partner Center webhook API-k lehetővé teszik a partnerek számára az Erőforrás-változási események regisztrálását.</span><span class="sxs-lookup"><span data-stu-id="8da90-109">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="8da90-110">Ezeket az eseményeket a rendszer HTTP-bejegyzések formájában továbbítja a partner regisztrált URL-címére.</span><span class="sxs-lookup"><span data-stu-id="8da90-110">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="8da90-111">A partneri központból érkező események fogadásához a partnerek visszahívást kapnak, ahol a partner Center közzéteheti az erőforrás-módosítási eseményt.</span><span class="sxs-lookup"><span data-stu-id="8da90-111">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="8da90-112">Az esemény digitálisan alá lesz írva, hogy a partner ellenőrizze, hogy a partner központból küldték-e el.</span><span class="sxs-lookup"><span data-stu-id="8da90-112">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="8da90-113">A partnerek a partner Center által támogatott webhook-eseményekről választhatnak, például a következő példákkal.</span><span class="sxs-lookup"><span data-stu-id="8da90-113">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="8da90-114">**Tesztelési esemény ("test-created")**</span><span class="sxs-lookup"><span data-stu-id="8da90-114">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="8da90-115">Ez az esemény lehetővé teszi, hogy saját bevezetést kérjen, és tesztelje a regisztrációt egy tesztelési esemény megadásával, majd a folyamat nyomon követésével.</span><span class="sxs-lookup"><span data-stu-id="8da90-115">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="8da90-116">Megtekintheti a Microsofttól érkező hibaüzeneteket, amikor az eseményt próbálja kézbesíteni.</span><span class="sxs-lookup"><span data-stu-id="8da90-116">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="8da90-117">Ez a korlátozás csak a "test-created" eseményekre vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="8da90-117">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="8da90-118">A hét napnál régebbi adatértékek törlődnek.</span><span class="sxs-lookup"><span data-stu-id="8da90-118">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="8da90-119">**Előfizetés frissített eseménye ("előfizetés-frissítve")**</span><span class="sxs-lookup"><span data-stu-id="8da90-119">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="8da90-120">Ez az esemény az előfizetés változásakor következik be.</span><span class="sxs-lookup"><span data-stu-id="8da90-120">This event is raised when the subscription changes.</span></span> <span data-ttu-id="8da90-121">Ezek az események akkor jönnek létre, ha a partner Center API-n keresztül végzett módosítások mellett belső módosítás is történik.</span><span class="sxs-lookup"><span data-stu-id="8da90-121">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8da90-122">Az előfizetés változásai és az előfizetés frissített eseményének megváltozása közötti időtartam 48 óra.</span><span class="sxs-lookup"><span data-stu-id="8da90-122">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="8da90-123">**Túllépte a küszöbértéket ("usagerecords-thresholdExceeded")**</span><span class="sxs-lookup"><span data-stu-id="8da90-123">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="8da90-124">Ez az esemény akkor következik be, ha az ügyfél Microsoft Azure használatának mennyisége meghaladja a használati költségekkel kapcsolatos költségvetést (a küszöbértéket).</span><span class="sxs-lookup"><span data-stu-id="8da90-124">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="8da90-125">További információ: [Azure-beli kiadások költségvetésének beállítása ügyfeleinek/partner-központ/set-an-Azure-költőpénzt-Budget-for-your-Customs).</span><span class="sxs-lookup"><span data-stu-id="8da90-125">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="8da90-126">**Hivatkozó létrehozott esemény ("hivatkozó-létrehozva")**</span><span class="sxs-lookup"><span data-stu-id="8da90-126">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="8da90-127">Ez az esemény az átirányítás létrehozásakor következik be.</span><span class="sxs-lookup"><span data-stu-id="8da90-127">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="8da90-128">**Hivatkozó frissített esemény ("referral-frissítve")**</span><span class="sxs-lookup"><span data-stu-id="8da90-128">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="8da90-129">Ez az esemény az átirányítás frissítésekor következik be.</span><span class="sxs-lookup"><span data-stu-id="8da90-129">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="8da90-130">**Számla üzemkész eseménye ("számla kész")**</span><span class="sxs-lookup"><span data-stu-id="8da90-130">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="8da90-131">Ez az esemény akkor következik be, amikor az új számla elkészült.</span><span class="sxs-lookup"><span data-stu-id="8da90-131">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="8da90-132">A jövőbeli webhook-események hozzáadódnak a rendszeren megjelenő olyan erőforrásokhoz, amelyek a partner által nem vezéreltek, és további frissítésekre kerül majd, hogy a lehető legrövidebb idő alatt megkapják ezeket az eseményeket.</span><span class="sxs-lookup"><span data-stu-id="8da90-132">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="8da90-133">A partnerek visszajelzései hasznosak lehetnek a felvenni kívánt új események meghatározásához.</span><span class="sxs-lookup"><span data-stu-id="8da90-133">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="8da90-134">A partner Center által támogatott webhook-események teljes listáját a következő témakörben talál: a [partner Center webhook eseményei](partner-center-webhook-events.md).</span><span class="sxs-lookup"><span data-stu-id="8da90-134">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8da90-135">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8da90-135">Prerequisites</span></span>

- <span data-ttu-id="8da90-136">A [partner Center-hitelesítésben](partner-center-authentication.md)leírt hitelesítő adatok.</span><span class="sxs-lookup"><span data-stu-id="8da90-136">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8da90-137">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az alkalmazás + felhasználó hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="8da90-137">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="8da90-138">Események fogadása a partner központtól</span><span class="sxs-lookup"><span data-stu-id="8da90-138">Receiving events from Partner Center</span></span>

<span data-ttu-id="8da90-139">A partner Centertől érkező események fogadásához közzé kell tenni egy nyilvánosan elérhető végpontot.</span><span class="sxs-lookup"><span data-stu-id="8da90-139">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="8da90-140">Mivel ez a végpont elérhető, ellenőriznie kell, hogy a kommunikáció a partner központból származik-e.</span><span class="sxs-lookup"><span data-stu-id="8da90-140">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="8da90-141">A kapott webhook-események digitális aláírása a Microsoft gyökeréhez tartozó tanúsítvánnyal történik.</span><span class="sxs-lookup"><span data-stu-id="8da90-141">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="8da90-142">A rendszer az esemény aláírásához használt tanúsítványra mutató hivatkozást is biztosít.</span><span class="sxs-lookup"><span data-stu-id="8da90-142">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="8da90-143">Ez lehetővé teszi a tanúsítvány megújítását anélkül, hogy újból üzembe kellene helyeznie vagy konfigurálnia kell a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="8da90-143">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="8da90-144">A partner Center 10 kísérletet tesz az esemény kézbesítésére.</span><span class="sxs-lookup"><span data-stu-id="8da90-144">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="8da90-145">Ha az esemény még nem érkezik meg 10 próbálkozás után, akkor a rendszer egy offline várólistába helyezi, és nem hajt végre további kísérleteket a kézbesítéskor.</span><span class="sxs-lookup"><span data-stu-id="8da90-145">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="8da90-146">Az alábbi példa egy, a partner Centerből közzétett eseményt mutat be.</span><span class="sxs-lookup"><span data-stu-id="8da90-146">The following sample shows an event posted from Partner Center.</span></span>

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

>[!NOTE]
><span data-ttu-id="8da90-147">Az engedélyezési fejléc "Signature" sémával rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="8da90-147">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="8da90-148">Ez a tartalom Base64 kódolású aláírása.</span><span class="sxs-lookup"><span data-stu-id="8da90-148">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="8da90-149">A visszahívás hitelesítése</span><span class="sxs-lookup"><span data-stu-id="8da90-149">How to authenticate the callback</span></span>

<span data-ttu-id="8da90-150">A partner Centertől kapott visszahívási esemény hitelesítéséhez kövesse az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="8da90-150">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="8da90-151">Ellenőrizze, hogy jelen vannak-e a szükséges fejlécek (Engedélyezés, x-MS-Certificate-URL, x-MS-Signature-algoritmus).</span><span class="sxs-lookup"><span data-stu-id="8da90-151">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="8da90-152">Töltse le a tartalom aláírásához használt tanúsítványt (x-MS-Certificate-URL).</span><span class="sxs-lookup"><span data-stu-id="8da90-152">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="8da90-153">Ellenőrizze a tanúsítványlánc utasításait.</span><span class="sxs-lookup"><span data-stu-id="8da90-153">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="8da90-154">Ellenőrizze a tanúsítvány "szervezetét".</span><span class="sxs-lookup"><span data-stu-id="8da90-154">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="8da90-155">Az UTF8 kódolású tartalom beolvasása pufferbe.</span><span class="sxs-lookup"><span data-stu-id="8da90-155">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="8da90-156">Hozzon létre egy RSA titkosítási szolgáltatót.</span><span class="sxs-lookup"><span data-stu-id="8da90-156">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="8da90-157">Győződjön meg arról, hogy a megadott kivonatoló algoritmussal (például SHA256) aláírt adatértékek megfelelnek-e.</span><span class="sxs-lookup"><span data-stu-id="8da90-157">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="8da90-158">Ha az ellenőrzés sikeres, dolgozza fel az üzenetet.</span><span class="sxs-lookup"><span data-stu-id="8da90-158">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="8da90-159">Alapértelmezés szerint az aláírási jogkivonat egy engedélyezési fejlécben lesz elküldve.</span><span class="sxs-lookup"><span data-stu-id="8da90-159">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="8da90-160">Ha a **SignatureTokenToMsSignatureHeader** értéke TRUE (igaz) értékre van állítva a regisztrációban, az aláírási tokent az x-MS-Signature fejlécben küldi el a rendszer.</span><span class="sxs-lookup"><span data-stu-id="8da90-160">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="8da90-161">Eseményvezérelt modell</span><span class="sxs-lookup"><span data-stu-id="8da90-161">Event model</span></span>

<span data-ttu-id="8da90-162">A következő táblázat a partneri központ eseményeinek tulajdonságait ismerteti.</span><span class="sxs-lookup"><span data-stu-id="8da90-162">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="8da90-163">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="8da90-163">Properties</span></span>

| <span data-ttu-id="8da90-164">Név</span><span class="sxs-lookup"><span data-stu-id="8da90-164">Name</span></span>                      | <span data-ttu-id="8da90-165">Leírás</span><span class="sxs-lookup"><span data-stu-id="8da90-165">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="8da90-166">**EventName**</span><span class="sxs-lookup"><span data-stu-id="8da90-166">**EventName**</span></span>             | <span data-ttu-id="8da90-167">Az esemény neve.</span><span class="sxs-lookup"><span data-stu-id="8da90-167">The name of the event.</span></span> <span data-ttu-id="8da90-168">A (z) {Resource} – {Action} formátumban.</span><span class="sxs-lookup"><span data-stu-id="8da90-168">In the form {resource}-{action}.</span></span> <span data-ttu-id="8da90-169">Például: "test-created".</span><span class="sxs-lookup"><span data-stu-id="8da90-169">For example, "test-created".</span></span>  |
| <span data-ttu-id="8da90-170">**ResourceUri**</span><span class="sxs-lookup"><span data-stu-id="8da90-170">**ResourceUri**</span></span>           | <span data-ttu-id="8da90-171">A módosult erőforrás URI-ja.</span><span class="sxs-lookup"><span data-stu-id="8da90-171">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="8da90-172">**ResourceName**</span><span class="sxs-lookup"><span data-stu-id="8da90-172">**ResourceName**</span></span>          | <span data-ttu-id="8da90-173">A módosult erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="8da90-173">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="8da90-174">**AuditUrl**</span><span class="sxs-lookup"><span data-stu-id="8da90-174">**AuditUrl**</span></span>              | <span data-ttu-id="8da90-175">Választható.</span><span class="sxs-lookup"><span data-stu-id="8da90-175">Optional.</span></span> <span data-ttu-id="8da90-176">A naplózási rekord URI-ja.</span><span class="sxs-lookup"><span data-stu-id="8da90-176">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="8da90-177">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="8da90-177">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="8da90-178">A dátum és az idő UTC formátumban, amikor az erőforrás megváltozása megtörtént.</span><span class="sxs-lookup"><span data-stu-id="8da90-178">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="8da90-179">Sample</span><span class="sxs-lookup"><span data-stu-id="8da90-179">Sample</span></span>

<span data-ttu-id="8da90-180">Az alábbi példa egy partner Center-esemény szerkezetét mutatja be.</span><span class="sxs-lookup"><span data-stu-id="8da90-180">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="8da90-181">Webhook API-k</span><span class="sxs-lookup"><span data-stu-id="8da90-181">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="8da90-182">Hitelesítés</span><span class="sxs-lookup"><span data-stu-id="8da90-182">Authentication</span></span>

<span data-ttu-id="8da90-183">A webhook API-kon lévő összes hívást az engedélyezési fejléc tulajdonosi jogkivonatának használatával hitelesíti a rendszer.</span><span class="sxs-lookup"><span data-stu-id="8da90-183">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="8da90-184">Hozzáférési jogkivonat beszerzése a hozzáféréshez `https://api.partnercenter.microsoft.com` .</span><span class="sxs-lookup"><span data-stu-id="8da90-184">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="8da90-185">Ez a jogkivonat ugyanaz a jogkivonat, amely a partner Center API-k további részeinek elérésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="8da90-185">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="8da90-186">Események listájának beolvasása</span><span class="sxs-lookup"><span data-stu-id="8da90-186">Get a list of events</span></span>

<span data-ttu-id="8da90-187">A webhook API-k által jelenleg támogatott események listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8da90-187">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="8da90-188">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8da90-188">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="8da90-189">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8da90-189">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="8da90-190">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8da90-190">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US

[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```

### <a name="register-to-receive-events"></a><span data-ttu-id="8da90-191">Regisztrálás az események fogadására</span><span class="sxs-lookup"><span data-stu-id="8da90-191">Register to receive events</span></span>

<span data-ttu-id="8da90-192">Regisztrálja a bérlőt a megadott események fogadásához.</span><span class="sxs-lookup"><span data-stu-id="8da90-192">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8da90-193">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8da90-193">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="8da90-194">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8da90-194">Request example</span></span>

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a><span data-ttu-id="8da90-195">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8da90-195">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="view-a-registration"></a><span data-ttu-id="8da90-196">Regisztráció megtekintése</span><span class="sxs-lookup"><span data-stu-id="8da90-196">View a registration</span></span>

<span data-ttu-id="8da90-197">Egy bérlő webhookok eseményének regisztrációját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8da90-197">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8da90-198">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8da90-198">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="8da90-199">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8da90-199">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="8da90-200">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8da90-200">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="update-an-event-registration"></a><span data-ttu-id="8da90-201">Esemény-regisztráció frissítése</span><span class="sxs-lookup"><span data-stu-id="8da90-201">Update an event registration</span></span>

<span data-ttu-id="8da90-202">Egy meglévő esemény regisztrációjának frissítése.</span><span class="sxs-lookup"><span data-stu-id="8da90-202">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8da90-203">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8da90-203">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="8da90-204">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8da90-204">Request example</span></span>

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

### <a name="response-example"></a><span data-ttu-id="8da90-205">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8da90-205">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="8da90-206">Tesztelési esemény küldése a regisztráció érvényesítéséhez</span><span class="sxs-lookup"><span data-stu-id="8da90-206">Send a test event to validate your registration</span></span>

<span data-ttu-id="8da90-207">Tesztelési eseményt hoz létre a webhookok regisztrálásának ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="8da90-207">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="8da90-208">Ez a teszt arra szolgál, hogy ellenőrizze, hogy tud-e eseményeket fogadni a partner központból.</span><span class="sxs-lookup"><span data-stu-id="8da90-208">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="8da90-209">Az események adatai a kezdeti esemény létrehozása után hét nappal törlődnek.</span><span class="sxs-lookup"><span data-stu-id="8da90-209">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="8da90-210">Az érvényesítési esemény elküldése előtt regisztrálnia kell a "test-created" eseményhez a regisztrációs API használatával.</span><span class="sxs-lookup"><span data-stu-id="8da90-210">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="8da90-211">Egy érvényesítési esemény közzétételekor percenként 2 kérelem van.</span><span class="sxs-lookup"><span data-stu-id="8da90-211">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8da90-212">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8da90-212">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="8da90-213">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8da90-213">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="8da90-214">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8da90-214">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="8da90-215">Az esemény kézbesítésének ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="8da90-215">Verify that the event was delivered</span></span>

<span data-ttu-id="8da90-216">Az érvényesítési esemény aktuális állapotát adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8da90-216">Returns the current state of the validation event.</span></span> <span data-ttu-id="8da90-217">Ez az ellenőrzés hasznos lehet az esemény-kézbesítési problémák elhárításához.</span><span class="sxs-lookup"><span data-stu-id="8da90-217">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="8da90-218">A válasz az esemény továbbítására tett összes kísérlet eredményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="8da90-218">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8da90-219">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8da90-219">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="8da90-220">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8da90-220">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="8da90-221">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8da90-221">Response example</span></span>

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```

## <a name="example-for-signature-validation"></a><span data-ttu-id="8da90-222">Példa aláírás-ellenőrzésre</span><span class="sxs-lookup"><span data-stu-id="8da90-222">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="8da90-223">Minta visszahívási vezérlő aláírása (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8da90-223">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="8da90-224">Aláírás ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="8da90-224">Signature Validation</span></span>

<span data-ttu-id="8da90-225">Az alábbi példa bemutatja, hogyan adhat hozzá olyan engedélyezési attribútumot a vezérlőhöz, amely fogadja a webhook eseményeinek visszahívásait.</span><span class="sxs-lookup"><span data-stu-id="8da90-225">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // for example RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
