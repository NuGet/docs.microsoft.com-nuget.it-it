---
title: Domande frequenti su NuGet
description: Domande frequenti e relative risposte per l'uso di NuGet dalla riga di comando e in Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: aae6f0474cc6e8e8aa5c269b79be6fd949d9184c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237997"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="9739b-103">Domande frequenti su NuGet</span><span class="sxs-lookup"><span data-stu-id="9739b-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="9739b-104">Per le domande frequenti relative a NuGet.org, ad esempio domande sull'account NuGet.org, vedere [Domande frequenti su NuGet.org](../nuget-org/nuget-org-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="9739b-105">**Che cos'è richiesto per eseguire NuGet?**</span><span class="sxs-lookup"><span data-stu-id="9739b-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="9739b-106">Tutte le informazioni sia sull'interfaccia utente che sugli strumenti da riga di comando sono disponibili in [Installazione degli strumenti client di NuGet](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="9739b-107">**NuGet supporta Mono?**</span><span class="sxs-lookup"><span data-stu-id="9739b-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="9739b-108">Lo strumento da riga di comando, `nuget.exe`, supporta l'esecuzione e la compilazione in Mono 3.2+ e consente di creare pacchetti in Mono.</span><span class="sxs-lookup"><span data-stu-id="9739b-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="9739b-109">Anche se `nuget.exe` funziona in modo ottimale in Windows, esistono alcuni problemi noti in Linux e OS X. Vedere i [problemi relativi a Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="9739b-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="9739b-110">È disponibile un [client grafico](https://github.com/mrward/monodevelop-nuget-addin) come componente aggiuntivo per MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="9739b-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="9739b-111">**Come è possibile determinare il contenuto di un pacchetto e se è stabile e utile per la mia applicazione?**</span><span class="sxs-lookup"><span data-stu-id="9739b-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="9739b-112">La fonte principale di informazioni su un pacchetto è la relativa pagina di presentazione in nuget.org (o un altro feed privato).</span><span class="sxs-lookup"><span data-stu-id="9739b-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="9739b-113">Ogni pagina di pacchetto in nuget.org include una descrizione del pacchetto, la cronologia delle versioni e le statistiche di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="9739b-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="9739b-114">La sezione **Info** nella pagina del pacchetto contiene anche un collegamento al sito Web del progetto in cui è in genere possibile trovare numerosi esempi e documentazione per scoprire di più su come viene usato il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9739b-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="9739b-115">Per altre informazioni, vedere [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="9739b-116">NuGet in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9739b-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="9739b-117">**Come viene supportato NuGet nei diversi prodotti Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="9739b-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="9739b-118">Visual Studio in Windows supporta l'[interfaccia utente di Gestione pacchetti](../consume-packages/install-use-packages-visual-studio.md) e la [console di Gestione pacchetti](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="9739b-119">Visual Studio per Mac include funzionalità incorporate di NuGet come descritto in [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="9739b-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="9739b-120">Visual Studio Code (tutte le piattaforme) non include alcuna integrazione diretta di NuGet.</span><span class="sxs-lookup"><span data-stu-id="9739b-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="9739b-121">Usare l'[interfaccia della riga di comando di NuGet](../reference/nuget-exe-cli-reference.md) o l'[interfaccia della riga di comando di dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="9739b-122">Azure DevOps offre [un passaggio di compilazione per il ripristino dei pacchetti NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="9739b-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="9739b-123">È anche possibile [ospitare feed di pacchetti NuGet privati in Azure DevOps](/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="9739b-123">You can also [host private NuGet package feeds on Azure DevOps](/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="9739b-124">**Come è possibile controllare la versione esatta degli strumenti di NuGet installati?**</span><span class="sxs-lookup"><span data-stu-id="9739b-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="9739b-125">In Visual Studio, usare il comando **Guida > informazioni su Microsoft Visual Studio** e controllare la versione visualizzata accanto a **Gestione pacchetti NuGet** .</span><span class="sxs-lookup"><span data-stu-id="9739b-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager** .</span></span>

<span data-ttu-id="9739b-126">In alternativa, avviare la console di Gestione pacchetti ( **Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti** ) e immettere `$host` per visualizzare informazioni su NuGet, compresa la versione.</span><span class="sxs-lookup"><span data-stu-id="9739b-126">Alternatively, launch the Package Manager Console ( **Tools > NuGet Package Manager > Package Manager Console** ) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="9739b-127">**Quali linguaggi di programmazione sono supportati da NuGet?**</span><span class="sxs-lookup"><span data-stu-id="9739b-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="9739b-128">NuGet funziona in generale per i linguaggi .NET ed è progettato per integrare le librerie .NET in un progetto.</span><span class="sxs-lookup"><span data-stu-id="9739b-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="9739b-129">Dato che supporta anche l'automazione di MSBuild e Visual Studio in alcuni tipi di progetto, sono supportati anche altri progetti e linguaggi a vari livelli.</span><span class="sxs-lookup"><span data-stu-id="9739b-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="9739b-130">La versione più recente di NuGet supporta C#, Visual Basic, F#, WiX e C++.</span><span class="sxs-lookup"><span data-stu-id="9739b-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="9739b-131">**Quali modelli di progetto sono supportati da NuGet?**</span><span class="sxs-lookup"><span data-stu-id="9739b-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="9739b-132">NuGet offre il supporto completo per un'ampia gamma di modelli di progetto come Windows, Web, Cloud, SharePoint, Wix e così via.</span><span class="sxs-lookup"><span data-stu-id="9739b-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="9739b-133">**Qual è la procedura per aggiornare i pacchetti che fanno parte di modelli di Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="9739b-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="9739b-134">Passare alla scheda **Aggiornamenti** nell'interfaccia utente di Gestione pacchetti e selezionare **Aggiorna tutto** oppure usare il [comando `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) dalla console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="9739b-134">Go to the **Updates** tab in the Package Manager UI and select **Update All** , or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="9739b-135">Per aggiornare il modello stesso, è necessario aggiornare manualmente il repository del modello.</span><span class="sxs-lookup"><span data-stu-id="9739b-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="9739b-136">Vedere il [blog di Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) su questo argomento.</span><span class="sxs-lookup"><span data-stu-id="9739b-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="9739b-137">Si noti che questa operazione viene eseguita a proprio rischio, poiché gli aggiornamenti manuali potrebbero danneggiare il modello, se le versioni più recenti di tutte le dipendenze non sono compatibili tra loro.</span><span class="sxs-lookup"><span data-stu-id="9739b-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="9739b-138">**È possibile usare NuGet all'esterno di Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="9739b-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="9739b-139">Sì, NuGet funziona direttamente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="9739b-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="9739b-140">Vedere la [guida all'installazione](../install-nuget-client-tools.md) e le [informazioni di riferimento sull'interfaccia della riga di comando](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="9739b-141">Riga di comando di NuGet</span><span class="sxs-lookup"><span data-stu-id="9739b-141">NuGet command line</span></span>

<span data-ttu-id="9739b-142">**Qual è la procedura per ottenere la versione più recente dello strumento da riga di comando di NuGet?**</span><span class="sxs-lookup"><span data-stu-id="9739b-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="9739b-143">Vedere la [guida all'installazione](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="9739b-144">Per controllare la versione installata corrente dello strumento, usare `nuget help`.</span><span class="sxs-lookup"><span data-stu-id="9739b-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="9739b-145">**Che cos'è la licenza per nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="9739b-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="9739b-146">È possibile ridistribuire nuget.exe ai sensi della licenza MIT.</span><span class="sxs-lookup"><span data-stu-id="9739b-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="9739b-147">L'utente è responsabile dell'aggiornamento e della manutenzione di qualsiasi copia di nuget.exe che si sceglie di ridistribuire.</span><span class="sxs-lookup"><span data-stu-id="9739b-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="9739b-148">**È possibile estendere lo strumento da riga di comando di NuGet?**</span><span class="sxs-lookup"><span data-stu-id="9739b-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="9739b-149">Sì, è possibile aggiungere comandi personalizzati a `nuget.exe`, come descritto nel [post di Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="9739b-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="9739b-150">Console di Gestione pacchetti Nuget (Visual Studio in Windows)</span><span class="sxs-lookup"><span data-stu-id="9739b-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="9739b-151">**Qual è la procedura per ottenere l'accesso all'oggetto DTE nella console di Gestione pacchetti**</span><span class="sxs-lookup"><span data-stu-id="9739b-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="9739b-152">L'oggetto di primo livello nel modello a oggetti di automazione di Visual Studio viene chiamato oggetto DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="9739b-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="9739b-153">La console rende disponibile questo oggetto tramite una variabile denominata `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="9739b-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="9739b-154">Per altre informazioni, vedere [Cenni preliminari sul modello di automazione](/visualstudio/extensibility/internals/automation-model-overview) nella documentazione sull'estendibilità di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9739b-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="9739b-155">**Si tenta di eseguire il cast della variabile $DTE al tipo DTE2, ma viene ricevuto un errore: Impossibile convertire il valore "EnvDTE. DTEClass" di tipo "EnvDTE. DTEClass" nel tipo "EnvDTE80. DTE2". Cosa c'è che non va?**</span><span class="sxs-lookup"><span data-stu-id="9739b-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="9739b-156">Si tratta di un problema noto correlato alla modalità di interazione di PowerShell con un oggetto COM.</span><span class="sxs-lookup"><span data-stu-id="9739b-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="9739b-157">Attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="9739b-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="9739b-158">`Get-Interface` è una funzione helper aggiunta dall'host di PowerShell di NuGet.</span><span class="sxs-lookup"><span data-stu-id="9739b-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="9739b-159">Creazione e pubblicazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="9739b-159">Creating and publishing packages</span></span>

<span data-ttu-id="9739b-160">**Qual è la procedura per presentare un pacchetto in un feed?**</span><span class="sxs-lookup"><span data-stu-id="9739b-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="9739b-161">Vedere [Creare e pubblicare un pacchetto](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="9739b-162">**Sono disponibili più versioni della libreria destinate a versioni diverse della .NET Framework. Ricerca per categorie compilare un singolo pacchetto che supporta questa operazione?**</span><span class="sxs-lookup"><span data-stu-id="9739b-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="9739b-163">Vedere [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="9739b-164">**Qual è la procedura per configurare un repository o un feed personale?**</span><span class="sxs-lookup"><span data-stu-id="9739b-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="9739b-165">Vedere la [panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="9739b-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="9739b-166">**Qual è la procedura per caricare i pacchetti per il feed di NuGet in blocco?**</span><span class="sxs-lookup"><span data-stu-id="9739b-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="9739b-167">Vedere [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Pubblicazione in blocco di pacchetti NuGet) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="9739b-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="9739b-168">Utilizzo dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="9739b-168">Working with packages</span></span>

<span data-ttu-id="9739b-169">**È possibile installare i pacchetti NuGet senza connettività Internet?**</span><span class="sxs-lookup"><span data-stu-id="9739b-169">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="9739b-170">Sì, vedere il post di blog di Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Come accedere a NuGet quando il sito nuget.org non è disponibile oppure sei in aereo) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="9739b-170">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="9739b-171">**Qual è la procedura per installare i pacchetti in un percorso diverso rispetto alla cartella packages predefinita?**</span><span class="sxs-lookup"><span data-stu-id="9739b-171">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="9739b-172">Impostare l' [`repositoryPath`](../reference/nuget-config-file.md#config-section) impostazione in `Nuget.Config` utilizzando `nuget config -set repositoryPath=<path>` .</span><span class="sxs-lookup"><span data-stu-id="9739b-172">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="9739b-173">**Come è possibile evitare di aggiungere la cartella dei pacchetti NuGet nel controllo del codice sorgente?**</span><span class="sxs-lookup"><span data-stu-id="9739b-173">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="9739b-174">Impostare [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` su `true` .</span><span class="sxs-lookup"><span data-stu-id="9739b-174">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="9739b-175">Questa chiave funziona a livello di soluzione e quindi deve essere aggiunta al file `$(Solutiondir)\.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="9739b-175">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="9739b-176">Quando si abilita il ripristino dei pacchetti da Visual Studio, questo file viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9739b-176">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="9739b-177">**Qual è la procedura per disattivare il ripristino dei pacchetti?**</span><span class="sxs-lookup"><span data-stu-id="9739b-177">**How do I turn off package restore?**</span></span>

<span data-ttu-id="9739b-178">Vedere [Abilitazione e disabilitazione del ripristino dei pacchetti](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="9739b-178">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="9739b-179">**Perché viene visualizzato un errore "Non è possibile risolvere la dipendenza" durante l'installazione di un pacchetto locale con dipendenze remote?**</span><span class="sxs-lookup"><span data-stu-id="9739b-179">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="9739b-180">È necessario selezionare l'origine **Tutti** quando si installa un pacchetto locale nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9739b-180">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="9739b-181">In questo modo vengono aggregati tutti i feed anziché usarne solo uno.</span><span class="sxs-lookup"><span data-stu-id="9739b-181">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="9739b-182">Il motivo per cui viene visualizzato questo errore è che gli utenti di un repository locale spesso vogliono evitare l'installazione accidentale di un pacchetto remoto a causa di criteri aziendali.</span><span class="sxs-lookup"><span data-stu-id="9739b-182">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="9739b-183">**Se sono disponibili più progetti nella stessa cartella, in che modo è possibile usare file packages.config separati per ogni progetto?**</span><span class="sxs-lookup"><span data-stu-id="9739b-183">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="9739b-184">Nella maggior parte dei progetti in cui progetti separati risiedono in cartelle separate, questo non costituisce un problema perché NuGet identifica i file `packages.config` in ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="9739b-184">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="9739b-185">Con NuGet 3.3 + e più progetti nella stessa cartella, è possibile inserire il nome del progetto nei nomi di file `packages.config` usando il modello `packages.{project-name}.config`, e NuGet usa tale file.</span><span class="sxs-lookup"><span data-stu-id="9739b-185">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="9739b-186">Questo non è un problema quando si usa PackageReference, perché ogni file di progetto contiene il proprio elenco di dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9739b-186">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="9739b-187">**Se nuget.org non compare più nell'elenco dei repository, come è possibile ottenerlo di nuovo?**</span><span class="sxs-lookup"><span data-stu-id="9739b-187">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="9739b-188">Aggiungere `https://api.nuget.org/v3/index.json` all'elenco di origini, o</span><span class="sxs-lookup"><span data-stu-id="9739b-188">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="9739b-189">Eliminare `%appdata%\.nuget\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e consentire a NuGet di ricrearlo.</span><span class="sxs-lookup"><span data-stu-id="9739b-189">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>