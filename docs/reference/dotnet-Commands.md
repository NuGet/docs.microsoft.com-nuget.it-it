---
title: comandi NuGet dell'interfaccia della riga di comando DotNet
description: Un breve riferimento per i comandi correlati a NuGet che usano l'interfaccia della riga di comando dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327488"
---
# <a name="dotnet-cli-commands"></a>comandi dell'interfaccia della riga di comando DotNet

L' `dotnet` interfaccia della riga di comando (CLI), eseguita in Windows, Mac OS X e Linux, fornisce una serie di comandi essenziali, ad esempio l'installazione, il ripristino e la pubblicazione di pacchetti. Se DotNet soddisfa le proprie esigenze, non è necessario usare `nuget.exe`.

Per esempi relativi all'uso di questi comandi per l'uso di pacchetti, vedere [installare e gestire i pacchetti usando l'interfaccia della riga](../consume-packages/install-use-packages-dotnet-cli.md)di comando di DotNet. Per esempi relativi all'uso di questi comandi per la creazione di pacchetti, vedere [creare e pubblicare un pacchetto usando l'interfaccia della](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)riga di comando di DotNet.

Per informazioni di riferimento complete sull' `dotnet` interfaccia della riga di comando, vedere [strumenti dell'interfaccia della riga di comando di .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Utilizzo pacchetti

- [**pacchetto di aggiunta DotNet**](/dotnet/core/tools/dotnet-add-package): Aggiunge un riferimento al pacchetto nel file di progetto, quindi `dotnet restore` esegue per installare il pacchetto.
- [**pacchetto di rimozione DotNet**](/dotnet/core/tools/dotnet-remove-package): Rimuove un riferimento a un pacchetto dal file di progetto.
- [**DotNet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto. A partire da NuGet 4.0, esegue lo stesso codice di `nuget restore`.
- [**variabili locali DotNet NuGet**](/dotnet/core/tools/dotnet-nuget-locals): Elenca i percorsi delle cartelle *Global-Packages*, *http-cache*e *Temp* e cancella il contenuto di tali cartelle.
- [**nuovo nugetconfig DotNet**](/dotnet/core/tools/dotnet-new): Crea un [`nuget.config`](../reference/nuget-config-file.md) file per configurare il comportamento di NuGet.

## <a name="package-creation"></a>Creazione di pacchetti

- [**pacchetto dotnet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Comprime il codice in un pacchetto NuGet.
- [**push NuGet DotNet**](/dotnet/core/tools/dotnet-nuget-push): Pubblica un pacchetto in un server NuGet. Applicabile a nuget.org, Azure Artifacts e a [Server NuGet di terze parti](../hosting-packages/overview.md).
- [**eliminazione NuGet DotNet**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o rimuove dall'elenco un pacchetto da un server NuGet. Applicabile a nuget.org, Azure Artifacts e a [Server NuGet di terze parti](../hosting-packages/overview.md).
