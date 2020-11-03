---
title: Gestire pacchetti NuGet tramite l'interfaccia della riga di comando di nuget.exe
description: Istruzioni per usare l'interfaccia della riga di comando di nuget.exe insieme a pacchetti NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237387"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="f0cf9-103">Gestire pacchetti tramite l'interfaccia della riga di comando nuget.exe</span><span class="sxs-lookup"><span data-stu-id="f0cf9-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="f0cf9-104">Lo strumento della riga di comando consente di aggiornare e ripristinare facilmente pacchetti NuGet in progetti e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="f0cf9-105">Questo strumento offre tutte le funzionalità di NuGet in Windows e anche la maggior parte delle funzionalità in Mac e Linux per l'esecuzione in Mono.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="f0cf9-106">L'interfaccia della riga di comando di `nuget.exe` viene usata per il progetto .NET Framework e per i progetti non di tipo SDK, ad esempio un progetto non di tipo SDK destinato alle librerie .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="f0cf9-107">Se si usa un progetto non di tipo SDK, di cui è stata eseguita la migrazione a `PackageReference`, usare invece l'interfaccia della riga di comando di `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="f0cf9-108">L'interfaccia della riga di comando di `nuget.exe` richiede un file [packages.config](../reference/packages-config.md) per i riferimenti ai pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="f0cf9-109">Nella maggior parte degli scenari è consigliabile [eseguire la migrazione dei progetti non di tipo SDK](../consume-packages/migrate-packages-config-to-package-reference.md) che usano `packages.config` a PackageReference, per poter poi usare l'interfaccia della riga di comando di `dotnet` anziché l'interfaccia della riga di comando di `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="f0cf9-110">La migrazione non è attualmente disponibile per i progetti C++ e ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="f0cf9-111">Questo articolo illustra l'utilizzo di base di alcuni dei comandi più comuni dell'interfaccia della riga di comando di `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="f0cf9-112">Per la maggior parte di questi comandi, lo strumento della riga di comando cerca un file di progetto nella directory corrente, a meno che non venga specificato un file di progetto nel comando.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="f0cf9-113">Per un elenco completo dei comandi e degli argomenti che è possibile usare, vedere [Informazioni di riferimento sull'interfaccia della riga di comando di nuget.exe](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f0cf9-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0cf9-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f0cf9-114">Prerequisites</span></span>

- <span data-ttu-id="f0cf9-115">Installare l'interfaccia della riga di comando `nuget.exe` scaricandola da [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), salvare il file `.exe` in una cartella appropriata e aggiungere tale cartella alla variabile di ambiente PATH.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="f0cf9-116">Installare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f0cf9-116">Install a package</span></span>

<span data-ttu-id="f0cf9-117">Il comando [install](../reference/cli-reference/cli-ref-install.md) scarica e installa un pacchetto in un progetto (per impostazione predefinita nella cartella corrente) usando le origini pacchetto specificate.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="f0cf9-118">Installare i nuovi pacchetti nella cartella *packages* nella directory radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0cf9-119">Il comando `install` non modifica un file di progetto o *il file packages.config* . È pertanto simile a `restore` perché aggiunge soltanto pacchetti su disco, ma non modifica le dipendenze di un progetto.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-119">The `install`command does not modify a project file or *packages.config* ; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="f0cf9-120">Per aggiungere una dipendenza, aggiungere un pacchetto tramite l'interfaccia utente di Gestione pacchetti o la console in Visual Studio oppure modificare il file *packages.config* , quindi eseguire `install` o `restore`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="f0cf9-121">Aprire una riga di comando e passare alla directory che contiene il file di progetto.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="f0cf9-122">Usare il comando seguente per installare un pacchetto NuGet nella cartella *packages* .</span><span class="sxs-lookup"><span data-stu-id="f0cf9-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="f0cf9-123">Per installare il pacchetto `Newtonsoft.json` nella cartella *packages* , usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f0cf9-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="f0cf9-124">In alternativa, è possibile usare il comando seguente per installare un pacchetto NuGet tramite un file `packages.config` esistente nella cartella *packages* .</span><span class="sxs-lookup"><span data-stu-id="f0cf9-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="f0cf9-125">In questo modo non si aggiunge il pacchetto alle dipendenze del progetto, ma si installa il pacchetto localmente.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="f0cf9-126">Installare una versione specifica di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f0cf9-126">Install a specific version of a package</span></span>

