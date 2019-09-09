---
title: Modello di URL dei dettagli del pacchetto, API NuGet
description: Il modello di URL dei dettagli del pacchetto consente ai client di visualizzare nell'interfaccia utente un collegamento Web a più dettagli del pacchetto
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 6657536ea6c699a834f57494c66b2a7d741dfcb7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488172"
---
# <a name="package-details-url-template"></a><span data-ttu-id="e3360-103">Modello URL Dettagli pacchetto</span><span class="sxs-lookup"><span data-stu-id="e3360-103">Package details URL template</span></span>

<span data-ttu-id="e3360-104">È possibile che un client crei un URL che può essere usato dall'utente per visualizzare altri dettagli del pacchetto nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="e3360-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="e3360-105">Questa operazione è utile quando un'origine del pacchetto desidera visualizzare informazioni aggiuntive su un pacchetto che potrebbero non rientrare nell'ambito di ciò che viene visualizzato nell'applicazione client NuGet.</span><span class="sxs-lookup"><span data-stu-id="e3360-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="e3360-106">La risorsa utilizzata per la compilazione di questo URL `PackageDetailsUriTemplate` è la risorsa presente nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="e3360-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e3360-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="e3360-107">Versioning</span></span>

<span data-ttu-id="e3360-108">Vengono usati `@type` i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3360-108">The following `@type` values are used:</span></span>

<span data-ttu-id="e3360-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="e3360-109">@type value</span></span>                     | <span data-ttu-id="e3360-110">Note</span><span class="sxs-lookup"><span data-stu-id="e3360-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="e3360-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="e3360-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="e3360-112">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="e3360-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="e3360-113">Modello URL</span><span class="sxs-lookup"><span data-stu-id="e3360-113">URL template</span></span>

<span data-ttu-id="e3360-114">L'URL per l'API seguente è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` indicati sopra.</span><span class="sxs-lookup"><span data-stu-id="e3360-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e3360-115">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="e3360-115">HTTP methods</span></span>

<span data-ttu-id="e3360-116">Anche se il client non è destinato a eseguire richieste all'URL dei dettagli del pacchetto per conto dell'utente, la pagina Web deve supportare `GET` il metodo per consentire l'apertura semplice di un URL selezionato in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="e3360-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="e3360-117">Costruire l'URL</span><span class="sxs-lookup"><span data-stu-id="e3360-117">Construct the URL</span></span>

<span data-ttu-id="e3360-118">Dato un ID e una versione del pacchetto noti, l'implementazione client può costruire un URL usato per accedere a un'interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="e3360-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="e3360-119">L'implementazione client deve visualizzare l'URL costruito (o collegamento selezionabile) per consentire all'utente di aprire un Web browser all'URL e di ottenere ulteriori informazioni sul pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e3360-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="e3360-120">Il contenuto della pagina dei dettagli del pacchetto è determinato dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="e3360-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="e3360-121">L'URL deve essere un URL assoluto e lo schema (protocollo) deve essere HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e3360-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="e3360-122">Il valore di `@id` nell'indice del servizio è una stringa URL contenente uno dei token segnaposto seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3360-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="e3360-123">Segnaposto URL</span><span class="sxs-lookup"><span data-stu-id="e3360-123">URL placeholders</span></span>

<span data-ttu-id="e3360-124">Name</span><span class="sxs-lookup"><span data-stu-id="e3360-124">Name</span></span>        | <span data-ttu-id="e3360-125">Type</span><span class="sxs-lookup"><span data-stu-id="e3360-125">Type</span></span>    | <span data-ttu-id="e3360-126">Obbligatoria</span><span class="sxs-lookup"><span data-stu-id="e3360-126">Required</span></span> | <span data-ttu-id="e3360-127">Note</span><span class="sxs-lookup"><span data-stu-id="e3360-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="e3360-128">string</span><span class="sxs-lookup"><span data-stu-id="e3360-128">string</span></span>  | <span data-ttu-id="e3360-129">no</span><span class="sxs-lookup"><span data-stu-id="e3360-129">no</span></span>       | <span data-ttu-id="e3360-130">ID del pacchetto per cui ottenere i dettagli</span><span class="sxs-lookup"><span data-stu-id="e3360-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="e3360-131">string</span><span class="sxs-lookup"><span data-stu-id="e3360-131">string</span></span>  | <span data-ttu-id="e3360-132">no</span><span class="sxs-lookup"><span data-stu-id="e3360-132">no</span></span>       | <span data-ttu-id="e3360-133">Versione del pacchetto per cui ottenere i dettagli</span><span class="sxs-lookup"><span data-stu-id="e3360-133">The package version to get details for</span></span>

<span data-ttu-id="e3360-134">Il server deve accettare `{id}` i `{version}` valori e con qualsiasi combinazione di maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="e3360-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="e3360-135">Inoltre, il server non deve essere sensibile alla [normalizzazione](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers)della versione.</span><span class="sxs-lookup"><span data-stu-id="e3360-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="e3360-136">In altre parole, il server deve accettare anche versioni non normalizzate.</span><span class="sxs-lookup"><span data-stu-id="e3360-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="e3360-137">Ad esempio, il modello di dettagli del pacchetto NuGet. org è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="e3360-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="e3360-138">Se l'implementazione client deve visualizzare un collegamento ai dettagli del pacchetto per NuGet. Versioning 4.3.0, produrrebbe l'URL seguente e lo fornirà all'utente:</span><span class="sxs-lookup"><span data-stu-id="e3360-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
