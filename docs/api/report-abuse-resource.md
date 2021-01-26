---
title: Modello di URL di abuso report, API NuGet
description: Il modello report abuse URL consente ai client di visualizzare un collegamento Segnala abusi nell'interfaccia utente.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775227"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="6391b-103">Modello di URL di report abusi</span><span class="sxs-lookup"><span data-stu-id="6391b-103">Report abuse URL template</span></span>

<span data-ttu-id="6391b-104">È possibile che un client crei un URL che può essere usato dall'utente per segnalare gli abusi relativi a un pacchetto specifico.</span><span class="sxs-lookup"><span data-stu-id="6391b-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="6391b-105">Questa operazione è utile quando un'origine del pacchetto vuole abilitare tutte le esperienze client (anche di terze parti) per delegare i report sugli abusi all'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6391b-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="6391b-106">La risorsa utilizzata per la compilazione di questo URL è la `ReportAbuseUriTemplate` risorsa presente nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="6391b-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6391b-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="6391b-107">Versioning</span></span>

<span data-ttu-id="6391b-108">`@type`Vengono usati i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="6391b-108">The following `@type` values are used:</span></span>

<span data-ttu-id="6391b-109">Valore della proprietà @type</span><span class="sxs-lookup"><span data-stu-id="6391b-109">@type value</span></span>                       | <span data-ttu-id="6391b-110">Note</span><span class="sxs-lookup"><span data-stu-id="6391b-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="6391b-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="6391b-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="6391b-112">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="6391b-112">The initial release</span></span>
<span data-ttu-id="6391b-113">ReportAbuseUriTemplate/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="6391b-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="6391b-114">Alias di `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="6391b-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="6391b-115">Modello di URL</span><span class="sxs-lookup"><span data-stu-id="6391b-115">URL template</span></span>

<span data-ttu-id="6391b-116">L'URL per l'API seguente è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` indicati sopra.</span><span class="sxs-lookup"><span data-stu-id="6391b-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6391b-117">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="6391b-117">HTTP methods</span></span>

<span data-ttu-id="6391b-118">Anche se il client non è destinato a eseguire richieste all'URL del report abusi per conto dell'utente, la pagina Web deve supportare il `GET` metodo per consentire l'apertura semplice di un URL selezionato in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="6391b-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="6391b-119">Costruire l'URL</span><span class="sxs-lookup"><span data-stu-id="6391b-119">Construct the URL</span></span>

<span data-ttu-id="6391b-120">Dato un ID e una versione del pacchetto noti, l'implementazione client può costruire un URL usato per accedere a un'interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="6391b-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="6391b-121">L'implementazione client deve visualizzare l'URL costruito (o collegamento selezionabile) per consentire all'utente di aprire un Web browser all'URL e di apportare eventuali segnalazioni di abusi necessarie.</span><span class="sxs-lookup"><span data-stu-id="6391b-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="6391b-122">L'implementazione del modulo report di abusi è determinata dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="6391b-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="6391b-123">Il valore di `@id` è una stringa URL che contiene i token segnaposto seguenti:</span><span class="sxs-lookup"><span data-stu-id="6391b-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="6391b-124">Segnaposto URL</span><span class="sxs-lookup"><span data-stu-id="6391b-124">URL placeholders</span></span>

<span data-ttu-id="6391b-125">Nome</span><span class="sxs-lookup"><span data-stu-id="6391b-125">Name</span></span>        | <span data-ttu-id="6391b-126">Type</span><span class="sxs-lookup"><span data-stu-id="6391b-126">Type</span></span>    | <span data-ttu-id="6391b-127">Necessario</span><span class="sxs-lookup"><span data-stu-id="6391b-127">Required</span></span> | <span data-ttu-id="6391b-128">Note</span><span class="sxs-lookup"><span data-stu-id="6391b-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="6391b-129">string</span><span class="sxs-lookup"><span data-stu-id="6391b-129">string</span></span>  | <span data-ttu-id="6391b-130">no</span><span class="sxs-lookup"><span data-stu-id="6391b-130">no</span></span>       | <span data-ttu-id="6391b-131">ID del pacchetto per segnalare gli abusi per</span><span class="sxs-lookup"><span data-stu-id="6391b-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="6391b-132">string</span><span class="sxs-lookup"><span data-stu-id="6391b-132">string</span></span>  | <span data-ttu-id="6391b-133">no</span><span class="sxs-lookup"><span data-stu-id="6391b-133">no</span></span>       | <span data-ttu-id="6391b-134">Versione del pacchetto per cui segnalare gli abusi</span><span class="sxs-lookup"><span data-stu-id="6391b-134">The package version to report abuse for</span></span>

<span data-ttu-id="6391b-135">I `{id}` `{version}` valori e interpretati dall'implementazione del server non devono fare distinzione tra maiuscole e minuscole e non sono sensibili alla normalizzazione della versione.</span><span class="sxs-lookup"><span data-stu-id="6391b-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="6391b-136">Il modello di abusi dei report di NuGet. org, ad esempio, ha un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="6391b-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="6391b-137">Se l'implementazione client deve visualizzare un collegamento al modulo segnalazione abusi per NuGet. Versioning 4.3.0, produrrebbe l'URL seguente e lo fornirà all'utente:</span><span class="sxs-lookup"><span data-stu-id="6391b-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
