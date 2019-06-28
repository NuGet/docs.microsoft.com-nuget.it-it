---
title: comandi dotnet NuGet CLI
description: Un riferimento breve per i comandi correlati a NuGet tramite l'interfaccia della riga di comando di dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426009"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="e5bd8-103">comandi della riga di comando di dotnet</span><span class="sxs-lookup"><span data-stu-id="e5bd8-103">dotnet CLI commands</span></span>

<span data-ttu-id="e5bd8-104">Il `dotnet` interfaccia della riga di comando (CLI), che viene eseguito in Windows, Mac OS X e Linux, offre una serie di comandi essenziali, ad esempio installazione, il ripristino e la pubblicazione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="e5bd8-105">Se dotnet soddisfa le proprie esigenze, non è necessario usare `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="e5bd8-106">Per esempi dell'uso di questi comandi per utilizzare pacchetti, vedere [installare e gestire i pacchetti tramite la riga di comando di dotnet](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e5bd8-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="e5bd8-107">Per esempi dell'uso di questi comandi per creare pacchetti, vedere [creare e pubblicare un pacchetto usando la riga di comando di dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e5bd8-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="e5bd8-108">Per i riferimenti ai comandi completo sul `dotnet` CLI, vedere [degli strumenti dell'interfaccia della riga di comando (CLI) di .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="e5bd8-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="e5bd8-109">Utilizzo di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="e5bd8-109">Package consumption</span></span>

- <span data-ttu-id="e5bd8-110">[**dotnet Aggiungi pacchetto**](/dotnet/core/tools/dotnet-add-package): Aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="e5bd8-111">[**comando dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Rimuove un riferimento al pacchetto dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="e5bd8-112">[**comando dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="e5bd8-113">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="e5bd8-114">[**variabili locali di dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): Elenca le località POP della *global-packages*, *http-cache*, e *temp* cartelle e cancella il contenuto di tali cartelle.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="e5bd8-115">Creazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="e5bd8-115">Package creation</span></span>

- <span data-ttu-id="e5bd8-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Comprime il codice in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="e5bd8-117">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="e5bd8-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Effettua il push di un pacchetto a un server e lo pubblica, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="e5bd8-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Dall'elenco o elimina un pacchetto da un host, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="e5bd8-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
