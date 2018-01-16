---
title: Domande frequenti su NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: Domande e risposte frequenti per l'uso di NuGet nella riga di comando e in Visual Studio e per l'uso della raccolta NuGet.
keywords: Domande frequenti NuGet, domande e risposte, problemi comuni, versioni di NuGet, versioni dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d19a24a2d1955e996e18d44fee346865d36493f8
ms.sourcegitcommit: e5b7cf6675be9891341c196afe822cea6f71d60c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="af491-104">Domande frequenti su NuGet</span><span class="sxs-lookup"><span data-stu-id="af491-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="af491-105">In questo argomento</span><span class="sxs-lookup"><span data-stu-id="af491-105">In this topic:</span></span>

- [<span data-ttu-id="af491-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="af491-106">Getting started</span></span>](#getting-started)
- [<span data-ttu-id="af491-107">NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af491-107">NuGet in Visual Studio</span></span>](#nuget-in-visual-studio)
- [<span data-ttu-id="af491-108">Riga di comando di NuGet</span><span class="sxs-lookup"><span data-stu-id="af491-108">NuGet command line</span></span>](#nuget-command-line)
- [<span data-ttu-id="af491-109">Console di Gestione pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="af491-109">NuGet Package Manager Console</span></span>](#nuget-package-manager-console)
- [<span data-ttu-id="af491-110">Creazione e pubblicazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="af491-110">Creating and publishing packages</span></span>](#creating-and-publishing-packages)
- [<span data-ttu-id="af491-111">Utilizzo dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="af491-111">Working with packages</span></span>](#working-with-packages)
- [<span data-ttu-id="af491-112">Gestione dei pacchetti in nuget.org</span><span class="sxs-lookup"><span data-stu-id="af491-112">Managing packages on nuget.org</span></span>](#managing-packages-on-nugetorg)
- [<span data-ttu-id="af491-113">nuget.org non accessibile</span><span class="sxs-lookup"><span data-stu-id="af491-113">nuget.org not accessible</span></span>](#nugetorg-not-accessible)

## <a name="getting-started"></a><span data-ttu-id="af491-114">Per iniziare</span><span class="sxs-lookup"><span data-stu-id="af491-114">Getting started</span></span>

<span data-ttu-id="af491-115">**Che cos'è richiesto per eseguire NuGet?**</span><span class="sxs-lookup"><span data-stu-id="af491-115">**What is required to run NuGet?**</span></span>

<span data-ttu-id="af491-116">Tutte le informazioni sia sull'interfaccia utente che sugli strumenti da riga di comando sono disponibili in [Installazione degli strumenti client di NuGet](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="af491-116">All the information around both UI and command-line tools is available in the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="af491-117">**NuGet supporta Mono?**</span><span class="sxs-lookup"><span data-stu-id="af491-117">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="af491-118">Lo strumento da riga di comando, `nuget.exe`, supporta l'esecuzione e la compilazione in Mono 3.2+ e consente di creare pacchetti in Mono.</span><span class="sxs-lookup"><span data-stu-id="af491-118">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="af491-119">Anche se `nuget.exe` funziona in modo ottimale in Windows, esistono alcuni problemi noti in Linux e OS X. Vedere i [problemi relativi a Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="af491-119">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="af491-120">È disponibile un [client grafico](https://github.com/mrward/monodevelop-nuget-addin) come componente aggiuntivo per MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="af491-120">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="af491-121">**Come è possibile determinare il contenuto di un pacchetto e se è stabile e utile per la mia applicazione?**</span><span class="sxs-lookup"><span data-stu-id="af491-121">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="af491-122">La fonte principale di informazioni su un pacchetto è la relativa pagina di presentazione in nuget.org (o un altro feed privato).</span><span class="sxs-lookup"><span data-stu-id="af491-122">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="af491-123">Ogni pagina di pacchetto in nuget.org include una descrizione del pacchetto, la cronologia delle versioni e le statistiche di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="af491-123">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="af491-124">La sezione **Info** nella pagina del pacchetto contiene anche un collegamento al sito Web del progetto in cui è in genere possibile trovare numerosi esempi e documentazione per scoprire di più su come viene usato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af491-124">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="af491-125">Per altre informazioni, vedere [Ricerca e scelta di pacchetti](../Consume-Packages/Finding-and-Choosing-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="af491-125">For more information, see [Finding and choosing packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="af491-126">NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af491-126">NuGet in Visual Studio</span></span>

<span data-ttu-id="af491-127">**Come viene supportato NuGet nei diversi prodotti Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="af491-127">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="af491-128">Visual Studio in Windows supporta l'[interfaccia utente di Gestione pacchetti](../tools/Package-Manager-UI.md) e la [console di Gestione pacchetti](../tools/Package-Manager-Console.md).</span><span class="sxs-lookup"><span data-stu-id="af491-128">Visual Studio on Windows supports the [Package Manager UI](../tools/Package-Manager-UI.md) and the [Package Manager Console](../tools/Package-Manager-Console.md).</span></span>
- <span data-ttu-id="af491-129">Visual Studio per Mac include funzionalità incorporate di NuGet come descritto in [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="af491-129">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="af491-130">Visual Studio Code (tutte le piattaforme) non include alcuna integrazione diretta di NuGet.</span><span class="sxs-lookup"><span data-stu-id="af491-130">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="af491-131">Usare l'[interfaccia della riga di comando di NuGet](../tools/nuget-exe-CLI-Reference.md) o l'[interfaccia della riga di comando di dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="af491-131">Use the [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="af491-132">Visual Studio Team Services offre [un passaggio di compilazione per il ripristino dei pacchetti NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="af491-132">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="af491-133">È anche possibile [ospitare feed di pacchetti NuGet privati in Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="af491-133">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="af491-134">**Come è possibile controllare la versione esatta degli strumenti di NuGet installati?**</span><span class="sxs-lookup"><span data-stu-id="af491-134">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="af491-135">In Visual Studio, usare il comando **Guida > informazioni su Microsoft Visual Studio** e controllare la versione visualizzata accanto a **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="af491-135">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="af491-136">In alternativa, avviare la console di Gestione pacchetti (**Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**) e immettere `$host` per visualizzare informazioni su NuGet, compresa la versione.</span><span class="sxs-lookup"><span data-stu-id="af491-136">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="af491-137">**Quali linguaggi di programmazione sono supportati da NuGet?**</span><span class="sxs-lookup"><span data-stu-id="af491-137">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="af491-138">NuGet funziona in generale per i linguaggi .NET ed è progettato per integrare le librerie .NET in un progetto.</span><span class="sxs-lookup"><span data-stu-id="af491-138">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="af491-139">Dato che supporta anche l'automazione di MSBuild e Visual Studio in alcuni tipi di progetto, sono supportati anche altri progetti e linguaggi a vari livelli.</span><span class="sxs-lookup"><span data-stu-id="af491-139">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="af491-140">La versione più recente di NuGet supporta C#, Visual Basic, F#, WiX e C++.</span><span class="sxs-lookup"><span data-stu-id="af491-140">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="af491-141">**Quali modelli di progetto sono supportati da NuGet?**</span><span class="sxs-lookup"><span data-stu-id="af491-141">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="af491-142">NuGet offre il supporto completo per un'ampia gamma di modelli di progetto come Windows, Web, Cloud, SharePoint, Wix e così via.</span><span class="sxs-lookup"><span data-stu-id="af491-142">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="af491-143">**Qual è la procedura per aggiornare i pacchetti che fanno parte di modelli di Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="af491-143">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="af491-144">Passare alla scheda **Aggiornamenti** nell'interfaccia utente di Gestione pacchetti e selezionare **Aggiorna tutto** oppure usare il [comando `Update-Package`](../Tools/ps-ref-update-package.md) dalla console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="af491-144">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../Tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="af491-145">Per aggiornare il modello stesso, è necessario aggiornare manualmente il repository del modello.</span><span class="sxs-lookup"><span data-stu-id="af491-145">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="af491-146">Vedere il [blog di Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) su questo argomento.</span><span class="sxs-lookup"><span data-stu-id="af491-146">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="af491-147">Si noti che questa operazione viene eseguita a proprio rischio, poiché gli aggiornamenti manuali potrebbero danneggiare il modello, se le versioni più recenti di tutte le dipendenze non sono compatibili tra loro.</span><span class="sxs-lookup"><span data-stu-id="af491-147">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="af491-148">**È possibile usare NuGet all'esterno di Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="af491-148">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="af491-149">Sì, NuGet funziona direttamente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="af491-149">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="af491-150">Vedere la [guida all'installazione](../guides/install-nuget.md) e le [informazioni di riferimento sull'interfaccia della riga di comando](../tools/nuget-exe-CLI-Reference.md).</span><span class="sxs-lookup"><span data-stu-id="af491-150">See the [Install guide](../guides/install-nuget.md) and the [CLI reference](../tools/nuget-exe-CLI-Reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="af491-151">Riga di comando di NuGet</span><span class="sxs-lookup"><span data-stu-id="af491-151">NuGet command line</span></span>

<span data-ttu-id="af491-152">**Qual è la procedura per ottenere la versione più recente dello strumento da riga di comando di NuGet?**</span><span class="sxs-lookup"><span data-stu-id="af491-152">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="af491-153">Vedere la [guida all'installazione](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="af491-153">See the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="af491-154">**È possibile estendere lo strumento da riga di comando di NuGet?**</span><span class="sxs-lookup"><span data-stu-id="af491-154">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="af491-155">Sì, è possibile aggiungere comandi personalizzati a `nuget.exe`, come descritto nel [post di Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="af491-155">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="af491-156">Console di Gestione pacchetti Nuget (Visual Studio in Windows)</span><span class="sxs-lookup"><span data-stu-id="af491-156">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="af491-157">**Qual è la procedura per ottenere l'accesso all'oggetto DTE nella console di Gestione pacchetti**</span><span class="sxs-lookup"><span data-stu-id="af491-157">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="af491-158">L'oggetto di primo livello nel modello a oggetti di automazione di Visual Studio viene chiamato oggetto DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="af491-158">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="af491-159">La console rende disponibile questo oggetto tramite una variabile denominata `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="af491-159">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="af491-160">Per altre informazioni, vedere [Cenni preliminari sul modello di automazione](/visualstudio/extensibility/internals/automation-model-overview) nella documentazione sull'estendibilità di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af491-160">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="af491-161">**Quando si tenta di eseguire il cast della variabile $DTE al tipo DTE2 viene visualizzato un errore: Impossibile convertire il valore "EnvDTE.DTEClass" di tipo "EnvDTE.DTEClass" al tipo "EnvDTE80.DTE2". Qual è il problema?**</span><span class="sxs-lookup"><span data-stu-id="af491-161">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="af491-162">Si tratta di un problema noto correlato alla modalità di interazione di PowerShell con un oggetto COM.</span><span class="sxs-lookup"><span data-stu-id="af491-162">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="af491-163">Provare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="af491-163">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="af491-164">`Get-Interface` è una funzione helper aggiunta dall'host di PowerShell di NuGet.</span><span class="sxs-lookup"><span data-stu-id="af491-164">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="af491-165">Creazione e pubblicazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="af491-165">Creating and publishing packages</span></span>

<span data-ttu-id="af491-166">**Qual è la procedura per presentare un pacchetto in un feed?**</span><span class="sxs-lookup"><span data-stu-id="af491-166">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="af491-167">Vedere [Creare e pubblicare un pacchetto](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="af491-167">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="af491-168">**Sono disponibili più versioni di una libreria destinate a versioni diverse di .NET Framework. Qual è la procedura per compilare un singolo pacchetto che supporti questo scenario?**</span><span class="sxs-lookup"><span data-stu-id="af491-168">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="af491-169">Vedere [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="af491-169">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="af491-170">**Qual è la procedura per configurare un repository o un feed personale?**</span><span class="sxs-lookup"><span data-stu-id="af491-170">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="af491-171">Vedere la [panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="af491-171">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="af491-172">**Qual è la procedura per caricare i pacchetti per il feed di NuGet in blocco?**</span><span class="sxs-lookup"><span data-stu-id="af491-172">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="af491-173">Vedere [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Pubblicazione in blocco di pacchetti NuGet) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="af491-173">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="af491-174">Utilizzo dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="af491-174">Working with packages</span></span>

<span data-ttu-id="af491-175">**Qual è la differenza tra un pacchetto a livello di progetto e un pacchetto a livello di soluzione?**</span><span class="sxs-lookup"><span data-stu-id="af491-175">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="af491-176">Un pacchetto a livello di soluzione (NuGet 3.x+) viene installato una sola volta in una soluzione e diventa quindi disponibile per tutti i progetti nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="af491-176">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="af491-177">Un pacchetto a livello di progetto viene installato in ogni progetto che lo usa.</span><span class="sxs-lookup"><span data-stu-id="af491-177">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="af491-178">Un pacchetto a livello di soluzione potrebbe anche installare nuovi comandi che possono essere chiamati dall'interno della console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="af491-178">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="af491-179">**È possibile installare i pacchetti NuGet senza connettività Internet?**</span><span class="sxs-lookup"><span data-stu-id="af491-179">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="af491-180">Sì, vedere il post di blog di Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Come accedere a NuGet quando il sito nuget.org non è disponibile oppure sei in aereo) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="af491-180">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="af491-181">**Qual è la procedura per installare i pacchetti in un percorso diverso rispetto alla cartella packages predefinita?**</span><span class="sxs-lookup"><span data-stu-id="af491-181">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="af491-182">Configurare l'impostazione [`repositoryPath`](../Schema/nuget-config-file.md#config-section) in `Nuget.Config` con `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="af491-182">Set the [`repositoryPath`](../Schema/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="af491-183">**Come è possibile evitare di aggiungere la cartella dei pacchetti NuGet nel controllo del codice sorgente?**</span><span class="sxs-lookup"><span data-stu-id="af491-183">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="af491-184">Impostare [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` su `true`.</span><span class="sxs-lookup"><span data-stu-id="af491-184">Set the [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="af491-185">Questa chiave funziona a livello di soluzione e quindi deve essere aggiunta al file `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="af491-185">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="af491-186">Quando si abilita il ripristino dei pacchetti da Visual Studio, questo file viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="af491-186">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="af491-187">**Qual è la procedura per disattivare il ripristino dei pacchetti?**</span><span class="sxs-lookup"><span data-stu-id="af491-187">**How do I turn off package restore?**</span></span>

<span data-ttu-id="af491-188">Vedere [Abilitazione e disabilitazione del ripristino dei pacchetti](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="af491-188">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="af491-189">**Perché viene visualizzato un errore "Non è possibile risolvere la dipendenza" durante l'installazione di un pacchetto locale con dipendenze remote?**</span><span class="sxs-lookup"><span data-stu-id="af491-189">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="af491-190">È necessario selezionare l'origine **Tutti** quando si installa un pacchetto locale nel progetto.</span><span class="sxs-lookup"><span data-stu-id="af491-190">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="af491-191">In questo modo vengono aggregati tutti i feed anziché usarne solo uno.</span><span class="sxs-lookup"><span data-stu-id="af491-191">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="af491-192">Il motivo per cui viene visualizzato questo errore è che gli utenti di un repository locale spesso vogliono evitare l'installazione accidentale di un pacchetto remoto a causa di criteri aziendali.</span><span class="sxs-lookup"><span data-stu-id="af491-192">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="af491-193">**Se sono disponibili più progetti nella stessa cartella, in che modo è possibile usare file packages.config separati per ogni progetto?**</span><span class="sxs-lookup"><span data-stu-id="af491-193">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="af491-194">Nella maggior parte dei progetti in cui progetti separati risiedono in cartelle separate, questo non costituisce un problema perché NuGet identifica i file `packages.config` in ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="af491-194">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="af491-195">Con NuGet 3.3 + e più progetti nella stessa cartella, è possibile inserire il nome del progetto nei nomi di file `packages.config` usando il modello `packages.{project-name}.config`, e NuGet usa tale file.</span><span class="sxs-lookup"><span data-stu-id="af491-195">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="af491-196">Questo non è un problema quando si usa PackageReference, perché ogni file di progetto contiene il proprio elenco di dipendenze.</span><span class="sxs-lookup"><span data-stu-id="af491-196">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="af491-197">**Se nuget.org non compare più nell'elenco dei repository, come è possibile ottenerlo di nuovo?**</span><span class="sxs-lookup"><span data-stu-id="af491-197">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="af491-198">Aggiungere `https://api.nuget.org/v3/index.json` all'elenco di origini, o</span><span class="sxs-lookup"><span data-stu-id="af491-198">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="af491-199">Eliminare `%appdata%\.nuget\NuGet.Config` in modo che NuGet lo crei di nuovo.</span><span class="sxs-lookup"><span data-stu-id="af491-199">Delete the `%appdata%\.nuget\NuGet.Config` and let NuGet re-create it.</span></span>

<span data-ttu-id="af491-200">**Quali sono le condizioni di licenza predefinite se un pacchetto non include informazioni di licenza specifiche?**</span><span class="sxs-lookup"><span data-stu-id="af491-200">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="af491-201">Ogni pacchetto è disciplinato dalle condizioni incluse nel pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af491-201">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="af491-202">È necessario leggere le condizioni applicabili prima di accedere, scaricare o acquisire qualsiasi pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af491-202">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="af491-203">In nuget.org, usare il collegamento **License Info** (Informazioni di licenza) nella pagina del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af491-203">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="af491-204">Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto su nuget.org.</span><span class="sxs-lookup"><span data-stu-id="af491-204">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="af491-205">Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile per le informazioni fornite da terze parti.</span><span class="sxs-lookup"><span data-stu-id="af491-205">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>


## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="af491-206">Gestione dei pacchetti in nuget.org</span><span class="sxs-lookup"><span data-stu-id="af491-206">Managing packages on nuget.org</span></span>

<span data-ttu-id="af491-207">**È possibile modificare i metadati del pacchetto dopo che è stato caricato? Per quale motivo si richiede di modificare il file nuspec e di caricare un nuovo pacchetto per apportare modifiche ai metadati del pacchetto?**</span><span class="sxs-lookup"><span data-stu-id="af491-207">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="af491-208">NuGet richiede che tutti i pacchetti siano firmati.</span><span class="sxs-lookup"><span data-stu-id="af491-208">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="af491-209">Uno dei principi di progettazione della firma dei pacchetti è che il contenuto del pacchetto firmato non deve essere modificabile e ciò include il file nuspec.</span><span class="sxs-lookup"><span data-stu-id="af491-209">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="af491-210">La modifica dei metadati del pacchetto comporta modifiche al file nuspec, invalidando le firme esistenti.</span><span class="sxs-lookup"><span data-stu-id="af491-210">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="af491-211">Si consiglia di modificare i flussi di lavoro esistenti in modo da non richiedere la modifica dei metadati del pacchetto dopo aver creato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af491-211">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="af491-212">Si noti che le dipendenze elencate per il pacchetto vengono generate automaticamente dal pacchetto stesso e non possono essere modificate.</span><span class="sxs-lookup"><span data-stu-id="af491-212">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="af491-213">Inoltre, il caricamento dei pacchetti in [staging.nuget.org](http://staging.nuget.org) è un ottimo modo per testare e convalidare il pacchetto senza rendere disponibile un pacchetto nella raccolta pubblica.</span><span class="sxs-lookup"><span data-stu-id="af491-213">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="af491-214">**È possibile riservare nomi per i pacchetti che verranno pubblicati in futuro?**</span><span class="sxs-lookup"><span data-stu-id="af491-214">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="af491-215">Sì.</span><span class="sxs-lookup"><span data-stu-id="af491-215">Yes.</span></span> <span data-ttu-id="af491-216">È possibile riservare ID per i pacchetti in [nuget.org](https://www.nuget.org/) richiedendo un prefisso per l'ID dei pacchetti per l'account.</span><span class="sxs-lookup"><span data-stu-id="af491-216">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="af491-217">Per richiedere un prefisso per l'ID dei pacchetti, inviare un messaggio di posta elettronica all'account (@) nuget.org con il nome visualizzato del proprietario del pacchetto e il prefisso richiesto.</span><span class="sxs-lookup"><span data-stu-id="af491-217">In order to request a package ID prefix, send mail to account (at) nuget.org with the package owner display name, and the requested package ID prefix.</span></span>  

<span data-ttu-id="af491-218">**Come è possibile ottenere l'attestazione di proprietà per i pacchetti?**</span><span class="sxs-lookup"><span data-stu-id="af491-218">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="af491-219">Vedere [Gestione dei proprietari dei pacchetti in nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="af491-219">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="af491-220">**Qual è la procedura per gestire il caso di un proprietario di pacchetto che viola una licenza di software?**</span><span class="sxs-lookup"><span data-stu-id="af491-220">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="af491-221">Microsoft incoraggia la collaborazione tra i membri della community di NuGet per risolvere eventuali controversie tra i proprietari di pacchetti e i proprietari di altro software.</span><span class="sxs-lookup"><span data-stu-id="af491-221">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="af491-222">È stato elaborato un [processo di risoluzione delle controversie](../policies/dispute-resolution.md) da seguire prima di chiedere l'intercessione degli amministratori di nuget.org.</span><span class="sxs-lookup"><span data-stu-id="af491-222">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="af491-223">**È consigliabile caricare i pacchetti di test in nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="af491-223">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="af491-224">Per scopi di test, è possibile usare [staging.nuget.org](http://staging.nuget.org) o server NuGet pubblici alternativi, come [myget.org](https://myget.org) o [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="af491-224">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="af491-225">Si noti che i pacchetti caricati in staging.nuget.org potrebbero non essere conservati.</span><span class="sxs-lookup"><span data-stu-id="af491-225">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="af491-226">Vedere [Goodbye preview.nuget.org](http://blog.nuget.org/20130419/goodbye-preview.html) (Addio preview.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="af491-226">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="af491-227">**Quali sono le dimensioni massime per i pacchetti che è possibile caricare in nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="af491-227">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="af491-228">nuget.org consente pacchetti fino a 250 MB, ma è consigliabile mantenere dimensioni inferiori a 1 MB per i pacchetti se possibile e usare le dipendenze per collegare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="af491-228">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="af491-229">Come regola generale, i pacchetti contengono un solo assembly per evitare conflitti.</span><span class="sxs-lookup"><span data-stu-id="af491-229">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="af491-230">NuGet usa HTTP per scaricare i pacchetti, pertanto per i pacchetti di dimensioni maggiori sono più probabili errori di installazione rispetto a quelli più piccoli.</span><span class="sxs-lookup"><span data-stu-id="af491-230">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="af491-231">È possibile condividere le dipendenze tra più pacchetti, riducendo le dimensioni totali del download per i consumer dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="af491-231">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="af491-232">Le dipendenze sono prevalentemente statiche e non cambiano mai.</span><span class="sxs-lookup"><span data-stu-id="af491-232">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="af491-233">Quando si corregge un bug nel codice, è possibile che non occorra aggiornare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="af491-233">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="af491-234">Se si aggregano le dipendenze, alla fine diventa necessario ripubblicare ogni volta pacchetti più grandi.</span><span class="sxs-lookup"><span data-stu-id="af491-234">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="af491-235">Suddividendo i pacchetti NuGet in dipendenze correlate, gli aggiornamenti sono molto più selezionati per i consumer del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="af491-235">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="af491-236">nuget.org non accessibile</span><span class="sxs-lookup"><span data-stu-id="af491-236">nuget.org not accessible</span></span>

<span data-ttu-id="af491-237">**Perché non è possibile scaricare o caricare pacchetti in nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="af491-237">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="af491-238">Verificare innanzitutto di usare le versioni più recenti di NuGet.</span><span class="sxs-lookup"><span data-stu-id="af491-238">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="af491-239">Se il problema persiste anche con la versione più recente, [contattare il supporto tecnico](https://www.nuget.org/policies/Contact) e fornire informazioni aggiuntive per la risoluzione del problema di connessione, tra cui:</span><span class="sxs-lookup"><span data-stu-id="af491-239">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="af491-240">Versione di NuGet in uso</span><span class="sxs-lookup"><span data-stu-id="af491-240">The version of NuGet you're using</span></span>
- <span data-ttu-id="af491-241">Origini dei pacchetti in uso</span><span class="sxs-lookup"><span data-stu-id="af491-241">The package sources you're using</span></span>
- <span data-ttu-id="af491-242">Log di ripristino con livello di dettaglio massimo</span><span class="sxs-lookup"><span data-stu-id="af491-242">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="af491-243">Tracce MTR o Fiddler (vedere più avanti)</span><span class="sxs-lookup"><span data-stu-id="af491-243">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="af491-244">Area geografica</span><span class="sxs-lookup"><span data-stu-id="af491-244">Your geographical area</span></span>
- <span data-ttu-id="af491-245">Versione del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="af491-245">Your operating system version</span></span>
- <span data-ttu-id="af491-246">Configurazione del computer (CPU, rete, disco rigido)</span><span class="sxs-lookup"><span data-stu-id="af491-246">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="af491-247">Se il computer è protetto da proxy o firewall</span><span class="sxs-lookup"><span data-stu-id="af491-247">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="af491-248">Versioni di .NET installate nel computer</span><span class="sxs-lookup"><span data-stu-id="af491-248">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="af491-249">Versioni di strumenti multipiattaforma in uso, ad esempio interfaccia della riga di comando di .NET o DNU</span><span class="sxs-lookup"><span data-stu-id="af491-249">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="af491-250">*Per acquisire una traccia MTR:*</span><span class="sxs-lookup"><span data-stu-id="af491-250">*To capture MTR:*</span></span>

- <span data-ttu-id="af491-251">Scaricare WinMTR da [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="af491-251">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="af491-252">Immettere `api.nuget.org` come nome host e fare clic su **Start** (Avvia).</span><span class="sxs-lookup"><span data-stu-id="af491-252">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="af491-253">Attendere fino a quando il valore indicato nella colonna **Sent** (Inviati) è > = 100.</span><span class="sxs-lookup"><span data-stu-id="af491-253">Wait until the **Sent** column is >= 100.</span></span>

    ![Acquisizione di una traccia MTR](media/mtr.png)

- <span data-ttu-id="af491-255">Copiare il testo negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="af491-255">Copy text to clipboard.</span></span>

<span data-ttu-id="af491-256">*Per acquisire una traccia Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="af491-256">*To capture Fiddler:*</span></span>

- <span data-ttu-id="af491-257">Installare la versione più recente di [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="af491-257">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="af491-258">Avviare Fiddler e disabilitare l'acquisizione del traffico tramite il menu **File > Capture Traffic** (File > Acquisisci traffico).</span><span class="sxs-lookup"><span data-stu-id="af491-258">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="af491-259">Rimuovere tutte le sessioni (selezionare tutti gli elementi nell'elenco e premere **CANC**).</span><span class="sxs-lookup"><span data-stu-id="af491-259">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="af491-260">Configurare Fiddler per acquisire il traffico HTTPS selezionando **Decrypt HTTPS traffic** (Decrittografa traffico HTTPS) nella scheda **HTTPS** nel menu **Tools > Fiddler Options** (Strumenti > Opzioni Fiddler).</span><span class="sxs-lookup"><span data-stu-id="af491-260">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="af491-261">Chiudere Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="af491-261">Close Visual Studio.</span></span>
- <span data-ttu-id="af491-262">Abilitare il menu **File > Capture Traffic** (File > Acquisisci traffico).</span><span class="sxs-lookup"><span data-stu-id="af491-262">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="af491-263">Avviare Visual Studio o nuget.exe ed eseguire le azioni che non funzionano.</span><span class="sxs-lookup"><span data-stu-id="af491-263">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="af491-264">Il traffico generato da queste azioni dovrebbe essere visualizzato in Fiddler.</span><span class="sxs-lookup"><span data-stu-id="af491-264">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="af491-265">Dopo aver eseguito le azioni, usare **File > Save > All Sessions** (File > Salva > Tutte le sessioni) per archiviare le sessioni acquisite.</span><span class="sxs-lookup"><span data-stu-id="af491-265">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="af491-266">Nota: può essere richiesto di impostare la variabile di ambiente `HTTP_PROXY` su `http://127.0.0.1:8888` per il routing del traffico NuGet attraverso Fiddler.</span><span class="sxs-lookup"><span data-stu-id="af491-266">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="af491-267">Se il problema persiste, provare i [suggerimenti indicati in questo post di StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="af491-267">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="af491-268">**Quali sono gli endpoint API per nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="af491-268">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="af491-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Si noti che l'API V2 è deprecata e non funziona con NuGet 4+.)</span><span class="sxs-lookup"><span data-stu-id="af491-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
