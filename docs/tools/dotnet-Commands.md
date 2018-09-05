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
# <a name="dotnet-commands"></a>Comandi dotnet

Il `dotnet` dell'interfaccia della riga di comando, che viene eseguito in Windows, Mac OS X e Linux, offre una serie di comandi nuget.exe essenziali, come indicato di seguito. Se dotnet soddisfa le proprie esigenze, non è necessario usare `nuget.exe`.

Per informazioni complete sullo `dotnet`, vedere [degli strumenti dell'interfaccia della riga di comando (CLI) di .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Utilizzo di un pacchetto

- [**dotnet Aggiungi pacchetto**](/dotnet/core/tools/dotnet-add-package): aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.
- [**comando dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): rimuove un riferimento al pacchetto dal file di progetto.
- [**comando dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.
- [**variabili locali di dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): Elenca le località POP della *global-packages*, *http-cache*, e *temp* cartelle e cancella il contenuto di tali cartelle.

## <a name="package-creation"></a>Creazione del pacchetto

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): effettua il push di un pacchetto a un server e lo pubblica, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): dall'elenco o elimina un pacchetto da un host, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.
