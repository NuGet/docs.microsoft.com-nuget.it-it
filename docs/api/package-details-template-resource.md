---
title: Modello di URL dettagli del pacchetto, NuGet API
description: Il modello di URL dei dettagli del pacchetto consente ai client di visualizzare l'interfaccia utente web collegamento a ulteriori dettagli del pacchetto
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638074"
---
# <a name="package-details-url-template"></a><span data-ttu-id="4d76c-103">Modello di URL dei dettagli del pacchetto</span><span class="sxs-lookup"><span data-stu-id="4d76c-103">Package details URL template</span></span>

<span data-ttu-id="4d76c-104">È possibile che un client per creare un URL che può essere utilizzato dall'utente per visualizzare ulteriori dettagli del pacchetto nel web browser.</span><span class="sxs-lookup"><span data-stu-id="4d76c-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="4d76c-105">Ciò è utile quando si desidera visualizzare informazioni aggiuntive relative a un pacchetto che potrebbe non rientrare nell'ambito di ciò che l'applicazione client di NuGet Mostra un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4d76c-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="4d76c-106">La risorsa usata per la creazione di questo URL è il `PackageDetailsUriTemplate` trovare la risorsa nella [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="4d76c-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="4d76c-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="4d76c-107">Versioning</span></span>

<span data-ttu-id="4d76c-108">Nell'esempio `@type` vengono utilizzati i valori:</span><span class="sxs-lookup"><span data-stu-id="4d76c-108">The following `@type` values are used:</span></span>

<span data-ttu-id="4d76c-109">Valore di @type</span><span class="sxs-lookup"><span data-stu-id="4d76c-109">@type value</span></span>                     | <span data-ttu-id="4d76c-110">Note</span><span class="sxs-lookup"><span data-stu-id="4d76c-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="4d76c-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="4d76c-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="4d76c-112">La versione iniziale</span><span class="sxs-lookup"><span data-stu-id="4d76c-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="4d76c-113">Modello di URL</span><span class="sxs-lookup"><span data-stu-id="4d76c-113">URL template</span></span>

<span data-ttu-id="4d76c-114">L'URL per l'API seguente è il valore della `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.</span><span class="sxs-lookup"><span data-stu-id="4d76c-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="4d76c-115">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="4d76c-115">HTTP methods</span></span>

<span data-ttu-id="4d76c-116">Anche se il client non può effettuare richieste all'URL dei dettagli del pacchetto per conto dell'utente, la pagina web deve supportare il `GET` metodo per consentire un URL selezionato essere facilmente aperto in un web browser.</span><span class="sxs-lookup"><span data-stu-id="4d76c-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="4d76c-117">Creare l'URL</span><span class="sxs-lookup"><span data-stu-id="4d76c-117">Construct the URL</span></span>

<span data-ttu-id="4d76c-118">Dato un ID noto pacchetto e versione, l'implementazione client può creare un URL utilizzato per accedere a un'interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="4d76c-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="4d76c-119">L'implementazione client deve visualizzare questo URL costruito (o un collegamento selezionabile) all'utente e consente loro di aprire un web browser all'URL e per altre informazioni sul pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4d76c-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="4d76c-120">Il contenuto della pagina dei dettagli del pacchetto è determinato dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="4d76c-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="4d76c-121">L'URL deve essere un URL assoluto e lo schema (protocollo) deve essere HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4d76c-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="4d76c-122">Il valore della `@id` nel servizio di indice è una stringa URL contenente uno dei token di segnaposto seguente:</span><span class="sxs-lookup"><span data-stu-id="4d76c-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="4d76c-123">Segnaposto URL</span><span class="sxs-lookup"><span data-stu-id="4d76c-123">URL placeholders</span></span>

<span data-ttu-id="4d76c-124">Nome</span><span class="sxs-lookup"><span data-stu-id="4d76c-124">Name</span></span>        | <span data-ttu-id="4d76c-125">Tipo</span><span class="sxs-lookup"><span data-stu-id="4d76c-125">Type</span></span>    | <span data-ttu-id="4d76c-126">Obbligatorio</span><span class="sxs-lookup"><span data-stu-id="4d76c-126">Required</span></span> | <span data-ttu-id="4d76c-127">Note</span><span class="sxs-lookup"><span data-stu-id="4d76c-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="4d76c-128">string</span><span class="sxs-lookup"><span data-stu-id="4d76c-128">string</span></span>  | <span data-ttu-id="4d76c-129">No</span><span class="sxs-lookup"><span data-stu-id="4d76c-129">no</span></span>       | <span data-ttu-id="4d76c-130">L'ID del pacchetto per ottenere i dettagli per</span><span class="sxs-lookup"><span data-stu-id="4d76c-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="4d76c-131">string</span><span class="sxs-lookup"><span data-stu-id="4d76c-131">string</span></span>  | <span data-ttu-id="4d76c-132">No</span><span class="sxs-lookup"><span data-stu-id="4d76c-132">no</span></span>       | <span data-ttu-id="4d76c-133">La versione del pacchetto per ottenere i dettagli per</span><span class="sxs-lookup"><span data-stu-id="4d76c-133">The package version to get details for</span></span>

<span data-ttu-id="4d76c-134">Il server deve accettare `{id}` e `{version}` valori con qualsiasi maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4d76c-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="4d76c-135">Inoltre, il server non deve essere sensibile alle se è la versione [normalizzato](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="4d76c-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="4d76c-136">In altre parole, il server deve accettare accettano anche le versioni non normalizzato.</span><span class="sxs-lookup"><span data-stu-id="4d76c-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="4d76c-137">Ad esempio, modello di dettagli del pacchetto di nuget.org aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4d76c-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="4d76c-138">Se l'implementazione client deve visualizzare un collegamento per i dettagli del pacchetto per NuGet.Versioning 4.3.0, verrebbe generato l'URL seguente e offrirlo all'utente:</span><span class="sxs-lookup"><span data-stu-id="4d76c-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
