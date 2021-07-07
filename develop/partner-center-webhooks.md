---
title: Partnerközpont – webhookok
description: A webhookokkal a partnerek regisztrálnak az erőforrás-módosítási eseményekre.
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 74d5981436ba29ea4f6f93a5693ec6da82777eb4
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547749"
---
# <a name="partner-center-webhooks"></a><span data-ttu-id="8b93f-103">Partnerközpont – webhookok</span><span class="sxs-lookup"><span data-stu-id="8b93f-103">Partner Center webhooks</span></span>

<span data-ttu-id="8b93f-104">**A következőkre vonatkozik:** Partnerközpont | Partnerközpont 21Vianet | Partnerközpont Microsoft Cloud Germany | Partnerközpont a Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8b93f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8b93f-105">A Partnerközpont Webhook API-k lehetővé teszik a partnerek számára az erőforrás-változási eseményekre való regisztrációt.</span><span class="sxs-lookup"><span data-stu-id="8b93f-105">The Partner Center Webhook APIs allow partners to register for resource change events.</span></span> <span data-ttu-id="8b93f-106">Ezeket az eseményeket HTTP POS-ként kézbesíti a rendszer a partner regisztrált URL-címére.</span><span class="sxs-lookup"><span data-stu-id="8b93f-106">These events are delivered in the form of HTTP POSTs to the partner's registered URL.</span></span> <span data-ttu-id="8b93f-107">Ahhoz, hogy a partnerek eseményt Partnerközpont fogadnak, visszahívási eseményt fognak fogadni, Partnerközpont postán közzétenik az erőforrás-módosítási eseményt.</span><span class="sxs-lookup"><span data-stu-id="8b93f-107">To receive an event from Partner Center, partners will host a callback where Partner Center can POST the resource change event.</span></span> <span data-ttu-id="8b93f-108">Az esemény digitálisan lesz aláírva, hogy a partner ellenőrizni tudja, hogy a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="8b93f-108">The event will be digitally signed so that the partner can verify that it was sent from Partner Center.</span></span>

<span data-ttu-id="8b93f-109">A partnerek az alábbi példákhoz hasonló webhookesemények közül választhatnak, amelyet a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="8b93f-109">Partners can select from Webhook events, like the following examples, that are supported by Partner Center.</span></span>

- <span data-ttu-id="8b93f-110">**Tesztesemény ("test-created")**</span><span class="sxs-lookup"><span data-stu-id="8b93f-110">**Test Event ("test-created")**</span></span>

    <span data-ttu-id="8b93f-111">Ez az esemény lehetővé teszi, hogy önkiszolgálóan regisztrálja és tesztelje a regisztrációt egy tesztesemény lekért kérésével, majd nyomon követi a folyamat előrehaladását.</span><span class="sxs-lookup"><span data-stu-id="8b93f-111">This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress.</span></span> <span data-ttu-id="8b93f-112">Láthatja a Microsofttól az esemény kézbesítése közben kapott hibaüzeneteket.</span><span class="sxs-lookup"><span data-stu-id="8b93f-112">You can see the failure messages that are being received from Microsoft while trying to deliver the event.</span></span> <span data-ttu-id="8b93f-113">Ez a korlátozás csak a "teszt által létrehozott" eseményekre vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="8b93f-113">This restriction only applies to "test-created" events.</span></span> <span data-ttu-id="8b93f-114">A hét napnál régebbi adatok el lesznek ürülve.</span><span class="sxs-lookup"><span data-stu-id="8b93f-114">Data older than seven days will be purged.</span></span>

