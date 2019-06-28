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
# <a name="dotnet-cli-commands"></a>comandi della riga di comando di dotnet

Il `dotnet` interfaccia della riga di comando (CLI), che viene eseguito in Windows, Mac OS X e Linux, offre una serie di comandi essenziali, ad esempio installazione, il ripristino e la pubblicazione di pacchetti. Se dotnet soddisfa le proprie esigenze, non è necessario usare `nuget.exe`.

Per esempi dell'uso di questi comandi per utilizzare pacchetti, vedere [installare e gestire i pacchetti tramite la riga di comando di dotnet](../consume-packages/install-use-packages-dotnet-cli.md). Per esempi dell'uso di questi comandi per creare pacchetti, vedere [creare e pubblicare un pacchetto usando la riga di comando di dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Per i riferimenti ai comandi completo sul `dotnet` CLI, vedere [degli strumenti dell'interfaccia della riga di comando (CLI) di .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Utilizzo di un pacchetto

- [**dotnet Aggiungi pacchetto**](/dotnet/core/tools/dotnet-add-package): Aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.
- [**comando dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Rimuove un riferimento al pacchetto dal file di progetto.
- [**comando dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget restore`.
- [**variabili locali di dotnet nuget**](/dotnet/core/tools/dotnet-nuget-locals): Elenca le località POP della *global-packages*, *http-cache*, e *temp* cartelle e cancella il contenuto di tali cartelle.

## <a name="package-creation"></a>Creazione del pacchetto

- [**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Comprime il codice in un pacchetto NuGet. A partire da NuGet 4.0, questo viene eseguito lo stesso codice `nuget pack`.
- [**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Effettua il push di un pacchetto a un server e lo pubblica, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.
- [**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Dall'elenco o elimina un pacchetto da un host, applicabile a nuget.org, Visual Studio Team Services e server NuGet di terze parti.
