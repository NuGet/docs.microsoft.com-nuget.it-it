---
title: i comandi NuGet dotNet | Documenti Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Riferimento per i comandi correlati NuGet tramite l'interfaccia della riga di comando dotnet breve.
keywords: i comandi NuGet dotnet pack dotnet, ripristino dotnet, variabili locali nuget dotnet, dotnet nuget push, dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 352145701fba509e21e774a429d227e7427a1f0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="dotnet-commands"></a>comandi dotNet

Il `dotnet` interfaccia della riga di comando, che viene eseguito in Windows, Mac OS X e Linux, fornisce una serie di comandi nuget.exe essenziali, come indicato di seguito. Se dotnet soddisfa le proprie esigenze, non è necessario utilizzare `nuget.exe`.

Per informazioni complete sui `dotnet`, vedere [gli strumenti di interfaccia della riga di comando (CLI) di .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Utilizzo di pacchetto

- [**aggiungere il pacchetto dotnet**](/dotnet/core/tools/dotnet-add-package): aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.
- [**rimuovere un pacchetto dotnet**](/dotnet/core/tools/dotnet-remove-package): rimuove un riferimento pacchetto dal file di progetto.
- [**ripristino dotnet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.
- [**variabili locali nuget dotnet**](/dotnet/core/tools/dotnet-nuget-locals): Elenca i percorsi del *globale pacchetti*, *cache http*, e *temp* cartelle e cancella il contenuto di tali cartelle.

## <a name="package-creation"></a>Creazione del pacchetto

- [**pack dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.
- [**push nuget dotnet**](/dotnet/core/tools/dotnet-nuget-push): inserisce un pacchetto a un server e la pubblicazione, applicabile a nuget.org, Visual Studio Team Services e i server NuGet di terze parti.
- [**eliminare dotnet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o unlists un pacchetto da un host, applicabile a nuget.org, Visual Studio Team Services e i server NuGet di terze parti.