- <span data-ttu-id="8b93f-115">**Előfizetés-frissített esemény ("subscription-updated")**</span><span class="sxs-lookup"><span data-stu-id="8b93f-115">**Subscription Updated Event ("subscription-updated")**</span></span>

    <span data-ttu-id="8b93f-116">Ez az esemény akkor történik, amikor az előfizetés megváltozik.</span><span class="sxs-lookup"><span data-stu-id="8b93f-116">This event is raised when the subscription changes.</span></span> <span data-ttu-id="8b93f-117">Ezek az események akkor jönnek létre, ha belső változás történik azon felül, hogy a módosítások a Partnerközpont API-n keresztül történnek.</span><span class="sxs-lookup"><span data-stu-id="8b93f-117">These events will be generated when there is an internal change in addition to when changes are made through the Partner Center API.</span></span>

    >[!NOTE]
    ><span data-ttu-id="8b93f-118">Akár 48 órás késés is lehet az előfizetés változásának és az Előfizetés frissítése esemény aktiválásának ideje között.</span><span class="sxs-lookup"><span data-stu-id="8b93f-118">There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.</span></span>

- <span data-ttu-id="8b93f-119">**Küszöbérték túllépve esemény ("usagerecords-thresholdExceeded")**</span><span class="sxs-lookup"><span data-stu-id="8b93f-119">**Threshold Exceeded Event ("usagerecords-thresholdExceeded")**</span></span>

    <span data-ttu-id="8b93f-120">Ez az esemény akkor lép fel, ha Microsoft Azure felhasználó használati költségének összege meghaladja a használati költség költségvetését (a küszöbértéküket).</span><span class="sxs-lookup"><span data-stu-id="8b93f-120">This event is raised when the amount of Microsoft Azure usage for any customer exceeds their usage spending budget (their threshold).</span></span> <span data-ttu-id="8b93f-121">További információ: [Azure-költségvetés beállítása az ügyfelek számára/partner-központ/set-an-azure-spending-budget-for-your-customers).</span><span class="sxs-lookup"><span data-stu-id="8b93f-121">For more information, see  [Set an Azure spending budget for your customers/partner-center/set-an-azure-spending-budget-for-your-customers).</span></span>

- <span data-ttu-id="8b93f-122">**Ajánlás által létrehozott esemény ("referral-created")**</span><span class="sxs-lookup"><span data-stu-id="8b93f-122">**Referral Created Event ("referral-created")**</span></span>

    <span data-ttu-id="8b93f-123">Ez az esemény a hivatkozás létrehozásakor jön létre.</span><span class="sxs-lookup"><span data-stu-id="8b93f-123">This event is raised when the referral is created.</span></span>

- <span data-ttu-id="8b93f-124">**A hivatkozó frissített eseménye ("referral-updated")**</span><span class="sxs-lookup"><span data-stu-id="8b93f-124">**Referral Updated Event ("referral-updated")**</span></span>

    <span data-ttu-id="8b93f-125">Ez az esemény a hivatkozás frissítésekor történik.</span><span class="sxs-lookup"><span data-stu-id="8b93f-125">This event is raised when the referral is updated.</span></span>

- <span data-ttu-id="8b93f-126">**Számla kész esemény ("számla kész")**</span><span class="sxs-lookup"><span data-stu-id="8b93f-126">**Invoice Ready Event ("invoice-ready")**</span></span>

    <span data-ttu-id="8b93f-127">Ez az esemény akkor történik, amikor az új számla elkészült.</span><span class="sxs-lookup"><span data-stu-id="8b93f-127">This event is raised when the new invoice is ready.</span></span>

<span data-ttu-id="8b93f-128">A jövőben webhookesemények lesznek hozzáadva az olyan erőforrásokhoz, amelyek megváltoznak a rendszerben, és amelyek nem a partner ellenőrzése alatt áll, és további frissítéseket is el kell látni, hogy ezek az események a lehető legközelebb legyenek a "valós időhöz".</span><span class="sxs-lookup"><span data-stu-id="8b93f-128">Future Webhook events will be added for resources that change in the system that the partner isn't in control of, and further updates will be made to get those events as close to "real time" as possible.</span></span> <span data-ttu-id="8b93f-129">A partnerektől származó visszajelzések, amelyek miatt az események értéket képviselnek a vállalatuk számára, hasznosak lehetnek annak meghatározásában, hogy milyen új eseményeket kell hozzáadniuk.</span><span class="sxs-lookup"><span data-stu-id="8b93f-129">Feedback from Partners on which events add value to their business will be useful in determining what new events to add.</span></span>

