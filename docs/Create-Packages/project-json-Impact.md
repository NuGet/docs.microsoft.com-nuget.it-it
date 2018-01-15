---
title: Impatto di project.json sugli autori di pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 983485df-9375-4827-b58b-70065320ee37
description: "Informazioni dettagliate su come l'implementazione di project.json in NuGet 3.x abbia effetto sugli autori di pacchetti, ad esempio con funzionalità, contenuto e formato dei pacchetti non supportati."
keywords: "NuGet e project.json, impatto di project.json, considerazioni sulla creazione di pacchetti, funzionalità di project.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 69a6bbbe1c96b06dbba7ac787b836b8b62c438ec
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="9c7d7-104">Impatto di project.json durante la creazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="9c7d7-104">Impact of project.json when creating packages</span></span>

<span data-ttu-id="9c7d7-105">Il sistema `project.json` usato in NuGet 3+ ha effetto sugli autori di pacchetti in diversi modi, come illustrato nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-105">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="9c7d7-106">Modifiche che hanno effetto sull'utilizzo dei pacchetti esistenti</span><span class="sxs-lookup"><span data-stu-id="9c7d7-106">Changes affecting existing packages usage</span></span>

<span data-ttu-id="9c7d7-107">I tradizionali pacchetti NuGet supportano un set di funzionalità che non passano nella sfera transitiva.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-107">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="9c7d7-108">Gli script di installazione e disinstallazione vengono ignorati</span><span class="sxs-lookup"><span data-stu-id="9c7d7-108">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="9c7d7-109">Il modello di ripristino transitivo, illustrato in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson), non contempla il concetto di "fase di installazione dei pacchetti".</span><span class="sxs-lookup"><span data-stu-id="9c7d7-109">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson), does not have a concept of "package install time".</span></span> <span data-ttu-id="9c7d7-110">Un pacchetto è presento o non presente, ma non esiste un processo coerente eseguito quando viene installato un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-110">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="9c7d7-111">Gli script di installazione inoltre erano supportati solo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-111">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="9c7d7-112">Gli altri IDE dovevano simulare l'API di estendibilità di Visual Studio per provare a supportare tali script e nessun supporto era disponibile negli editor e negli strumenti da riga di comando comuni.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-112">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="9c7d7-113">Le trasformazioni di contenuto non sono supportate.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-113">Content transforms are not supported.</span></span>

<span data-ttu-id="9c7d7-114">Analogamente agli script di installazione, le trasformazioni vengono eseguite durante l'installazione dei pacchetti e in genere non sono idempotenti.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-114">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="9c7d7-115">Poiché non esiste più una fase di installazione, la trasformazione XDT e funzionalità simili non sono supportate e vengono ignorate se un pacchetto di questo tipo viene usato in uno scenario transitivo.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-115">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>


### <a name="content"></a><span data-ttu-id="9c7d7-116">Content</span><span class="sxs-lookup"><span data-stu-id="9c7d7-116">Content</span></span>

<span data-ttu-id="9c7d7-117">Nei tradizionali pacchetti NuGet sono disponibili file di contento, ad esempio codice sorgente e file di configurazione,</span><span class="sxs-lookup"><span data-stu-id="9c7d7-117">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="9c7d7-118">che in genere vengono usati in due scenari:</span><span class="sxs-lookup"><span data-stu-id="9c7d7-118">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="9c7d7-119">File iniziali rilasciati nel progetto in modo che l'utente possa modificarli successivamente.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-119">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="9c7d7-120">Un esempio comune sono i file di configurazione predefiniti.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-120">The common example is default configuration files.</span></span>

