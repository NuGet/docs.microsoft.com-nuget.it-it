---
title: Installare e gestire pacchetti NuGet usando l'interfaccia della riga di comando di dotnet
description: Istruzioni per usare l'interfaccia della riga di comando di dotnet insieme a pacchetti NuGet.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 38455e61bd91f115df9f27df090ba47a029f6877
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622941"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="00646-103">Installare e gestire pacchetti usando l'interfaccia della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="00646-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="00646-104">Lo strumento della riga di comando consente di installare, disinstallare e aggiornare facilmente pacchetti NuGet in progetti e soluzioni.</span><span class="sxs-lookup"><span data-stu-id="00646-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="00646-105">Viene eseguito in Windows, Mac OS X e Linux.</span><span class="sxs-lookup"><span data-stu-id="00646-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="00646-106">L'interfaccia della riga di comando di dotnet viene usata per i progetti .NET Core e .NET Standard (tipi di progetto in stile SDK) e per qualsiasi altro progetto in stile SDK, ad esempio i progetti in stile SDK per .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="00646-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="00646-107">Per altre informazioni, vedere [Attributo SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="00646-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="00646-108">Questo articolo illustra l'utilizzo di base di alcuni dei comandi più comuni dell'interfaccia della riga di comando di dotnet.</span><span class="sxs-lookup"><span data-stu-id="00646-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="00646-109">Per la maggior parte di questi comandi, lo strumento della riga di comando cerca un file di progetto nella directory corrente, a meno che non venga specificato un file di progetto nel comando. Il file di progetto è un'opzione facoltativa.</span><span class="sxs-lookup"><span data-stu-id="00646-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="00646-110">Per un elenco completo dei comandi e degli argomenti che è possibile usare, vedere [Strumenti dell'interfaccia della riga di comando di .NET Core](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="00646-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00646-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="00646-111">Prerequisites</span></span>

- <span data-ttu-id="00646-112">[.NET Core SDK](https://www.microsoft.com/net/download/), che fornisce lo strumento da riga di comando `dotnet`.</span><span class="sxs-lookup"><span data-stu-id="00646-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="00646-113">A partire da Visual Studio 2017, l'interfaccia della riga di comando di dotnet viene installata automaticamente con qualsiasi carico di lavoro .NET Core correlato.</span><span class="sxs-lookup"><span data-stu-id="00646-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="00646-114">Installare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="00646-114">Install a package</span></span>

<span data-ttu-id="00646-115">Il comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="00646-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="00646-116">Aprire una riga di comando e passare alla directory che contiene il file di progetto.</span><span class="sxs-lookup"><span data-stu-id="00646-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="00646-117">Usare il comando seguente per installare un pacchetto Nuget:</span><span class="sxs-lookup"><span data-stu-id="00646-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="00646-118">Ad esempio, per installare il pacchetto `Newtonsoft.Json`, usare il comando seguente</span><span class="sxs-lookup"><span data-stu-id="00646-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="00646-119">Dopo aver eseguito il comando, esaminare il file di progetto per assicurarsi che il pacchetto sia stato installato.</span><span class="sxs-lookup"><span data-stu-id="00646-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="00646-120">È possibile aprire il file `.csproj` per visualizzare il riferimento aggiunto:</span><span class="sxs-lookup"><span data-stu-id="00646-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="00646-121">Installare una versione specifica di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="00646-121">Install a specific version of a package</span></span>

<span data-ttu-id="00646-122">Se la versione non viene specificata, NuGet installa la versione più recente del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="00646-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="00646-123">È anche possibile usare il comando [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) per installare una versione specifica di un pacchetto Nuget:</span><span class="sxs-lookup"><span data-stu-id="00646-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="00646-124">Per aggiungere ad esempio la versione 12.0.1 del pacchetto `Newtonsoft.Json`, usare questo comando:</span><span class="sxs-lookup"><span data-stu-id="00646-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="00646-125">Elencare i riferimenti al pacchetto</span><span class="sxs-lookup"><span data-stu-id="00646-125">List package references</span></span>

<span data-ttu-id="00646-126">È possibile elencare i riferimenti al pacchetto per il progetto usando il comando [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="00646-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="00646-127">Rimuovere un pacchetto</span><span class="sxs-lookup"><span data-stu-id="00646-127">Remove a package</span></span>

<span data-ttu-id="00646-128">Usare il comando [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) per rimuovere un riferimento al pacchetto dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="00646-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="00646-129">Ad esempio, per rimuovere il pacchetto `Newtonsoft.Json`, usare il comando seguente</span><span class="sxs-lookup"><span data-stu-id="00646-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="00646-130">Aggiornare un pacchetto</span><span class="sxs-lookup"><span data-stu-id="00646-130">Update a package</span></span>

<span data-ttu-id="00646-131">Se la versione del pacchetto non viene specificata, NuGet installa la versione del pacchetto più recente quando si usa il comando `dotnet add package` (opzione `-v`).</span><span class="sxs-lookup"><span data-stu-id="00646-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="00646-132">Ripristinare pacchetti</span><span class="sxs-lookup"><span data-stu-id="00646-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
