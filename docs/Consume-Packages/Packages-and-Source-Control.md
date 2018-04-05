---
title: Pacchetti NuGet e controllo del codice sorgente | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Considerazioni sulle modalità di gestione dei pacchetti NuGet all'interno di sistemi di controllo della versione e di controllo del codice sorgente e su come omettere i pacchetti con Git e il controllo della versione di Team Foundation.
keywords: Controllo del codice sorgente NuGet, controllo della versione NuGet, NuGet e Git, NuGet e TFS, NuGet e il controllo della versione di Team Foundation, omissione di pacchetti, repository di controllo del codice sorgente, repository di controllo della versione
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 43fc1653616091b0f974903147645c0c99c8f57b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="omitting-nuget-packages-in-source-control-systems"></a><span data-ttu-id="9cff0-104">Omissione di pacchetti NuGet nei sistemi di controllo del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="9cff0-104">Omitting NuGet packages in source control systems</span></span>

<span data-ttu-id="9cff0-105">Gli sviluppatori omettono in genere i pacchetti NuGet nei repository di controllo del codice sorgente e si affidano invece al [ripristino dei pacchetti](package-restore.md) per reinstallare le dipendenze di un progetto prima di una compilazione.</span><span class="sxs-lookup"><span data-stu-id="9cff0-105">Developers typically omit NuGet packages from their source control repositories and rely instead on [package restore](package-restore.md) to reinstall a project's dependencies before a build.</span></span>

<span data-ttu-id="9cff0-106">Di seguito sono indicati i motivi validi per affidarsi al ripristino dei pacchetti:</span><span class="sxs-lookup"><span data-stu-id="9cff0-106">The reasons for relying on package restore include the following:</span></span>

1. <span data-ttu-id="9cff0-107">I sistemi di controllo della versione distribuiti, come Git, includono copie complete di ogni versione di ogni file all'interno del repository.</span><span class="sxs-lookup"><span data-stu-id="9cff0-107">Distributed version control systems, such as Git, include full copies of every version of every file within the repository.</span></span> <span data-ttu-id="9cff0-108">I file binari che vengono aggiornati di frequente causano aumenti notevoli delle dimensioni del repository e prolungano il tempo necessario per la sua clonazione.</span><span class="sxs-lookup"><span data-stu-id="9cff0-108">Binary files that are frequently updated lead to significant bloat and lengthens the time it takes to clone the repository.</span></span>
1. <span data-ttu-id="9cff0-109">Quando i pacchetti vengono inclusi nel repository, gli sviluppatori sono tenuti ad aggiungere i riferimenti direttamente al contenuto del pacchetto su disco anziché fare riferimento ai pacchetti tramite NuGet, e ciò può portare a nomi di percorso hardcoded nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9cff0-109">When packages are included in the repository, developers are liable to add references directly to package contents on disk rather than referencing packages through NuGet, which can lead to hard-coded path names in the project.</span></span>
1. <span data-ttu-id="9cff0-110">Diventa più difficile ripulire la soluzione da eventuali cartelle di pacchetti inutilizzate, perché è necessario accertarsi di non eliminare eventuali cartelle di pacchetti ancora in uso.</span><span class="sxs-lookup"><span data-stu-id="9cff0-110">It becomes harder to clean your solution of any unused package folders, as you need to ensure you don't delete any package folders still in use.</span></span>
1. <span data-ttu-id="9cff0-111">L'omissione dei pacchetti consente di mantenere limiti di proprietà ben definiti tra il proprio codice e i pacchetti di altri da cui si dipende.</span><span class="sxs-lookup"><span data-stu-id="9cff0-111">By omitting packages, you maintain clean boundaries of ownership between your code and the packages from others that you depend upon.</span></span> <span data-ttu-id="9cff0-112">Molti pacchetti NuGet vengono già gestiti in repository di controllo del codice sorgente specifici.</span><span class="sxs-lookup"><span data-stu-id="9cff0-112">Many NuGet packages are maintained in their own source control repositories already.</span></span>

<span data-ttu-id="9cff0-113">Anche se il ripristino dei pacchetti è il comportamento predefinito con NuGet, sono necessari alcuni interventi manuali per omettere i pacchetti dal controllo del codice sorgente, nello specifico la cartella `packages`, come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="9cff0-113">Although package restore is the default behavior with NuGet, some manual work is necessary to omit packages&mdash;namely, the `packages` folder in your project&mdash;from source control, as described in this article.</span></span>

## <a name="omitting-packages-with-git"></a><span data-ttu-id="9cff0-114">Omissione di pacchetti con Git</span><span class="sxs-lookup"><span data-stu-id="9cff0-114">Omitting packages with Git</span></span>

