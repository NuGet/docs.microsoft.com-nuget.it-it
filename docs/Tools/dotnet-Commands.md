---
title: Comandi NuGet dotnet
description: Riferimento per i comandi correlati NuGet tramite l'interfaccia della riga di comando dotnet breve.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="08f5f-103">Comandi dotnet</span><span class="sxs-lookup"><span data-stu-id="08f5f-103">dotnet commands</span></span>

<span data-ttu-id="08f5f-104">Il `dotnet` interfaccia della riga di comando, che viene eseguito in Windows, Mac OS X e Linux, fornisce una serie di comandi nuget.exe essenziali, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="08f5f-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="08f5f-105">Se dotnet soddisfa le proprie esigenze, non è necessario utilizzare `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="08f5f-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="08f5f-106">Per informazioni complete sui `dotnet`, vedere [gli strumenti di interfaccia della riga di comando (CLI) di .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="08f5f-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="08f5f-107">Utilizzo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="08f5f-107">Package consumption</span></span>

- <span data-ttu-id="08f5f-108">[**aggiungere il pacchetto dotnet**](/dotnet/core/tools/dotnet-add-package): aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="08f5f-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="08f5f-109">[**rimuovere un pacchetto dotnet**](/dotnet/core/tools/dotnet-remove-package): rimuove un riferimento pacchetto dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="08f5f-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="08f5f-110">[**ripristino dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto.</span><span class="sxs-lookup"><span data-stu-id="08f5f-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="08f5f-111">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="08f5f-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="08f5f-112">[**variabili locali nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): Elenca i percorsi del *globale pacchetti*, *cache http*, e *temp* cartelle e cancella il contenuto di tali cartelle.</span><span class="sxs-lookup"><span data-stu-id="08f5f-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="08f5f-113">Creazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="08f5f-113">Package creation</span></span>

- <span data-ttu-id="08f5f-114">[**pack dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="08f5f-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="08f5f-115">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="08f5f-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="08f5f-116">[**push nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserisce un pacchetto a un server e la pubblicazione, applicabile a nuget.org, Visual Studio Team Services e i server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="08f5f-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="08f5f-117">[**eliminare dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o unlists un pacchetto da un host, applicabile a nuget.org, Visual Studio Team Services e i server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="08f5f-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
