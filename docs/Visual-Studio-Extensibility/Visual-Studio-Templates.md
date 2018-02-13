---
title: Pacchetti NuGet nei modelli di Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/03/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Istruzioni per includere i pacchetti NuGet nei modelli di progetto e di elemento di Visual Studio.
keywords: NuGet in Visual Studio, modelli di progetto di Visual Studio, modelli di elemento di Visual Studio, pacchetti nei modelli di progetto, pacchetti nei modelli di elemento
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65b914e1fa59c28615f195b470880a12bf80efbb
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/02/2018
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="267f7-104">Pacchetti nei modelli di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="267f7-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="267f7-105">I modelli di progetto e di elemento di Visual Studio spesso hanno bisogno della garanzia che determinati pacchetti siano installati quando viene creato il progetto o l'elemento.</span><span class="sxs-lookup"><span data-stu-id="267f7-105">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="267f7-106">Ad esempio, il modello ASP.NET MVC 3 installa jQuery, Modernizr e altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="267f7-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="267f7-107">A supporto di questa funzionalità, gli autori di modelli possono indicare a NuGet di installare i pacchetti necessari, anziché singole librerie.</span><span class="sxs-lookup"><span data-stu-id="267f7-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="267f7-108">Gli sviluppatori possono quindi aggiornare facilmente tali pacchetti in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="267f7-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="267f7-109">Per altre informazioni sulla creazione dei modelli, fare riferimento a [Procedura: Creare modelli di progetto](/visualstudio/ide/how-to-create-project-templates) o [Creazione di modelli di progetto e di elemento personalizzati](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="267f7-109">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="267f7-110">Il resto di questa sezione descrive i passaggi specifici da eseguire durante la creazione di un modello per includere correttamente i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="267f7-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="267f7-111">Aggiunta di pacchetti a un modello</span><span class="sxs-lookup"><span data-stu-id="267f7-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="267f7-112">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="267f7-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="267f7-113">Per un esempio, vedere l'[esempio NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="267f7-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="267f7-114">Aggiunta di pacchetti a un modello</span><span class="sxs-lookup"><span data-stu-id="267f7-114">Adding packages to a template</span></span>

<span data-ttu-id="267f7-115">Quando viene creata un'istanza di un modello, viene richiamata una [creazione guidata di modelli](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) per caricare l'elenco dei pacchetti da installare insieme alle informazioni su dove trovare tali pacchetti.</span><span class="sxs-lookup"><span data-stu-id="267f7-115">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="267f7-116">I pacchetti possono essere incorporati in VSIX, incorporati nel modello o situati sul disco rigido locale, nel qual caso viene usata una chiave del Registro di sistema per fare riferimento al percorso del file.</span><span class="sxs-lookup"><span data-stu-id="267f7-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="267f7-117">Informazioni dettagliate su questi percorsi sono disponibili più avanti in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="267f7-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="267f7-118">I pacchetti preinstallati funzionano tramite [creazioni guidate di modelli](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="267f7-118">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="267f7-119">Viene richiamata una speciale procedura guidata quando viene creata l'istanza del modello.</span><span class="sxs-lookup"><span data-stu-id="267f7-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="267f7-120">La procedura guidata carica l'elenco dei pacchetti che devono essere installati e passa le informazioni alle API NuGet appropriate.</span><span class="sxs-lookup"><span data-stu-id="267f7-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="267f7-121">Passaggi per includere i pacchetti in un modello:</span><span class="sxs-lookup"><span data-stu-id="267f7-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="267f7-122">Nel file `vstemplate` aggiungere un riferimento alla creazione guidata di modelli di NuGet aggiungendo un elemento [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates):</span><span class="sxs-lookup"><span data-stu-id="267f7-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="267f7-123">`NuGet.VisualStudio.Interop.dll` è un assembly che contiene solo la classe `TemplateWizard`, che è un semplice wrapper che chiama l'implementazione effettiva in `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="267f7-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="267f7-124">La versione dell'assembly non verrà mai modificata, pertanto i modelli di progetto/elemento continuano a funzionare con le nuove versioni di NuGet.</span><span class="sxs-lookup"><span data-stu-id="267f7-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="267f7-125">Aggiungere l'elenco dei pacchetti da installare nel progetto:</span><span class="sxs-lookup"><span data-stu-id="267f7-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="267f7-126">*(NuGet 2.2.1+)* La procedura guidata supporta più elementi `<package>` per supportare più origini dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="267f7-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="267f7-127">Sono richiesti entrambi gli attributi `id` e `version`, il che significa che una versione specifica di un pacchetto verrà installata anche se è disponibile una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="267f7-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="267f7-128">Ciò impedisce agli aggiornamenti pacchetto di interrompere il modello, lasciando la scelta di aggiornare il pacchetto allo sviluppatore che usa il modello.</span><span class="sxs-lookup"><span data-stu-id="267f7-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="267f7-129">Specificare il repository dove NuGet può dove trovare i pacchetti come descritto nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="267f7-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="267f7-130">Repository di pacchetti VSIX</span><span class="sxs-lookup"><span data-stu-id="267f7-130">VSIX package repository</span></span>

<span data-ttu-id="267f7-131">L'approccio di distribuzione consigliato per i modelli di progetto/elemento di Visual Studio è un'[estensione VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) perché consente di inserire in un pacchetto più modelli di progetto/elemento e permette agli sviluppatori di individuare facilmente i modelli usando Gestione estensioni di Visual Studio o Visual Studio Gallery.</span><span class="sxs-lookup"><span data-stu-id="267f7-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="267f7-132">Anche gli aggiornamenti all'estensione sono facili da distribuire tramite il [meccanismo di aggiornamento automatico di Gestione estensioni di Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="267f7-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="267f7-133">VSIX può fungere da origine per i pacchetti richiesta dal modello:</span><span class="sxs-lookup"><span data-stu-id="267f7-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="267f7-134">Modificare l'elemento `<packages>` nel file `.vstemplate` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="267f7-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="267f7-135">L'attributo `repository` specifica il tipo di repository come `extension` mentre `repositoryId` è l'identificatore univoco di VSIX, ovvero il valore dell'attributo `ID` nel file `vsixmanifest` dell'estensione. Vedere [Riferimenti su VSIX Extension Schema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference).</span><span class="sxs-lookup"><span data-stu-id="267f7-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="267f7-136">Inserire i file `nupkg` in una cartella chiamata `Packages` all'interno di VSIX.</span><span class="sxs-lookup"><span data-stu-id="267f7-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="267f7-137">Aggiungere i file di pacchetto necessari come `<Asset>` nel file `vsixmanifest`. Vedere [Riferimenti su VSIX Extension Schema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference):</span><span class="sxs-lookup"><span data-stu-id="267f7-137">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="267f7-138">Si noti che è possibile distribuire i pacchetti nello stesso VSIX dei modelli di progetto oppure è possibile inserirli in un VSIX distinto, se più opportuno per lo specifico scenario.</span><span class="sxs-lookup"><span data-stu-id="267f7-138">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="267f7-139">Tuttavia, non fare riferimento ad alcun VSIX su cui non si ha controllo, perché le modifiche apportate a tale estensione potrebbero interrompere il modello.</span><span class="sxs-lookup"><span data-stu-id="267f7-139">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="267f7-140">Repository di pacchetti di modello</span><span class="sxs-lookup"><span data-stu-id="267f7-140">Template package repository</span></span>

<span data-ttu-id="267f7-141">Se si distribuisce solo un singolo modello di progetto/elemento e non è necessario inserire più modelli in un pacchetto, è possibile ricorrere a un approccio più semplice ma più limitato che include i pacchetti direttamente nel file ZIP del modello di progetto/elemento:</span><span class="sxs-lookup"><span data-stu-id="267f7-141">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="267f7-142">Modificare l'elemento `<packages>` nel file `.vstemplate` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="267f7-142">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="267f7-143">L'attributo `repository` ha il valore `template` e l'attributo `repositoryId` non è richiesto.</span><span class="sxs-lookup"><span data-stu-id="267f7-143">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="267f7-144">Inserire i pacchetti nella cartella radice del file ZIP del modello di progetto/elemento.</span><span class="sxs-lookup"><span data-stu-id="267f7-144">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="267f7-145">Si noti che l'uso di questo approccio in un VSIX che contiene più modelli comporta un aumento eccessivo non necessario quando uno o più pacchetti sono comuni per i modelli.</span><span class="sxs-lookup"><span data-stu-id="267f7-145">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="267f7-146">In tali casi, usare [VSIX come repository](#vsix-package-repository) come descritto nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="267f7-146">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="267f7-147">Percorso della cartella specificato dal Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="267f7-147">Registry-specified folder path</span></span>

<span data-ttu-id="267f7-148">Gli SDK che vengono installati tramite un file MSI possono installare i pacchetti NuGet direttamente nel computer dello sviluppatore.</span><span class="sxs-lookup"><span data-stu-id="267f7-148">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="267f7-149">In questo modo si rendono immediatamente disponibili quando viene usato un modello di progetto o di elemento, anziché doverli estrarre in quella fase.</span><span class="sxs-lookup"><span data-stu-id="267f7-149">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="267f7-150">I modelli ASP.NET usano questo approccio.</span><span class="sxs-lookup"><span data-stu-id="267f7-150">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="267f7-151">Fare in modo che il file MSI installi i pacchetti nel computer.</span><span class="sxs-lookup"><span data-stu-id="267f7-151">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="267f7-152">È possibile installare solo i file `.nupkg` oppure è possibile installarli insieme al contenuto espanso, che consente di risparmiare un ulteriore passaggio quando viene usato il modello.</span><span class="sxs-lookup"><span data-stu-id="267f7-152">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="267f7-153">In questo caso, seguire la struttura di cartelle standard di NuGet in cui i file `.nupkg` si trovano nella cartella radice e quindi ogni pacchetto dispone di una sottocartella con la coppia ID/versione come nome della sottocartella.</span><span class="sxs-lookup"><span data-stu-id="267f7-153">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="267f7-154">Scrivere una chiave del Registro di sistema per identificare il percorso del pacchetto:</span><span class="sxs-lookup"><span data-stu-id="267f7-154">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="267f7-155">Percorso della chiave: `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` a livello di computer o, in caso di pacchetti e modelli installati per utente, usare in alternativa `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.</span><span class="sxs-lookup"><span data-stu-id="267f7-155">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="267f7-156">Nome della chiave: usare un nome univoco per l'utente.</span><span class="sxs-lookup"><span data-stu-id="267f7-156">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="267f7-157">Ad esempio, i modelli ASP.NET MVC 4 per Visual Studio 2012 usano `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="267f7-157">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="267f7-158">Valori: percorso completo della cartella dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="267f7-158">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="267f7-159">Nell'elemento `<packages>` nel file `.vstemplate` aggiungere l'attributo `repository="registry"` e specificare il nome della chiave del Registro di sistema nell'attributo `keyName`.</span><span class="sxs-lookup"><span data-stu-id="267f7-159">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="267f7-160">Se i pacchetti sono già stati decompressi in precedenza, usare l'attributo `isPreunzipped="true"`.</span><span class="sxs-lookup"><span data-stu-id="267f7-160">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="267f7-161">*(NuGet 3.2+)* Se si vuole forzare una compilazione in fase di progettazione al termine dell'installazione del pacchetto, aggiungere l'attributo `forceDesignTimeBuild="true"`.</span><span class="sxs-lookup"><span data-stu-id="267f7-161">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="267f7-162">Come ottimizzazione, aggiungere `skipAssemblyReferences="true"` perché il modello stesso include già i riferimenti necessari.</span><span class="sxs-lookup"><span data-stu-id="267f7-162">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="267f7-163">Suggerimenti</span><span class="sxs-lookup"><span data-stu-id="267f7-163">Best Practices</span></span>

1. <span data-ttu-id="267f7-164">Dichiarare una dipendenza da VSIX di NuGet aggiungendo un riferimento a esso nel manifesto VSIX:</span><span class="sxs-lookup"><span data-stu-id="267f7-164">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="267f7-165">Richiedere il salvataggio dei modelli di progetto/elemento in fase di creazione includendo [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) nel file `.vstemplate`.</span><span class="sxs-lookup"><span data-stu-id="267f7-165">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="267f7-166">I modelli non includono un file `packages.config` e non includono riferimenti o contenuto che verrebbero aggiunti al momento dell'installazione dei i pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="267f7-166">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
