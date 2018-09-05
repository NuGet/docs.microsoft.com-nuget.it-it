---
title: comandi dotnet NuGet
description: Un riferimento breve per i comandi correlati a NuGet tramite l'interfaccia della riga di comando di dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546316"
---
# <a name="dotnet-commands"></a><span data-ttu-id="7d078-103">Comandi dotnet</span><span class="sxs-lookup"><span data-stu-id="7d078-103">dotnet commands</span></span>

<span data-ttu-id="7d078-104">Il `dotnet` dell'interfaccia della riga di comando, che viene eseguito in Windows, Mac OS X e Linux, offre una serie di comandi nuget.exe essenziali, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="7d078-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="7d078-105">Se dotnet soddisfa le proprie esigenze, non è necessario usare `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="7d078-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="7d078-106">Per informazioni complete sullo `dotnet`, vedere [degli strumenti dell'interfaccia della riga di comando (CLI) di .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="7d078-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="7d078-107">Utilizzo di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="7d078-107">Package consumption</span></span>

- <span data-ttu-id="7d078-108">[**dotnet Aggiungi pacchetto**](/dotnet/core/tools/dotnet-add-package): aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="7d078-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="7d078-109">[**comando dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): rimuove un riferimento al pacchetto dal file di progetto.</span><span class="sxs-lookup"><span data-stu-id="7d078-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="7d078-110">[**comando dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto.</span><span class="sxs-lookup"><span data-stu-id="7d078-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="7d078-111">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="7d078-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="7d078-112">[**variabili locali di dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): Elenca le località POP della *global-packages*, *http-cache*, e *temp* cartelle e cancella il contenuto di tali cartelle.</span><span class="sxs-lookup"><span data-stu-id="7d078-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="7d078-113">Creazione del pacchetto</span><span class="sxs-lookup"><span data-stu-id="7d078-113">Package creation</span></span>

- <span data-ttu-id="7d078-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d078-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="7d078-115">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="7d078-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="7d078-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): effettua il push di un pacchetto a un server e lo pubblica, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="7d078-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="7d078-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): dall'elenco o elimina un pacchetto da un host, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.</span><span class="sxs-lookup"><span data-stu-id="7d078-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