2. <span data-ttu-id="9c7d7-121">File di contenuto usati come complemento degli assembly installati nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-121">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="9c7d7-122">In questo caso l'esempio può essere l'immagine di un logo usata da un assembly.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-122">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="9c7d7-123">Il supporto per il contenuto è attualmente disabilitato per motivi simili a quelli degli script e delle trasformazioni, ma ne è in corso la progettazione.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-123">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="9c7d7-124">I file di contenuto possono comunque essere inseriti nei pacchetti anche se attualmente vengono ignorati, tuttavia l'utente finale può comunque copiarli nella posizione corretta.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-124">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="9c7d7-125">Per una proposta di ripristino dei file di contenuto e per seguirne lo stato, vedere [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="9c7d7-125">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="9c7d7-126">Impatto per gli autori di pacchetti</span><span class="sxs-lookup"><span data-stu-id="9c7d7-126">Impact for package authors</span></span>

<span data-ttu-id="9c7d7-127">I pacchetti che usano le funzionalità indicate sopra devono usare un meccanismo diverso.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-127">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="9c7d7-128">Il meccanismo di norma più utile prevede l'uso dei file di destinazioni/proprietà MSBuild che sono ancora pienamente supportati.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-128">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="9c7d7-129">Il sistema di compilazione può scegliere di selezionare altre convenzioni nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-129">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="9c7d7-130">In questo modo vengono supportate le destinazioni MSBuild, oltre agli analizzatori Roslyn.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-130">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="9c7d7-131">È possibile compilare pacchetti che supportano destinazioni e analizzatori per scenari `packages.config` e `project.json`.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-131">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="9c7d7-132">I pacchetti che provano a modificare il progetto per semplificare l'avvio in genere funzionano in un set molto limitato di scenari e devono fornire un file leggimi o linee guida su come usare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-132">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="9c7d7-133">La maggior parte dei pacchetti esistenti non dovrà usare il formato descritto sotto.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-133">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="9c7d7-134">Il formato consente il contenuto nativo come scenario di prima classe.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-134">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="9c7d7-135">Gli assembly gestiti dipendono quindi da implementazioni collegate all'hardware per l'invio di implementazioni binarie unitamente agli assembly gestiti in base alla piattaforma di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-135">This means that managed assemblies depending on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="9c7d7-136">Il pacchetto System.IO.Compression, ad esempio, utilizza questa tecnologia.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-136">For example System.IO.Compression package is utilizing this technology.</span></span> [<span data-ttu-id="9c7d7-137">https://www.nuget.org/packages/System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="9c7d7-137">https://www.nuget.org/packages/System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="9c7d7-138">In sintesi, se la funzionalità illustrata sopra non è assolutamente necessaria, è consigliabile continuare a usare il formato di pacchetto esistente, perché il formato descritto qui è supportato solo da NuGet 3.x+.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="9c7d7-139">Anche se è possibile compilare pacchetti che funzionino in scenari sia `packages.config` che `project.json` tramite l'esecuzione di shim, spesso è più semplice limitarsi a strutturare i pacchetti nel modo tradizionale, senza le funzionalità deprecate citate sopra.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>


## <a name="3x-package-format"></a><span data-ttu-id="9c7d7-140">Formato del pacchetto 3.x</span><span class="sxs-lookup"><span data-stu-id="9c7d7-140">3.x package format</span></span>  ##

<span data-ttu-id="9c7d7-141">Il formato del pacchetto 3.x consente di usare diverse funzionalità aggiuntive oltre a quelle di NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="9c7d7-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="9c7d7-142">Definizione di un assembly di riferimento usato per la compilazione e di un set di assembly di implementazioni usati per il runtime in diverse piattaforme o dispositivi.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="9c7d7-143">Ciò consente di sfruttare le API specifiche della piattaforma fornendo al contempo una superficie di attacco comune agli utenti.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="9c7d7-144">In particolare risulta semplificata la scrittura di librerie portabili intermedie.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

2. <span data-ttu-id="9c7d7-145">I pacchetti possono basarsi sulle piattaforme, ad esempio sistemi operativi o architettura CPU.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

3. <span data-ttu-id="9c7d7-146">È consentita la separazione di implementazioni specifiche delle piattaforme nei pacchetti complementari.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-146">Allows for separation of platform specific implementations to companion packages.</span></span>

4. <span data-ttu-id="9c7d7-147">Supporto delle dipendenze native come oggetto di prima classe.</span><span class="sxs-lookup"><span data-stu-id="9c7d7-147">Support Native dependencies as a first class citizen.</span></span>