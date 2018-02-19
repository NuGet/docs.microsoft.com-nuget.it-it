---
title: Modi per installare pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: Descrive il processo di installazione dei pacchetti NuGet in un progetto, incluso cosa accade sul disco e ai file di progetto applicabili.
keywords: installare NuGet, utilizzo di un pacchetto NuGet, installazione di pacchetti NuGet, riferimenti ai pacchetti NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Diversi modi per installare un pacchetto NuGet

I pacchetti NuGet possono essere scaricati e installati usando uno dei metodi seguenti (vedere [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md) se non sono già installati):

| Metodo | Descrizione |
| --- | --- |
| Interfaccia della riga di comando di dotnet.exe<br/>`dotnet install <package_name>` | (Tutte le piattaforme) Scarica il pacchetto identificato da \<package_name\>, espande il relativo contenuto in una cartella nella directory corrente e aggiunge un riferimento al file di progetto. Inoltre, scarica e installa le dipendenze.<ul><li>[Installare e usare un pacchetto (interfaccia della riga di comando di dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Comandi dotnet](../tools/dotnet-commands.md)</li></ul> |
| Interfaccia utente di Gestione pacchetti (Visual Studio) | (Windows e Mac) Offre un'interfaccia utente tramite la quale è possibile esplorare, selezionare e installare i pacchetti e le relative dipendenze in un progetto. Aggiunge i riferimenti ai pacchetti installati nel file di progetto.<ul><li>[Installare e usare un pacchetto (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Package Manager UI reference (Windows)](../tools/package-manager-ui.md) (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti in Windows)</li><li>[Inserimento di un pacchetto NuGet nel progetto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Console di Gestione pacchetti (Visual Studio)<br/>`Install-Package <package_name>` | (Solo Windows) Scarica e installa il pacchetto identificato da \<package_name\> in un progetto specificato nella soluzione, quindi aggiunge un riferimento al file di progetto. Inoltre, scarica e installa le dipendenze.<ul><li>[Installare e usare un pacchetto (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Package Manager Console Guide](../tools/package-manager-console.md) (Guida alla console di Gestione pacchetti)</li></ul> |
| Interfaccia della riga di comando di nuget.exe<br/>`nuget install <package_name>` | (Tutte le piattaforme) Scarica il pacchetto identificato da \<package_name\> e ne espande il contenuto in una cartella nella directory corrente. Può anche scaricare tutti i pacchetti elencati in un file `packages.config`. Inoltre, scarica e installa le dipendenze, ma non apporta modifiche ai file di progetto.<ul><li>[Comando install](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Procedura di installazione generale

In generale, NuGet esegue le operazioni seguenti quando viene richiesto di installare un pacchetto:

1. Acquisire il pacchetto:
    - Verifica se il pacchetto richiesto esiste già in una cache (vedere [Gestione delle cache NuGet](managing-the-nuget-cache.md)).
    - Se il pacchetto non è presente nella cache, tenta di scaricare il pacchetto dalle origini elencate nei [file di configurazione](Configuring-NuGet-Behavior.md).
      - Per i progetti che usano il formato di riferimento `packages.config`, NuGet usa l'ordine delle origini nella configurazione.
      - Per i progetti che usano il formato PackageReference, NuGet controlla prima le origini che sono cartelle locali, quindi le origini nelle condivisioni di rete e infine le origini HTTP (Internet).
      - In generale, l'ordine in cui NuGet controlla le origini non è particolarmente significativo, perché qualsiasi pacchetto con uno specifico identificatore e numero di versione è esattamente lo stesso in qualsiasi origine venga trovato.
    - Se il pacchetto viene acquisito correttamente da una delle origini, NuGet lo aggiunge nella cache. In caso contrario, l'installazione non riesce.

1. Espandere il pacchetto nel progetto.
    - Espansione significa decomprimere il contenuto del pacchetto in una sottocartella appropriata. Anche una copia del file `.nupkg` stesso viene inserita nella sottocartella.
    - Se il pacchetto viene installato in un progetto di Visual Studio o .NET Core, vengono espansi solo i file pertinenti per il framework di destinazione del progetto. Durante l'installazione dalla riga di comando di nuget.exe, vengono espansi tutti gli assembly.

1. Se il pacchetto viene installato all'interno di Visual Studio o dell'interfaccia della riga di comando dotnet, viene aggiunto un riferimento al file di progetto appropriato (o a `packages.config` per alcuni tipi di progetto in Visual Studio).

## <a name="related-topics"></a>Argomenti correlati

- [Panoramica e flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/overview-and-workflow.md)
- [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md)
- [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md)
- [Gestione delle cache NuGet](managing-the-nuget-cache.md)