<span data-ttu-id="8b93f-130">A webhookesemények által támogatott webhookesemények teljes listájáért tekintse meg Partnerközpont [webhookesemények Partnerközpont listáját.](partner-center-webhook-events.md)</span><span class="sxs-lookup"><span data-stu-id="8b93f-130">For a complete list of Webhook events supported by Partner Center, see [Partner Center webhook events](partner-center-webhook-events.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b93f-131">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="8b93f-131">Prerequisites</span></span>

- <span data-ttu-id="8b93f-132">Az Partnerközpont [ismertetett hitelesítő adatok.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8b93f-132">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8b93f-133">Ez a forgatókönyv támogatja a hitelesítést az önálló alkalmazással és az App+User hitelesítő adatokkal.</span><span class="sxs-lookup"><span data-stu-id="8b93f-133">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="receiving-events-from-partner-center"></a><span data-ttu-id="8b93f-134">Események fogadása a Partnerközpont</span><span class="sxs-lookup"><span data-stu-id="8b93f-134">Receiving events from Partner Center</span></span>

<span data-ttu-id="8b93f-135">Ahhoz, hogy eseményeket fogad Partnerközpont egy nyilvánosan elérhető végpontot kell elérhetővé tenni.</span><span class="sxs-lookup"><span data-stu-id="8b93f-135">To receive events from Partner Center, you must expose a publicly accessible endpoint.</span></span> <span data-ttu-id="8b93f-136">Mivel ez a végpont elérhető, ellenőriznie kell, hogy a kommunikáció a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="8b93f-136">Because this endpoint is exposed, you must validate that the communication is from Partner Center.</span></span> <span data-ttu-id="8b93f-137">Minden kapott webhookesemény digitálisan alá van írva egy tanúsítvánnyal, amely a Microsoft-gyökérhez van láncolva.</span><span class="sxs-lookup"><span data-stu-id="8b93f-137">All Webhook events that you receive are digitally signed with a certificate that chains to the Microsoft Root.</span></span> <span data-ttu-id="8b93f-138">A szolgáltatás az esemény aláíráshoz használt tanúsítványra mutató hivatkozást is biztosít.</span><span class="sxs-lookup"><span data-stu-id="8b93f-138">A link to the certificate used to sign the event will also be provided.</span></span> <span data-ttu-id="8b93f-139">Ez lehetővé teszi a tanúsítvány megújítását anélkül, hogy újra üzembe kellene állítania vagy újra kellene konfigurálnia a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="8b93f-139">This will allow the certificate to be renewed without you having to redeploy or reconfigure your service.</span></span> <span data-ttu-id="8b93f-140">Partnerközpont 10 kísérletet tesz az esemény kézbesítésére.</span><span class="sxs-lookup"><span data-stu-id="8b93f-140">Partner Center will make 10 attempts to deliver the event.</span></span> <span data-ttu-id="8b93f-141">Ha az esemény 10 próbálkozás után sem lesz kézbesítve, akkor az offline üzenetsorba kerül, és a kézbesítéskor nem történik további kísérlet.</span><span class="sxs-lookup"><span data-stu-id="8b93f-141">If the event is still not delivered after 10 attempts, it will be moved into an offline queue and no further attempts will be made at delivery.</span></span>

<span data-ttu-id="8b93f-142">Az alábbi példa egy, a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="8b93f-142">The following sample shows an event posted from Partner Center.</span></span>

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
><span data-ttu-id="8b93f-143">Az Authorization fejléc "Signature" sémával rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="8b93f-143">The Authorization header has a scheme of "Signature".</span></span> <span data-ttu-id="8b93f-144">Ez a tartalom base64 kódolású aláírása.</span><span class="sxs-lookup"><span data-stu-id="8b93f-144">This is a base64 encoded signature of the content.</span></span>

## <a name="how-to-authenticate-the-callback"></a><span data-ttu-id="8b93f-145">A visszahívás hitelesítése</span><span class="sxs-lookup"><span data-stu-id="8b93f-145">How to authenticate the callback</span></span>

<span data-ttu-id="8b93f-146">A következő lépésekkel hitelesítheti a Partnerközpont visszahívási eseményt:</span><span class="sxs-lookup"><span data-stu-id="8b93f-146">To authenticate the callback event received from Partner Center, follow these steps:</span></span>

1. <span data-ttu-id="8b93f-147">Ellenőrizze, hogy a szükséges fejlécek jelen vannak-e (Engedélyezés, x-ms-certificate-url, x-ms-signature-algorithm).</span><span class="sxs-lookup"><span data-stu-id="8b93f-147">Verify the required headers are present (Authorization, x-ms-certificate-url, x-ms-signature-algorithm).</span></span>

2. <span data-ttu-id="8b93f-148">Töltse le a tartalom aláíráshoz használt tanúsítványt (x-ms-certificate-url).</span><span class="sxs-lookup"><span data-stu-id="8b93f-148">Download the certificate used to sign the content (x-ms-certificate-url).</span></span>

3. <span data-ttu-id="8b93f-149">Ellenőrizze a tanúsítványláncot.</span><span class="sxs-lookup"><span data-stu-id="8b93f-149">Verify the Certificate Chain.</span></span>

4. <span data-ttu-id="8b93f-150">Ellenőrizze a tanúsítvány "Szervezet" tanúsítványát.</span><span class="sxs-lookup"><span data-stu-id="8b93f-150">Verify the "Organization" of the certificate.</span></span>

5. <span data-ttu-id="8b93f-151">Olvassa be a tartalmat UTF8-kódolással egy pufferbe.</span><span class="sxs-lookup"><span data-stu-id="8b93f-151">Read the content with UTF8 encoding into a buffer.</span></span>

6. <span data-ttu-id="8b93f-152">RSA titkosítási szolgáltató létrehozása.</span><span class="sxs-lookup"><span data-stu-id="8b93f-152">Create an RSA Crypto Provider.</span></span>

7. <span data-ttu-id="8b93f-153">Ellenőrizze, hogy az adatok megegyeznek-e a megadott kivonatolási algoritmussal aláírt adatokkal (például SHA256).</span><span class="sxs-lookup"><span data-stu-id="8b93f-153">Verify the data matches what was signed with the specified hash algorithm (for example SHA256).</span></span>

8. <span data-ttu-id="8b93f-154">Ha az ellenőrzés sikeres, az üzenet feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="8b93f-154">If the verification succeeds, process the message.</span></span>

> [!NOTE]
> <span data-ttu-id="8b93f-155">Alapértelmezés szerint az aláírási jogkivonat egy Authorization fejlécben lesz elküldve.</span><span class="sxs-lookup"><span data-stu-id="8b93f-155">By default, the signature token will be sent in an Authorization header.</span></span> <span data-ttu-id="8b93f-156">Ha a regisztrációban a **SignatureTokenToMsSignatureHeader** true (igaz) értékre van állítva, az aláírási jogkivonat ehelyett az x-ms-signature fejlécben lesz elküldve.</span><span class="sxs-lookup"><span data-stu-id="8b93f-156">If you set **SignatureTokenToMsSignatureHeader** to true in your registration, the signature token will be sent in the x-ms-signature header instead.</span></span>

## <a name="event-model"></a><span data-ttu-id="8b93f-157">Eseménymodell</span><span class="sxs-lookup"><span data-stu-id="8b93f-157">Event model</span></span>

<span data-ttu-id="8b93f-158">Az alábbi táblázat egy esemény Partnerközpont ismerteti.</span><span class="sxs-lookup"><span data-stu-id="8b93f-158">The following table describes the properties of a Partner Center event.</span></span>

### <a name="properties"></a><span data-ttu-id="8b93f-159">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="8b93f-159">Properties</span></span>

| <span data-ttu-id="8b93f-160">Név</span><span class="sxs-lookup"><span data-stu-id="8b93f-160">Name</span></span>                      | <span data-ttu-id="8b93f-161">Leírás</span><span class="sxs-lookup"><span data-stu-id="8b93f-161">Description</span></span>                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="8b93f-162">**EventName**</span><span class="sxs-lookup"><span data-stu-id="8b93f-162">**EventName**</span></span>             | <span data-ttu-id="8b93f-163">Az esemény neve.</span><span class="sxs-lookup"><span data-stu-id="8b93f-163">The name of the event.</span></span> <span data-ttu-id="8b93f-164">A következő űrlapon: {resource}-{action}.</span><span class="sxs-lookup"><span data-stu-id="8b93f-164">In the form {resource}-{action}.</span></span> <span data-ttu-id="8b93f-165">Például: "test-created".</span><span class="sxs-lookup"><span data-stu-id="8b93f-165">For example, "test-created".</span></span>  |
| <span data-ttu-id="8b93f-166">**ResourceUri (Erőforrás-azonosító)**</span><span class="sxs-lookup"><span data-stu-id="8b93f-166">**ResourceUri**</span></span>           | <span data-ttu-id="8b93f-167">A módosított erőforrás URI-ját.</span><span class="sxs-lookup"><span data-stu-id="8b93f-167">The URI of the resource that changed.</span></span>                                                 |
| <span data-ttu-id="8b93f-168">**ResourceName (Erőforrásnév)**</span><span class="sxs-lookup"><span data-stu-id="8b93f-168">**ResourceName**</span></span>          | <span data-ttu-id="8b93f-169">A módosított erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="8b93f-169">The name of the resource that changed.</span></span>                                                |
| <span data-ttu-id="8b93f-170">**AuditUrl (Naplózásiurl)**</span><span class="sxs-lookup"><span data-stu-id="8b93f-170">**AuditUrl**</span></span>              | <span data-ttu-id="8b93f-171">Választható.</span><span class="sxs-lookup"><span data-stu-id="8b93f-171">Optional.</span></span> <span data-ttu-id="8b93f-172">A naplórekord URI-ját.</span><span class="sxs-lookup"><span data-stu-id="8b93f-172">The URI of the Audit record.</span></span>                                                |
| <span data-ttu-id="8b93f-173">**ResourceChangeUtcDate**</span><span class="sxs-lookup"><span data-stu-id="8b93f-173">**ResourceChangeUtcDate**</span></span> | <span data-ttu-id="8b93f-174">Az erőforrás változásának dátuma és időpontja (UTC formátumban).</span><span class="sxs-lookup"><span data-stu-id="8b93f-174">The date and time, in UTC format, when the resource change occurred.</span></span>                  |

### <a name="sample"></a><span data-ttu-id="8b93f-175">Sample</span><span class="sxs-lookup"><span data-stu-id="8b93f-175">Sample</span></span>

<span data-ttu-id="8b93f-176">Az alábbi minta egy esemény Partnerközpont mutatja be.</span><span class="sxs-lookup"><span data-stu-id="8b93f-176">The following sample shows the structure of a Partner Center event.</span></span>

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

## <a name="webhook-apis"></a><span data-ttu-id="8b93f-177">Webhook API-k</span><span class="sxs-lookup"><span data-stu-id="8b93f-177">Webhook APIs</span></span>

### <a name="authentication"></a><span data-ttu-id="8b93f-178">Hitelesítés</span><span class="sxs-lookup"><span data-stu-id="8b93f-178">Authentication</span></span>

<span data-ttu-id="8b93f-179">A webhook API-k hívásait az engedélyezési fejlécben található Bearer token hitelesíti.</span><span class="sxs-lookup"><span data-stu-id="8b93f-179">All calls to the Webhook APIs are authenticated using the Bearer token in the Authorization Header.</span></span> <span data-ttu-id="8b93f-180">Szerezzen be egy hozzáférési jogkivonatot a `https://api.partnercenter.microsoft.com` hozzáféréshez.</span><span class="sxs-lookup"><span data-stu-id="8b93f-180">Acquire an access token to access `https://api.partnercenter.microsoft.com`.</span></span> <span data-ttu-id="8b93f-181">Ez a jogkivonat ugyanaz a jogkivonat, amely a többi api-hoz való Partnerközpont használ.</span><span class="sxs-lookup"><span data-stu-id="8b93f-181">This token is the same token that is used to access the rest of the Partner Center APIs.</span></span>

### <a name="get-a-list-of-events"></a><span data-ttu-id="8b93f-182">Események listájának lekért listája</span><span class="sxs-lookup"><span data-stu-id="8b93f-182">Get a list of events</span></span>

<span data-ttu-id="8b93f-183">A webhook API-k által jelenleg támogatott események listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8b93f-183">Returns a list of the events that are currently supported by the Webhook APIs.</span></span>

### <a name="resource-url"></a><span data-ttu-id="8b93f-184">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8b93f-184">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/events`

### <a name="request-example"></a><span data-ttu-id="8b93f-185">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8b93f-185">Request example</span></span>

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

### <a name="response-example"></a><span data-ttu-id="8b93f-186">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8b93f-186">Response example</span></span>

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

### <a name="register-to-receive-events"></a><span data-ttu-id="8b93f-187">Regisztrálás események fogadására</span><span class="sxs-lookup"><span data-stu-id="8b93f-187">Register to receive events</span></span>

<span data-ttu-id="8b93f-188">Regisztrál egy bérlőt a megadott események fogadására.</span><span class="sxs-lookup"><span data-stu-id="8b93f-188">Registers a tenant to receive the specified events.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8b93f-189">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8b93f-189">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="8b93f-190">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8b93f-190">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="8b93f-191">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8b93f-191">Response example</span></span>

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

### <a name="view-a-registration"></a><span data-ttu-id="8b93f-192">Regisztráció megtekintése</span><span class="sxs-lookup"><span data-stu-id="8b93f-192">View a registration</span></span>

<span data-ttu-id="8b93f-193">Egy bérlő webhook eseményregisztrációját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8b93f-193">Returns the Webhooks event registration for a tenant.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8b93f-194">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8b93f-194">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="8b93f-195">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8b93f-195">Request example</span></span>

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="8b93f-196">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8b93f-196">Response example</span></span>

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

### <a name="update-an-event-registration"></a><span data-ttu-id="8b93f-197">Eseményregisztráció frissítése</span><span class="sxs-lookup"><span data-stu-id="8b93f-197">Update an event registration</span></span>

<span data-ttu-id="8b93f-198">Frissíti a meglévő eseményregisztrációt.</span><span class="sxs-lookup"><span data-stu-id="8b93f-198">Updates an existing event registration.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8b93f-199">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8b93f-199">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration`

### <a name="request-example"></a><span data-ttu-id="8b93f-200">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8b93f-200">Request example</span></span>

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

### <a name="response-example"></a><span data-ttu-id="8b93f-201">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8b93f-201">Response example</span></span>

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

### <a name="send-a-test-event-to-validate-your-registration"></a><span data-ttu-id="8b93f-202">Tesztesemény küldése a regisztráció érvényesítéséhez</span><span class="sxs-lookup"><span data-stu-id="8b93f-202">Send a test event to validate your registration</span></span>

<span data-ttu-id="8b93f-203">Létrehoz egy teszteseményt a webhookok regisztrációja érvényesítéséhez.</span><span class="sxs-lookup"><span data-stu-id="8b93f-203">Generates a test event to validate the Webhooks registration.</span></span> <span data-ttu-id="8b93f-204">A teszt célja annak ellenőrzése, hogy fogadhat-e eseményeket a Partnerközpont.</span><span class="sxs-lookup"><span data-stu-id="8b93f-204">This test is intended to validate that you can receive events from Partner Center.</span></span> <span data-ttu-id="8b93f-205">Ezeknek az eseményeknek az adatai hét nappal a kezdeti esemény létrehozása után törlődnek.</span><span class="sxs-lookup"><span data-stu-id="8b93f-205">Data for these events will be deleted seven days after the initial event is created.</span></span> <span data-ttu-id="8b93f-206">Érvényesítési esemény küldése előtt regisztrálnia kell a "test-created" eseményre a regisztrációs API-val.</span><span class="sxs-lookup"><span data-stu-id="8b93f-206">You must be registered for the "test-created" event, using the registration API, before sending a validation event.</span></span>

>[!NOTE]
><span data-ttu-id="8b93f-207">Érvényesítési esemény közzétételével percenként 2 kérelem van korlátozva.</span><span class="sxs-lookup"><span data-stu-id="8b93f-207">There is a throttle limit of 2 requests per minute when posting a validation event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8b93f-208">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8b93f-208">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents`

### <a name="request-example"></a><span data-ttu-id="8b93f-209">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8b93f-209">Request example</span></span>

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

### <a name="response-example"></a><span data-ttu-id="8b93f-210">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8b93f-210">Response example</span></span>

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

### <a name="verify-that-the-event-was-delivered"></a><span data-ttu-id="8b93f-211">Az esemény kézbesítésének ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="8b93f-211">Verify that the event was delivered</span></span>

<span data-ttu-id="8b93f-212">Az érvényesítési esemény aktuális állapotát adja vissza.</span><span class="sxs-lookup"><span data-stu-id="8b93f-212">Returns the current state of the validation event.</span></span> <span data-ttu-id="8b93f-213">Ez az ellenőrzés hasznos lehet az események kézbesítésével kapcsolatos problémák elhárításában.</span><span class="sxs-lookup"><span data-stu-id="8b93f-213">This verification can be helpful for troubleshooting event delivery issues.</span></span> <span data-ttu-id="8b93f-214">A Válasz az esemény kézbesítésére tett minden egyes kísérlet eredményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="8b93f-214">The Response contains a result for each attempt that is made to deliver the event.</span></span>

#### <a name="resource-url"></a><span data-ttu-id="8b93f-215">Erőforrás URL-címe</span><span class="sxs-lookup"><span data-stu-id="8b93f-215">Resource URL</span></span>

`https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}`

### <a name="request-example"></a><span data-ttu-id="8b93f-216">Példa kérésre</span><span class="sxs-lookup"><span data-stu-id="8b93f-216">Request example</span></span>

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

### <a name="response-example"></a><span data-ttu-id="8b93f-217">Példa válaszra</span><span class="sxs-lookup"><span data-stu-id="8b93f-217">Response example</span></span>

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

## <a name="example-for-signature-validation"></a><span data-ttu-id="8b93f-218">Példa az aláírás-ellenőrzésre</span><span class="sxs-lookup"><span data-stu-id="8b93f-218">Example for Signature Validation</span></span>

### <a name="sample-callback-controller-signature-aspnet"></a><span data-ttu-id="8b93f-219">Minta visszahívási vezérlő aláírása (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8b93f-219">Sample Callback Controller signature (ASP.NET)</span></span>

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

### <a name="signature-validation"></a><span data-ttu-id="8b93f-220">Aláírás-ellenőrzés</span><span class="sxs-lookup"><span data-stu-id="8b93f-220">Signature Validation</span></span>

<span data-ttu-id="8b93f-221">Az alábbi példa bemutatja, hogyan adhat hozzá engedélyezési attribútumot a webhookesemények visszahívásait fogadó vezérlőhöz.</span><span class="sxs-lookup"><span data-stu-id="8b93f-221">The following example shows how to add an Authorization Attribute to the controller that is receiving callbacks from Webhook events.</span></span>

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
