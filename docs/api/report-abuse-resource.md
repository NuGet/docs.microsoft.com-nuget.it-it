---
title: Modello di URL di report Abuse, API NuGet
description: Il modello di URL report abuse consente ai client visualizzare un collegamento nell'interfaccia utente di loro.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020440"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="905a7-103">Modello di report abuse URL</span><span class="sxs-lookup"><span data-stu-id="905a7-103">Report abuse URL template</span></span>

<span data-ttu-id="905a7-104">È possibile che un client per creare un URL che può essere utilizzato dall'utente per segnalare abusi relative a un pacchetto specifico.</span><span class="sxs-lookup"><span data-stu-id="905a7-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="905a7-105">Ciò è utile quando si vuole che il file di origine abilitare tutte le esperienze di client (anche 3rd party) delegare i report di uso improprio all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="905a7-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="905a7-106">La risorsa usata per la creazione di questo URL è il `ReportAbuseUriTemplate` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="905a7-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="905a7-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="905a7-107">Versioning</span></span>

<span data-ttu-id="905a7-108">Nell'esempio `@type` vengono utilizzati i valori:</span><span class="sxs-lookup"><span data-stu-id="905a7-108">The following `@type` values are used:</span></span>

<span data-ttu-id="905a7-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="905a7-109">@type value</span></span>                       | <span data-ttu-id="905a7-110">Note</span><span class="sxs-lookup"><span data-stu-id="905a7-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="905a7-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="905a7-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="905a7-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="905a7-112">The initial release</span></span>
<span data-ttu-id="905a7-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="905a7-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="905a7-114">Alias di `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="905a7-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="905a7-115">Modello di URL</span><span class="sxs-lookup"><span data-stu-id="905a7-115">URL template</span></span>

<span data-ttu-id="905a7-116">L'URL per l'API seguente è il valore della `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.</span><span class="sxs-lookup"><span data-stu-id="905a7-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="905a7-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="905a7-117">HTTP methods</span></span>

<span data-ttu-id="905a7-118">Anche se il client non può effettuare richieste per l'URL per segnalare abusi per conto dell'utente, la pagina web deve supportare il `GET` metodo per consentire un URL selezionato essere facilmente aperto in un web browser.</span><span class="sxs-lookup"><span data-stu-id="905a7-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="905a7-119">Creare l'URL</span><span class="sxs-lookup"><span data-stu-id="905a7-119">Construct the URL</span></span>

<span data-ttu-id="905a7-120">Dato un ID noto pacchetto e versione, l'implementazione client può creare un URL utilizzato per accedere a un'interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="905a7-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="905a7-121">L'implementazione client deve visualizzare questo URL costruito (o un collegamento selezionabile) all'utente e consente loro di aprire un web browser all'URL ed effettuare qualsiasi report abuse necessarie.</span><span class="sxs-lookup"><span data-stu-id="905a7-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="905a7-122">L'implementazione del form report abuse è determinato dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="905a7-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="905a7-123">Il valore della `@id` è una stringa URL contenente uno dei token di segnaposto seguente:</span><span class="sxs-lookup"><span data-stu-id="905a7-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="905a7-124">Segnaposto URL</span><span class="sxs-lookup"><span data-stu-id="905a7-124">URL placeholders</span></span>

<span data-ttu-id="905a7-125">nome</span><span class="sxs-lookup"><span data-stu-id="905a7-125">Name</span></span>        | <span data-ttu-id="905a7-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="905a7-126">Type</span></span>    | <span data-ttu-id="905a7-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="905a7-127">Required</span></span> | <span data-ttu-id="905a7-128">Note</span><span class="sxs-lookup"><span data-stu-id="905a7-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="905a7-129">stringa</span><span class="sxs-lookup"><span data-stu-id="905a7-129">string</span></span>  | <span data-ttu-id="905a7-130">No</span><span class="sxs-lookup"><span data-stu-id="905a7-130">no</span></span>       | <span data-ttu-id="905a7-131">L'ID del pacchetto per segnalare abusi per</span><span class="sxs-lookup"><span data-stu-id="905a7-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="905a7-132">stringa</span><span class="sxs-lookup"><span data-stu-id="905a7-132">string</span></span>  | <span data-ttu-id="905a7-133">No</span><span class="sxs-lookup"><span data-stu-id="905a7-133">no</span></span>       | <span data-ttu-id="905a7-134">La versione del pacchetto per segnalare abusi per</span><span class="sxs-lookup"><span data-stu-id="905a7-134">The package version to report abuse for</span></span>

<span data-ttu-id="905a7-135">Il `{id}` e `{version}` valori interpretato dall'implementazione del server devono essere maiuscole e minuscole e non sensibili al fatto che la versione è normalizzata.</span><span class="sxs-lookup"><span data-stu-id="905a7-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="905a7-136">Ad esempio, modello di uso improprio del report di nuget.org aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="905a7-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="905a7-137">Se l'implementazione client deve visualizzare un collegamento al modulo di uso improprio del report per NuGet.Versioning 4.3.0, verrebbe generato l'URL seguente e offrirlo all'utente:</span><span class="sxs-lookup"><span data-stu-id="905a7-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
