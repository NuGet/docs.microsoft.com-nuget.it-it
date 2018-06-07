---
title: Comandi NuGet dotnet
description: Riferimento per i comandi correlati NuGet tramite l'interfaccia della riga di comando dotnet breve.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: dd30c5d5e29ff7ef7c6622a9b93c32b908198d52
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817021"
---
# <a name="dotnet-commands"></a>Comandi dotnet

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
