---
title: File Leggimi del pacchetto NuGet.org
description: Spiegazione dettagliata del rendering dei file Readme NuGet.org e delle operazioni da eseguire quando si verificano problemi.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902248"
---
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="f2206-103">File Leggimi del pacchetto NuGet.org</span><span class="sxs-lookup"><span data-stu-id="f2206-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="f2206-104">[Includere un file Leggimi nel pacchetto NuGet per](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) rendere i dettagli del pacchetto più completi e più informativi per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="f2206-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="f2206-105">Questo è probabilmente uno dei primi elementi che gli utenti visualizzano quando visualizzano la pagina dei dettagli del pacchetto NuGet.org ed è essenziale per fare una buona impressione.</span><span class="sxs-lookup"><span data-stu-id="f2206-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2206-106">NuGet.org supporta solo file Leggimi in [Markdown](https://daringfireball.net/projects/markdown/) e immagini da un set limitato di domini.</span><span class="sxs-lookup"><span data-stu-id="f2206-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="f2206-107">Vedere i [domini consentiti per le immagini e](#allowed-domains-for-images-and-badges) le funzionalità [markdown](#supported-markdown-features) supportate per assicurarsi che il rendering del file Leggimi venga eseguito correttamente NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f2206-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="f2206-108">Cosa deve includere il file Leggimi?</span><span class="sxs-lookup"><span data-stu-id="f2206-108">What should my readme include?</span></span>

<span data-ttu-id="f2206-109">È consigliabile includere gli elementi seguenti nel file Leggimi:</span><span class="sxs-lookup"><span data-stu-id="f2206-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="f2206-110">Introduzione a che cos'è e cosa fa il pacchetto, quali problemi risolve?</span><span class="sxs-lookup"><span data-stu-id="f2206-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="f2206-111">Come iniziare a usare il pacchetto: esistono requisiti specifici?</span><span class="sxs-lookup"><span data-stu-id="f2206-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="f2206-112">Collegamenti a una documentazione più completa, se non inclusa nel file Leggimi stesso.</span><span class="sxs-lookup"><span data-stu-id="f2206-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="f2206-113">Almeno alcuni frammenti di codice/esempi o immagini di esempio.</span><span class="sxs-lookup"><span data-stu-id="f2206-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="f2206-114">Dove e come lasciare commenti e suggerimenti, ad esempio un collegamento ai problemi del progetto, Twitter, lo tracker di bug o un'altra piattaforma.</span><span class="sxs-lookup"><span data-stu-id="f2206-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="f2206-115">Come contribuire, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="f2206-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="f2206-116">Tenere presente che i file leggimi di alta qualità possono essere disponibili in un'ampia gamma di formati, forme e dimensioni.</span><span class="sxs-lookup"><span data-stu-id="f2206-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="f2206-117">Se in NuGet.org è già disponibile un pacchetto, è probabile che nel repository sia già presente un file di documentazione o un altro file che rappresenta un'ottima aggiunta alla pagina dei dettagli `readme.md` NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f2206-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="f2206-118">Visualizzare in anteprima il file Leggimi</span><span class="sxs-lookup"><span data-stu-id="f2206-118">Preview your readme</span></span>

<span data-ttu-id="f2206-119">Per visualizzare in anteprima il file Leggimi prima che sia live in NuGet.org, caricare il pacchetto usando il portale Web carica pacchetto [in NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) e scorrere verso il basso fino alla sezione "File Leggimi" dell'anteprima dei metadati.</span><span class="sxs-lookup"><span data-stu-id="f2206-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="f2206-120">L'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f2206-120">It should look something like this:</span></span>

![Anteprima file Leggimi](media\readme-upload-preview.PNG)

<span data-ttu-id="f2206-122">Prendere in considerazione la possibilità di [](#allowed-domains-for-images-and-badges) esaminare e [](#supported-markdown-features) visualizzare in anteprima il file Leggimi per la conformità delle immagini e la formattazione supportata per assicurarsi che sia una buona prima impressione per i potenziali utenti.</span><span class="sxs-lookup"><span data-stu-id="f2206-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="f2206-123">Per correggere gli errori nel file leggimi del pacchetto dopo che è stato pubblicato NuGet.org, è necessario eseguire il push di una versione aggiornata del pacchetto con la correzione.</span><span class="sxs-lookup"><span data-stu-id="f2206-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="f2206-124">Assicurarsi che tutto sia a posto in anticipo può far risparmiare il mal di testa lungo la strada.</span><span class="sxs-lookup"><span data-stu-id="f2206-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="f2206-125">Domini consentiti per immagini e notifiche</span><span class="sxs-lookup"><span data-stu-id="f2206-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="f2206-126">A causa di problemi di sicurezza e privacy, NuGet.org i domini da cui è possibile eseguire il rendering di immagini e notifiche agli host attendibili.</span><span class="sxs-lookup"><span data-stu-id="f2206-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="f2206-127">NuGet.org il rendering di tutte le immagini, incluse le notifiche, dei domini attendibili seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2206-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="f2206-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="f2206-128">api.bintray.com</span></span>
* <span data-ttu-id="f2206-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="f2206-129">api.codacy.com</span></span>
* <span data-ttu-id="f2206-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="f2206-130">api.codeclimate.com</span></span>
* <span data-ttu-id="f2206-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="f2206-131">api.dependabot.com</span></span>
* <span data-ttu-id="f2206-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="f2206-132">api.travis-ci.com</span></span>
* <span data-ttu-id="f2206-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="f2206-133">api.travis-ci.org</span></span>
* <span data-ttu-id="f2206-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="f2206-134">app.fossa.io</span></span>
* <span data-ttu-id="f2206-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="f2206-135">badge.fury.io</span></span>
* <span data-ttu-id="f2206-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="f2206-136">badgen.net</span></span>
* <span data-ttu-id="f2206-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="f2206-137">badges.gitter.im</span></span>
* <span data-ttu-id="f2206-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="f2206-138">bettercodehub.com</span></span>
* <span data-ttu-id="f2206-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="f2206-139">buildstats.info</span></span>
* <span data-ttu-id="f2206-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="f2206-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="f2206-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="f2206-141">ci.appveyor.com</span></span>
* <span data-ttu-id="f2206-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="f2206-142">circleci.com</span></span>
* <span data-ttu-id="f2206-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="f2206-143">codecov.io</span></span>
* <span data-ttu-id="f2206-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="f2206-144">codefactor.io</span></span>
* <span data-ttu-id="f2206-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="f2206-145">coveralls.io</span></span>
* <span data-ttu-id="f2206-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="f2206-146">dev.azure.com</span></span>
* <span data-ttu-id="f2206-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="f2206-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="f2206-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="f2206-148">gitlab.com</span></span>
* <span data-ttu-id="f2206-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="f2206-149">img.shields.io</span></span>
* <span data-ttu-id="f2206-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="f2206-150">isitmaintained.com</span></span>
* <span data-ttu-id="f2206-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="f2206-151">opencollective.com</span></span>
* <span data-ttu-id="f2206-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="f2206-152">raw.github.com</span></span>
* <span data-ttu-id="f2206-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="f2206-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="f2206-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="f2206-154">snyk.io</span></span>
* <span data-ttu-id="f2206-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="f2206-155">sonarcloud.io</span></span>
* <span data-ttu-id="f2206-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="f2206-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="f2206-157">Se si desidera aggiungere un altro dominio all'elenco degli [](https://github.com/NuGet/NuGetGallery/issues) elementi consentiti, è possibile determinare un problema che verrà esaminato dal team tecnico per la conformità alla privacy e alla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f2206-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="f2206-158">Le immagini con percorsi locali relativi e le immagini ospitate da domini non supportati non verranno visualizzate e genereranno un avviso nella pagina di anteprima del file Leggimi e nella pagina dei dettagli del pacchetto visibile solo ai proprietari del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f2206-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="f2206-159">Funzionalità markdown supportate</span><span class="sxs-lookup"><span data-stu-id="f2206-159">Supported Markdown features</span></span>
<span data-ttu-id="f2206-160">[Markdown è](https://daringfireball.net/projects/markdown/) un linguaggio di markup leggero con sintassi di formattazione del testo normale.</span><span class="sxs-lookup"><span data-stu-id="f2206-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="f2206-161">NuGet.org readmes supportano Markdown conforme a [CommonMark](https://commonmark.org/) tramite il [motore di analisi Markdig.](https://github.com/lunet-io/markdig)</span><span class="sxs-lookup"><span data-stu-id="f2206-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="f2206-162">NuGet.org attualmente supporta le funzionalità Markdown seguenti:</span><span class="sxs-lookup"><span data-stu-id="f2206-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="f2206-163">Intestazioni</span><span class="sxs-lookup"><span data-stu-id="f2206-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="f2206-164">Immagini</span><span class="sxs-lookup"><span data-stu-id="f2206-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="f2206-165">Enfasi aggiuntiva</span><span class="sxs-lookup"><span data-stu-id="f2206-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="f2206-166">Elenchi</span><span class="sxs-lookup"><span data-stu-id="f2206-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="f2206-167">Collegamenti</span><span class="sxs-lookup"><span data-stu-id="f2206-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="f2206-168">Citazioni</span><span class="sxs-lookup"><span data-stu-id="f2206-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="f2206-169">Escape barra rovesciata</span><span class="sxs-lookup"><span data-stu-id="f2206-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="f2206-170">Intervalli di codice</span><span class="sxs-lookup"><span data-stu-id="f2206-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="f2206-171">Elenchi di attività</span><span class="sxs-lookup"><span data-stu-id="f2206-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="f2206-172">Tabelle</span><span class="sxs-lookup"><span data-stu-id="f2206-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="f2206-173">Emoji</span><span class="sxs-lookup"><span data-stu-id="f2206-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="f2206-174">Collegamenti automatici</span><span class="sxs-lookup"><span data-stu-id="f2206-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

