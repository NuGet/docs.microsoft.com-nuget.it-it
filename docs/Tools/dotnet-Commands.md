---
title: i comandi NuGet dotNet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: Riferimento per i comandi correlati NuGet tramite l'interfaccia della riga di comando dotnet breve.
keywords: i comandi NuGet dotnet pack dotnet, ripristino dotnet, variabili locali nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a><span data-ttu-id="ac382-104">comandi dotNet</span><span class="sxs-lookup"><span data-stu-id="ac382-104">dotNet commands</span></span>

<span data-ttu-id="ac382-105">L'interfaccia della riga di comando DotNet, che viene eseguito in Windows, Mac OS X e Linux, fornisce un numero di comandi nuget.exe essenziali come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="ac382-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="ac382-106">Dove dotnet fornisce i comandi desiderati, non è necessario scaricare nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="ac382-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="ac382-107">[**pack dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pacchetti di codice per SDK NETCore di progetti in un pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac382-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="ac382-108">Tutti gli altri tipi di progetto devono utilizzare[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="ac382-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="ac382-109">[**ripristino dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto.</span><span class="sxs-lookup"><span data-stu-id="ac382-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="ac382-110">A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="ac382-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="ac382-111">[**variabili locali nuget dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): cancella o elenca le risorse locali di NuGet, ad esempio http-richiesta della cache, cache temporanea o cartella pacchetti globali a livello di computer.</span><span class="sxs-lookup"><span data-stu-id="ac382-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="ac382-112">[**push nuget dotnet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): inserisce un pacchetto a un server e la pubblicazione, applicabile a tutti i server NuGet di terze parti, Visual Studio Team Services o nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ac382-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="ac382-113">[**eliminare dotnet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Elimina o un pacchetto da un server, applicabile a tutti i server NuGet di terze parti, Visual Studio Team Services o nuget.org unlists.</span><span class="sxs-lookup"><span data-stu-id="ac382-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
