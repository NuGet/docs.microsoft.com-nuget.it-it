---
title: Il modello di URL abuso, NuGet API di report
description: Modello di URL del report abuso consente ai client di visualizzare un collegamento nell'interfaccia utente di loro.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="6f180-103">Modello di URL di report abusi</span><span class="sxs-lookup"><span data-stu-id="6f180-103">Report abuse URL template</span></span>

<span data-ttu-id="6f180-104">È possibile che un client generare un URL che può essere utilizzato dall'utente per segnalare abusi su un pacchetto specifico.</span><span class="sxs-lookup"><span data-stu-id="6f180-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="6f180-105">Ciò è utile quando si desidera abilitare tutte le esperienze di client (parte 3 anche) delegare abuso report all'origine del pacchetto un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6f180-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="6f180-106">La risorsa utilizzata per il recupero di contenuto del pacchetto è il `ReportAbuseUriTemplate` risorse, vedere il [indice servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6f180-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6f180-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="6f180-107">Versioning</span></span>

<span data-ttu-id="6f180-108">Nell'esempio `@type` vengono utilizzati i valori:</span><span class="sxs-lookup"><span data-stu-id="6f180-108">The following `@type` values are used:</span></span>

<span data-ttu-id="6f180-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="6f180-109">@type value</span></span>                       | <span data-ttu-id="6f180-110">Note</span><span class="sxs-lookup"><span data-stu-id="6f180-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="6f180-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="6f180-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="6f180-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="6f180-112">The initial release</span></span>
<span data-ttu-id="6f180-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="6f180-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="6f180-114">Alias di `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="6f180-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="6f180-115">Modello di URL</span><span class="sxs-lookup"><span data-stu-id="6f180-115">URL template</span></span>

<span data-ttu-id="6f180-116">L'URL per l'API seguente è il valore di `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.</span><span class="sxs-lookup"><span data-stu-id="6f180-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6f180-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="6f180-117">HTTP methods</span></span>

<span data-ttu-id="6f180-118">Anche se il client non può effettuare richieste all'URL di abuso del report per conto dell'utente, la pagina web deve supportare il `GET` metodo per consentire a un URL da aprire facilmente in un web browser si fa clic.</span><span class="sxs-lookup"><span data-stu-id="6f180-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="6f180-119">Costruire l'URL</span><span class="sxs-lookup"><span data-stu-id="6f180-119">Construct the URL</span></span>

<span data-ttu-id="6f180-120">Dato un ID pacchetto noti e una versione, l'implementazione del client può costruire un URL utilizzato per accedere a un'interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="6f180-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="6f180-121">L'implementazione del client deve essere visualizzato questo URL costruito (o un collegamento ipertestuale) all'utente consentendo di aprire un web browser all'URL e qualsiasi relazione abuso necessarie.</span><span class="sxs-lookup"><span data-stu-id="6f180-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="6f180-122">L'implementazione del modulo report abuso viene determinata dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="6f180-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="6f180-123">Il valore di `@id` è una stringa URL contenente uno dei token di segnaposto seguente:</span><span class="sxs-lookup"><span data-stu-id="6f180-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="6f180-124">Segnaposto URL</span><span class="sxs-lookup"><span data-stu-id="6f180-124">URL placeholders</span></span>

<span data-ttu-id="6f180-125">nome</span><span class="sxs-lookup"><span data-stu-id="6f180-125">Name</span></span>        | <span data-ttu-id="6f180-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="6f180-126">Type</span></span>    | <span data-ttu-id="6f180-127">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="6f180-127">Required</span></span> | <span data-ttu-id="6f180-128">Note</span><span class="sxs-lookup"><span data-stu-id="6f180-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="6f180-129">stringa</span><span class="sxs-lookup"><span data-stu-id="6f180-129">string</span></span>  | <span data-ttu-id="6f180-130">No</span><span class="sxs-lookup"><span data-stu-id="6f180-130">no</span></span>       | <span data-ttu-id="6f180-131">L'ID del pacchetto per segnalare abusi per</span><span class="sxs-lookup"><span data-stu-id="6f180-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="6f180-132">stringa</span><span class="sxs-lookup"><span data-stu-id="6f180-132">string</span></span>  | <span data-ttu-id="6f180-133">No</span><span class="sxs-lookup"><span data-stu-id="6f180-133">no</span></span>       | <span data-ttu-id="6f180-134">La versione del pacchetto per segnalare abusi per</span><span class="sxs-lookup"><span data-stu-id="6f180-134">The package version to report abuse for</span></span>

<span data-ttu-id="6f180-135">Il `{id}` e `{version}` valori dall'implementazione del server devono essere fatta distinzione tra maiuscole e minuscole e non sensibili se la versione è normalizzato.</span><span class="sxs-lookup"><span data-stu-id="6f180-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="6f180-136">Ad esempio, modello di abuso di nuget.org report simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="6f180-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="6f180-137">Se l'implementazione del client deve visualizzare un collegamento al modulo di abuso del report per NuGet.Versioning 4.3.0, verrebbe generato l'URL seguente e che sia disponibile per l'utente:</span><span class="sxs-lookup"><span data-stu-id="6f180-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
