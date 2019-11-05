---
title: Modello di URL dei dettagli del pacchetto, API NuGet
description: Il modello di URL dei dettagli del pacchetto consente ai client di visualizzare nell'interfaccia utente un collegamento Web a più dettagli del pacchetto
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610950"
---
# <a name="package-details-url-template"></a><span data-ttu-id="8ab1b-103">Modello URL Dettagli pacchetto</span><span class="sxs-lookup"><span data-stu-id="8ab1b-103">Package details URL template</span></span>

<span data-ttu-id="8ab1b-104">È possibile che un client crei un URL che può essere usato dall'utente per visualizzare altri dettagli del pacchetto nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="8ab1b-105">Questa operazione è utile quando un'origine del pacchetto desidera visualizzare informazioni aggiuntive su un pacchetto che potrebbero non rientrare nell'ambito di ciò che viene visualizzato nell'applicazione client NuGet.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="8ab1b-106">La risorsa usata per la compilazione di questo URL è la risorsa `PackageDetailsUriTemplate` trovata nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="8ab1b-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8ab1b-107">Versionamento</span><span class="sxs-lookup"><span data-stu-id="8ab1b-107">Versioning</span></span>

<span data-ttu-id="8ab1b-108">Vengono utilizzati i valori `@type` seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ab1b-108">The following `@type` values are used:</span></span>

<span data-ttu-id="8ab1b-109">Valore di@type</span><span class="sxs-lookup"><span data-stu-id="8ab1b-109">@type value</span></span>                     | <span data-ttu-id="8ab1b-110">Note</span><span class="sxs-lookup"><span data-stu-id="8ab1b-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="8ab1b-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="8ab1b-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="8ab1b-112">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="8ab1b-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="8ab1b-113">Modello URL</span><span class="sxs-lookup"><span data-stu-id="8ab1b-113">URL template</span></span>

<span data-ttu-id="8ab1b-114">L'URL per l'API seguente è il valore della proprietà `@id` associata a uno dei valori di `@type` di risorse indicati sopra.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8ab1b-115">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="8ab1b-115">HTTP methods</span></span>

<span data-ttu-id="8ab1b-116">Anche se il client non è destinato a eseguire richieste all'URL dei dettagli del pacchetto per conto dell'utente, la pagina Web deve supportare il metodo `GET` per consentire l'apertura semplice di un URL selezionato in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="8ab1b-117">Costruire l'URL</span><span class="sxs-lookup"><span data-stu-id="8ab1b-117">Construct the URL</span></span>

<span data-ttu-id="8ab1b-118">Dato un ID e una versione del pacchetto noti, l'implementazione client può costruire un URL usato per accedere a un'interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="8ab1b-119">L'implementazione client deve visualizzare l'URL costruito (o collegamento selezionabile) per consentire all'utente di aprire un Web browser all'URL e di ottenere ulteriori informazioni sul pacchetto.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="8ab1b-120">Il contenuto della pagina dei dettagli del pacchetto è determinato dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="8ab1b-121">L'URL deve essere un URL assoluto e lo schema (protocollo) deve essere HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="8ab1b-122">Il valore della `@id` nell'indice del servizio è una stringa URL contenente uno dei token segnaposto seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ab1b-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="8ab1b-123">Segnaposto URL</span><span class="sxs-lookup"><span data-stu-id="8ab1b-123">URL placeholders</span></span>

<span data-ttu-id="8ab1b-124">Name</span><span class="sxs-lookup"><span data-stu-id="8ab1b-124">Name</span></span>        | <span data-ttu-id="8ab1b-125">Digitare</span><span class="sxs-lookup"><span data-stu-id="8ab1b-125">Type</span></span>    | <span data-ttu-id="8ab1b-126">Richiesto</span><span class="sxs-lookup"><span data-stu-id="8ab1b-126">Required</span></span> | <span data-ttu-id="8ab1b-127">Note</span><span class="sxs-lookup"><span data-stu-id="8ab1b-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="8ab1b-128">string</span><span class="sxs-lookup"><span data-stu-id="8ab1b-128">string</span></span>  | <span data-ttu-id="8ab1b-129">No</span><span class="sxs-lookup"><span data-stu-id="8ab1b-129">no</span></span>       | <span data-ttu-id="8ab1b-130">ID del pacchetto per cui ottenere i dettagli</span><span class="sxs-lookup"><span data-stu-id="8ab1b-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="8ab1b-131">string</span><span class="sxs-lookup"><span data-stu-id="8ab1b-131">string</span></span>  | <span data-ttu-id="8ab1b-132">No</span><span class="sxs-lookup"><span data-stu-id="8ab1b-132">no</span></span>       | <span data-ttu-id="8ab1b-133">Versione del pacchetto per cui ottenere i dettagli</span><span class="sxs-lookup"><span data-stu-id="8ab1b-133">The package version to get details for</span></span>

<span data-ttu-id="8ab1b-134">Il server deve accettare `{id}` e `{version}` valori con qualsiasi combinazione di maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="8ab1b-135">Inoltre, il server non deve essere sensibile alla [normalizzazione](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)della versione.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="8ab1b-136">In altre parole, il server deve accettare anche versioni non normalizzate.</span><span class="sxs-lookup"><span data-stu-id="8ab1b-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="8ab1b-137">Ad esempio, il modello di dettagli del pacchetto NuGet. org è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8ab1b-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="8ab1b-138">Se l'implementazione client deve visualizzare un collegamento ai dettagli del pacchetto per NuGet. Versioning 4.3.0, produrrebbe l'URL seguente e lo fornirà all'utente:</span><span class="sxs-lookup"><span data-stu-id="8ab1b-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
