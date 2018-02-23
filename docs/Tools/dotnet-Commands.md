---
title: i comandi NuGet dotNet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Riferimento per i comandi correlati NuGet tramite l'interfaccia della riga di comando dotnet breve.
keywords: i comandi NuGet dotnet pack dotnet, ripristino dotnet, variabili locali nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="a2824-104">comandi dotNet</span><span class="sxs-lookup"><span data-stu-id="a2824-104">dotNet commands</span></span>

<span data-ttu-id="a2824-105">Il `dotnet` interfaccia della riga di comando, che viene eseguito in Windows, Mac OS X e Linux, fornisce una serie di comandi nuget.exe essenziali, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a2824-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="a2824-106">Se dotnet soddisfa le proprie esigenze, non è necessario utilizzare `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="a2824-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="a2824-107">Per informazioni complete sui `dotnet`, vedere [gli strumenti di interfaccia della riga di comando (CLI) di .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="a2824-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="a2824-108">Utilizzo di pacchetto</span><span class="sxs-lookup"><span data-stu-id="a2824-108">Package consumption</span></span>

- <span data-ttu-id="a2824-109">[**aggiungere il pacchetto dotnet**](/dotnet/core/tools/dotnet-add-package): aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="a2824-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="a2824-110">[**rimuovere un pacchetto dotnet**](/dotnet/core/tools/dotnet-remove-package): rimuove un riferimento pacchetto dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="a2824-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="a2824-111">[**ripristino dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto.</span><span class="sxs-lookup"><span data-stu-id="a2824-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="a2824-112">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="a2824-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="a2824-113">[**variabili locali nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): cancella o elenca le risorse locali di NuGet, ad esempio la cache della richiesta http, la cache temporanea e la cartella pacchetti globali a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="a2824-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="a2824-114">Creazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="a2824-114">Package creation</span></span>

- <span data-ttu-id="a2824-115">[**pack dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="a2824-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="a2824-116">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="a2824-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="a2824-117">[**push nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserisce un pacchetto a un server e la pubblicazione, applicabile a nuget.org, Visual Studio Team Services e i server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="a2824-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="a2824-118">[**eliminare dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o unlists un pacchetto da un host, applicabile a nuget.org, Visual Studio Team Services e i server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="a2824-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
