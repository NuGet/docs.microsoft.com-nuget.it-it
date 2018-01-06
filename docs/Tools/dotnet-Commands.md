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
ms.openlocfilehash: d020e62b8bd04c8f4a75756fb30ebcf13ffdb1b3
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="dotnet-commands"></a>comandi dotNet

L'interfaccia della riga di comando DotNet, che viene eseguito in Windows, Mac OS X e Linux, fornisce un numero di comandi nuget.exe essenziali come indicato di seguito. Dove dotnet fornisce i comandi desiderati, non è necessario scaricare nuget.exe.

- [**pack dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.
- [**ripristino dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.
- [**variabili locali nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): cancella o elenca le risorse locali di NuGet, ad esempio http-richiesta della cache, cache temporanea o cartella pacchetti globali a livello di computer.
- [**push nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserisce un pacchetto a un server e la pubblicazione, applicabile a tutti i server NuGet di terze parti, Visual Studio Team Services o nuget.org.
- [**eliminare dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o un pacchetto da un server, applicabile a tutti i server NuGet di terze parti, Visual Studio Team Services o nuget.org unlists.
