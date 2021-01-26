---
title: comandi NuGet dell'interfaccia della riga di comando DotNet
description: Un breve riferimento per i comandi correlati a NuGet che usano l'interfaccia della riga di comando dotnet.
author: JonDouglas
ms.author: jodou
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 5438354729ccc851bbbae6c0e7b9394d4226da52
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779989"
---
# <a name="dotnet-cli-commands"></a>Comandi dell'interfaccia della riga di comando di .NET

L' `dotnet` interfaccia della riga di comando (CLI), eseguita in Windows, Mac OS X e Linux, fornisce una serie di comandi essenziali, ad esempio l'installazione, il ripristino e la pubblicazione di pacchetti. Se DotNet soddisfa le proprie esigenze, non è necessario usare `nuget.exe` .

Per esempi relativi all'uso di questi comandi per l'uso di pacchetti, vedere [installare e gestire i pacchetti usando l'interfaccia della riga](../consume-packages/install-use-packages-dotnet-cli.md)di comando di DotNet. Per esempi relativi all'uso di questi comandi per la creazione di pacchetti, vedere [creare e pubblicare un pacchetto usando l'interfaccia della](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)riga di comando di DotNet.

Per informazioni di riferimento complete sull' `dotnet` interfaccia della riga di comando, vedere [strumenti dell'interfaccia della riga di comando di .NET Core](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Utilizzo pacchetti

- [**DotNet Add Package**](/dotnet/core/tools/dotnet-add-package): aggiunge un riferimento al pacchetto nel file di progetto, quindi esegue `dotnet restore` per installare il pacchetto.
- [**DotNet Remove Package**](/dotnet/core/tools/dotnet-remove-package): rimuove un riferimento a un pacchetto dal file di progetto.
- [**DotNet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Ripristina le dipendenze e gli strumenti di un progetto. A partire da NuGet 4.0, esegue lo stesso codice di `nuget restore`.
- [**DotNet NuGet locals**](/dotnet/core/tools/dotnet-nuget-locals): elenca i percorsi delle cartelle *Global-Packages*, *http-cache* e *Temp* e cancella il contenuto di tali cartelle.
- [**DotNet New nugetconfig**](/dotnet/core/tools/dotnet-new): crea un [`nuget.config`](../reference/nuget-config-file.md) file per configurare il comportamento di NuGet.

## <a name="package-creation"></a>Creazione di pacchetti

- [**DotNet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): comprime il codice in un pacchetto NuGet.
- [**DotNet NuGet push**](/dotnet/core/tools/dotnet-nuget-push): pubblica un pacchetto in un server NuGet. Applicabile a nuget.org, Azure Artifacts e a [Server NuGet di terze parti](../hosting-packages/overview.md).
- [**DotNet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): Elimina o rimuove dall'elenco un pacchetto da un server NuGet. Applicabile a nuget.org, Azure Artifacts e a [Server NuGet di terze parti](../hosting-packages/overview.md).
- [**DotNet NuGet Verify**](/dotnet/core/tools/dotnet-nuget-verify): verifica un pacchetto NuGet firmato.
