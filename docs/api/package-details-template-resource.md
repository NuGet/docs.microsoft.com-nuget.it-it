---
title: Modello di URL dei dettagli del pacchetto, API NuGet
description: Il modello di URL dei dettagli del pacchetto consente ai client di visualizzare nell'interfaccia utente un collegamento Web a più dettagli del pacchetto
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773944"
---
# <a name="package-details-url-template"></a><span data-ttu-id="54ed1-103">Modello URL Dettagli pacchetto</span><span class="sxs-lookup"><span data-stu-id="54ed1-103">Package details URL template</span></span>

<span data-ttu-id="54ed1-104">È possibile che un client crei un URL che può essere usato dall'utente per visualizzare altri dettagli del pacchetto nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="54ed1-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="54ed1-105">Questa operazione è utile quando un'origine del pacchetto desidera visualizzare informazioni aggiuntive su un pacchetto che potrebbero non rientrare nell'ambito di ciò che viene visualizzato nell'applicazione client NuGet.</span><span class="sxs-lookup"><span data-stu-id="54ed1-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="54ed1-106">La risorsa utilizzata per la compilazione di questo URL è la `PackageDetailsUriTemplate` risorsa presente nell' [indice del servizio](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="54ed1-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="54ed1-107">Controllo delle versioni</span><span class="sxs-lookup"><span data-stu-id="54ed1-107">Versioning</span></span>

<span data-ttu-id="54ed1-108">`@type`Vengono usati i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="54ed1-108">The following `@type` values are used:</span></span>

<span data-ttu-id="54ed1-109">Valore della proprietà @type</span><span class="sxs-lookup"><span data-stu-id="54ed1-109">@type value</span></span>                     | <span data-ttu-id="54ed1-110">Note</span><span class="sxs-lookup"><span data-stu-id="54ed1-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="54ed1-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="54ed1-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="54ed1-112">Versione iniziale</span><span class="sxs-lookup"><span data-stu-id="54ed1-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="54ed1-113">Modello di URL</span><span class="sxs-lookup"><span data-stu-id="54ed1-113">URL template</span></span>

<span data-ttu-id="54ed1-114">L'URL per l'API seguente è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` indicati sopra.</span><span class="sxs-lookup"><span data-stu-id="54ed1-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="54ed1-115">Metodi HTTP</span><span class="sxs-lookup"><span data-stu-id="54ed1-115">HTTP methods</span></span>

<span data-ttu-id="54ed1-116">Anche se il client non è destinato a eseguire richieste all'URL dei dettagli del pacchetto per conto dell'utente, la pagina Web deve supportare il `GET` metodo per consentire l'apertura semplice di un URL selezionato in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="54ed1-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="54ed1-117">Costruire l'URL</span><span class="sxs-lookup"><span data-stu-id="54ed1-117">Construct the URL</span></span>

<span data-ttu-id="54ed1-118">Dato un ID e una versione del pacchetto noti, l'implementazione client può costruire un URL usato per accedere a un'interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="54ed1-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="54ed1-119">L'implementazione client deve visualizzare l'URL costruito (o collegamento selezionabile) per consentire all'utente di aprire un Web browser all'URL e di ottenere ulteriori informazioni sul pacchetto.</span><span class="sxs-lookup"><span data-stu-id="54ed1-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="54ed1-120">Il contenuto della pagina dei dettagli del pacchetto è determinato dall'implementazione del server.</span><span class="sxs-lookup"><span data-stu-id="54ed1-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="54ed1-121">L'URL deve essere un URL assoluto e lo schema (protocollo) deve essere HTTPS.</span><span class="sxs-lookup"><span data-stu-id="54ed1-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="54ed1-122">Il valore di `@id` nell'indice del servizio è una stringa URL contenente uno dei token segnaposto seguenti:</span><span class="sxs-lookup"><span data-stu-id="54ed1-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="54ed1-123">Segnaposto URL</span><span class="sxs-lookup"><span data-stu-id="54ed1-123">URL placeholders</span></span>

<span data-ttu-id="54ed1-124">Nome</span><span class="sxs-lookup"><span data-stu-id="54ed1-124">Name</span></span>        | <span data-ttu-id="54ed1-125">Type</span><span class="sxs-lookup"><span data-stu-id="54ed1-125">Type</span></span>    | <span data-ttu-id="54ed1-126">Necessario</span><span class="sxs-lookup"><span data-stu-id="54ed1-126">Required</span></span> | <span data-ttu-id="54ed1-127">Note</span><span class="sxs-lookup"><span data-stu-id="54ed1-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="54ed1-128">string</span><span class="sxs-lookup"><span data-stu-id="54ed1-128">string</span></span>  | <span data-ttu-id="54ed1-129">no</span><span class="sxs-lookup"><span data-stu-id="54ed1-129">no</span></span>       | <span data-ttu-id="54ed1-130">ID del pacchetto per cui ottenere i dettagli</span><span class="sxs-lookup"><span data-stu-id="54ed1-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="54ed1-131">string</span><span class="sxs-lookup"><span data-stu-id="54ed1-131">string</span></span>  | <span data-ttu-id="54ed1-132">no</span><span class="sxs-lookup"><span data-stu-id="54ed1-132">no</span></span>       | <span data-ttu-id="54ed1-133">Versione del pacchetto per cui ottenere i dettagli</span><span class="sxs-lookup"><span data-stu-id="54ed1-133">The package version to get details for</span></span>

<span data-ttu-id="54ed1-134">Il server deve accettare `{id}` i `{version}` valori e con qualsiasi combinazione di maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="54ed1-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="54ed1-135">Inoltre, il server non deve essere sensibile alla [normalizzazione](../concepts/package-versioning.md#normalized-version-numbers)della versione.</span><span class="sxs-lookup"><span data-stu-id="54ed1-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="54ed1-136">In altre parole, il server deve accettare anche versioni non normalizzate.</span><span class="sxs-lookup"><span data-stu-id="54ed1-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="54ed1-137">Ad esempio, il modello di dettagli del pacchetto NuGet. org è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="54ed1-137">For example, nuget.org's package details template looks like this:</span></span>

```http
https://www.nuget.org/packages/{id}/{version}
```

<span data-ttu-id="54ed1-138">Se l'implementazione client deve visualizzare un collegamento ai dettagli del pacchetto per NuGet. Versioning 4.3.0, produrrebbe l'URL seguente e lo fornirà all'utente:</span><span class="sxs-lookup"><span data-stu-id="54ed1-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
