---
title: i comandi NuGet dotNet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Riferimento per i comandi correlati NuGet tramite l'interfaccia della riga di comando dotnet breve.
keywords: i comandi NuGet dotnet pack dotnet, ripristino dotnet, variabili locali nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d06e4590ab87b68e7846a13b2eba0f59eb9529d6
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="39a92-104">comandi dotNet</span><span class="sxs-lookup"><span data-stu-id="39a92-104">dotNet commands</span></span>

<span data-ttu-id="39a92-105">L'interfaccia della riga di comando DotNet, che viene eseguito in Windows, Mac OS X e Linux, fornisce un numero di comandi nuget.exe essenziali come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="39a92-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="39a92-106">Dove dotnet fornisce i comandi desiderati, non è necessario scaricare nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="39a92-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="39a92-107">[**pack dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="39a92-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="39a92-108">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="39a92-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="39a92-109">[**ripristino dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto.</span><span class="sxs-lookup"><span data-stu-id="39a92-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="39a92-110">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="39a92-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="39a92-111">[**variabili locali nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): cancella o elenca le risorse locali di NuGet, ad esempio http-richiesta della cache, cache temporanea o cartella pacchetti globali a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="39a92-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="39a92-112">[**push nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserisce un pacchetto a un server e la pubblicazione, applicabile a tutti i server NuGet di terze parti, Visual Studio Team Services o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="39a92-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="39a92-113">[**eliminare dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o un pacchetto da un server, applicabile a tutti i server NuGet di terze parti, Visual Studio Team Services o nuget.org unlists.</span><span class="sxs-lookup"><span data-stu-id="39a92-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