<span data-ttu-id="f0cf9-127">Se la versione non viene specificata quando si usa il comando [install](../reference/cli-reference/cli-ref-install.md), NuGet installa la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="f0cf9-128">È anche possibile installare una versione specifica di un pacchetto Nuget:</span><span class="sxs-lookup"><span data-stu-id="f0cf9-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="f0cf9-129">Per aggiungere ad esempio la versione 12.0.1 del pacchetto `Newtonsoft.json`, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="f0cf9-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="f0cf9-130">Per altre informazioni sulle limitazioni e sul comportamento del comando `install`, vedere [Installare un pacchetto](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="f0cf9-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="f0cf9-131">Rimuovere un pacchetto</span><span class="sxs-lookup"><span data-stu-id="f0cf9-131">Remove a package</span></span>

<span data-ttu-id="f0cf9-132">Per eliminare uno o più pacchetti, eliminare i pacchetti che si vogliono rimuovere dalla cartella *packages* .</span><span class="sxs-lookup"><span data-stu-id="f0cf9-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="f0cf9-133">Se si vuole reinstallare i pacchetti, usare il comando `restore` o `install`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="f0cf9-134">Elencare i pacchetti</span><span class="sxs-lookup"><span data-stu-id="f0cf9-134">List packages</span></span>

<span data-ttu-id="f0cf9-135">È possibile visualizzare un elenco dei pacchetti da un'origine specificata usando il comando [list](../reference/cli-reference/cli-ref-list.md).</span><span class="sxs-lookup"><span data-stu-id="f0cf9-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="f0cf9-136">Usare l'opzione `-Source` per limitare la ricerca.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="f0cf9-137">Elencare ad esempio i pacchetti nella cartella *packages* .</span><span class="sxs-lookup"><span data-stu-id="f0cf9-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="f0cf9-138">Se si usa un termine di ricerca, la ricerca includerà i nomi, i tag e le descrizioni dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="f0cf9-139">Aggiornare un singolo pacchetto</span><span class="sxs-lookup"><span data-stu-id="f0cf9-139">Update an individual package</span></span>

<span data-ttu-id="f0cf9-140">Se la versione del pacchetto non viene specificata, NuGet installa la versione del pacchetto più recente quando si usa il comando `install`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="f0cf9-141">Aggiornare tutti i pacchetti</span><span class="sxs-lookup"><span data-stu-id="f0cf9-141">Update all packages</span></span>

<span data-ttu-id="f0cf9-142">Usare il comando [update](../reference/cli-reference/cli-ref-update.md) per aggiornare tutti i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="f0cf9-143">Esegue l'aggiornamento di tutti i pacchetti in un progetto (usando `packages.config`) alle versioni disponibili più recenti.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="f0cf9-144">È consigliabile eseguire il comando `restore` prima di eseguire il comando `update`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="f0cf9-145">Ripristinare pacchetti</span><span class="sxs-lookup"><span data-stu-id="f0cf9-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="f0cf9-146">Ottenere la versione dell'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="f0cf9-146">Get the CLI version</span></span>

<span data-ttu-id="f0cf9-147">Usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="f0cf9-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="f0cf9-148">La prima riga nell'output del comando help mostra la versione.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="f0cf9-149">Per evitare lo scorrimento, usare invece `nuget help | more`.</span><span class="sxs-lookup"><span data-stu-id="f0cf9-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>