<span data-ttu-id="9cff0-115">Usare il [file con estensione gitignore](https://git-scm.com/docs/gitignore) per ignorare i pacchetti NuGet (`.nupkg`) la cartella `packages` e `project.assets.json`, tra le altre cose.</span><span class="sxs-lookup"><span data-stu-id="9cff0-115">Use the [.gitignore file](https://git-scm.com/docs/gitignore) to ignore NuGet packages (`.nupkg`) the `packages` folder, and `project.assets.json`, among other things.</span></span> <span data-ttu-id="9cff0-116">Per riferimento, vedere l'[esempio`.gitignore` per i progetti di Visual Studio](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span><span class="sxs-lookup"><span data-stu-id="9cff0-116">For reference, see the [sample `.gitignore` for Visual Studio projects](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore):</span></span>

<span data-ttu-id="9cff0-117">Le parti importanti del file `.gitignore` sono:</span><span class="sxs-lookup"><span data-stu-id="9cff0-117">The important parts of the `.gitignore` file are:</span></span>

```gitignore
# Ignore NuGet Packages
*.nupkg

# The packages folder can be ignored because of Package Restore
**/[Pp]ackages/*

# except build/, which is used as an MSBuild target.
!**/[Pp]ackages/build/

# Uncomment if necessary however generally it will be regenerated when needed
#!**/[Pp]ackages/repositories.config

# NuGet v3's project.json files produces more ignorable files
*.nuget.props
*.nuget.targets

# Ignore other intermediate files that NuGet might create. project.lock.json is used in conjunction
# with project.json (NuGet v3); project.assets.json is used in conjunction with the PackageReference
# format (NuGet v4 and .NET Core).
project.lock.json
project.assets.json
```

## <a name="omitting-packages-with-team-foundation-version-control"></a><span data-ttu-id="9cff0-118">Omissione dei pacchetti con il controllo della versione di Team Foundation</span><span class="sxs-lookup"><span data-stu-id="9cff0-118">Omitting packages with Team Foundation Version Control</span></span>

> [!Note]
> <span data-ttu-id="9cff0-119">Se possibile, seguire queste istruzioni *prima* di aggiungere il progetto al controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="9cff0-119">Follow these instructions if possible *before* adding your project to source control.</span></span> <span data-ttu-id="9cff0-120">In caso contrario, eliminare manualmente la cartella `packages` dal repository e archiviare la modifica prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="9cff0-120">Otherwise, manually delete the `packages` folder from your repository and check in that change before continuing.</span></span>

<span data-ttu-id="9cff0-121">Per disabilitare l'integrazione del controllo del codice sorgente con il controllo della versione di Team Foundation per una selezione di file:</span><span class="sxs-lookup"><span data-stu-id="9cff0-121">To disable source control integration with TFVC for selected files:</span></span>

1. <span data-ttu-id="9cff0-122">Creare una cartella denominata `.nuget` nella cartella della soluzione (dove si trova il file `.sln`).</span><span class="sxs-lookup"><span data-stu-id="9cff0-122">Create a folder called `.nuget` in your solution folder (where the `.sln` file is).</span></span>
    - <span data-ttu-id="9cff0-123">Suggerimento: in Windows, per creare la cartella in Esplora risorse usare il nome `.nuget.` *con* il punto finale.</span><span class="sxs-lookup"><span data-stu-id="9cff0-123">Tip: on Windows, to create this folder in Windows Explorer, use the name `.nuget.` *with* the trailing dot.</span></span>

1. <span data-ttu-id="9cff0-124">In questa cartella creare un file denominato `NuGet.Config` e aprirlo per la modifica.</span><span class="sxs-lookup"><span data-stu-id="9cff0-124">In that folder, create a file named `NuGet.Config` and open it for editing.</span></span>

1. <span data-ttu-id="9cff0-125">Aggiungere come minimo il testo seguente, in cui l'impostazione [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) indica a Visual Studio di ignorare tutti gli elementi nella cartella `packages`:</span><span class="sxs-lookup"><span data-stu-id="9cff0-125">Add the following text as a minimum, where the [disableSourceControlIntegration](../reference/nuget-config-file.md#solution-section) setting instructs Visual Studio to skip everything in the `packages` folder:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
       <solution>
           <add key="disableSourceControlIntegration" value="true" />
       </solution>
   </configuration>
   ```

1. <span data-ttu-id="9cff0-126">Se si usa TFS 2010 o versioni precedenti, mascherare la cartella `packages` nei mapping dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="9cff0-126">If you are using TFS 2010 or earlier, cloak the `packages` folder in your workspace mappings.</span></span>

1. <span data-ttu-id="9cff0-127">In TFS 2012 o versione successiva oppure con Visual Studio Team Services, creare un file `.tfignore` come descritto in [Add files to the server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore) (Aggiungere file al server).</span><span class="sxs-lookup"><span data-stu-id="9cff0-127">On TFS 2012 or later, or with Visual Studio Team Services, create a `.tfignore` file as described on [AddFiles to the Server](https://www.visualstudio.com/en-us/docs/tfvc/add-files-server#tfignore).</span></span> <span data-ttu-id="9cff0-128">In tale file, includere il contenuto seguente per ignorare in modo esplicito le modifiche per la cartella `\packages` a livello del repository e alcuni altri file intermedi.</span><span class="sxs-lookup"><span data-stu-id="9cff0-128">In that file, include the content below to explicitly ignore modifications to the `\packages` folder on the repository level and a few other intermediate files.</span></span> <span data-ttu-id="9cff0-129">È possibile creare il file in Esplora risorse usando il nome `.tfignore.` con il punto finale, ma potrebbe essere necessario disabilitare prima di tutto l'opzione per nascondere le estensioni di file conosciute:</span><span class="sxs-lookup"><span data-stu-id="9cff0-129">(You can create the file in Windows Explorer using the name a `.tfignore.` with the trailing dot, but you might need to disable the "Hide known file extensions" option first.):</span></span>

   ```cli
   # Ignore NuGet Packages
   *.nupkg

   # Ignore the NuGet packages folder in the root of the repository. If needed, prefix 'packages'
   # with additional folder names if it's not in the same folder as .tfignore.   
   packages

   # Exclude package target files which may be required for MSBuild, again prefixing the folder name as needed.
   !packages/*.targets

   # Omit temporary files
   project.lock.json
   project.assets.json
   *.nuget.props
   ```

1. <span data-ttu-id="9cff0-130">Aggiungere `NuGet.Config` e `.tfignore` al controllo del codice sorgente e archiviare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9cff0-130">Add `NuGet.Config` and `.tfignore` to source control and check in your changes.</span></span>
