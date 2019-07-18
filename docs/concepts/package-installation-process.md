---
title: Cosa accade quando viene installato un pacchetto
description: Informazioni dettagliate sul processo di installazione del pacchetto
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 5676239bedb7f8fbe9f74725864afd297405d5c1
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842324"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Cosa accade quando viene installato un pacchetto NuGet

Per semplificare, i diversi strumenti di NuGet creano in genere un riferimento a un pacchetto nel file di progetto o in `packages.config`, quindi eseguono un ripristino del pacchetto, che corrisponde in effetti all'installazione del pacchetto. L'eccezione è `nuget install`, che espande solo il pacchetto in una cartella `packages` e non modifica altri file.

Il processo generale è il seguente:

1. (Tutti gli strumenti eccetto `nuget.exe`) Registrare l'identificatore di pacchetto e la versione nel file di progetto o in `packages.config`.

   Se lo strumento di installazione è Visual Studio o l'interfaccia della riga di comando di dotnet, lo strumento tenta prima di tutto di installare il pacchetto. Se non è compatibile, il pacchetto non viene aggiunto al file di progetto o a `packages.config`.

2. Acquisire il pacchetto:
   - Controllare se il pacchetto (in base all'identificatore esatto e al numero versione) è già installato nella cartella *global-packages* come descritto in [Gestione delle cartelle dei pacchetti globali e della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Se il pacchetto non è presente nella cartella *global-packages*, tentare di recuperarlo dalle origini elencate nei [file di configurazione](../consume-packages/Configuring-NuGet-Behavior.md). Per le origini online, tentare prima di tutto di recuperare il pacchetto dalla cache HTTP, a meno che non si specifichi `-NoCache` con i comandi `nuget.exe` o non si specifichi `--no-cache` con `dotnet restore`. (Visual Studio e `dotnet add package` usano sempre la cache.) Se un pacchetto viene usato dalla cache, nell'output compare "CACHE". La cache ha una scadenza di 30 minuti.

   - Se il pacchetto non è presente nella cache HTTP, tentare di scaricarlo dalle origini elencate nella configurazione. Se un pacchetto viene scaricato, nell'output compaiono "GET" e "OK". NuGet registra il traffico HTTP con un livello di dettaglio normale.

   - Se il pacchetto non può essere acquisito correttamente da qualsiasi origine, l'installazione non riesce a questo punto con un errore come [NU1103](../reference/errors-and-warnings/NU1103.md). Si noti che gli errori dai comandi `nuget.exe` indicano solo l'ultima origine controllata, ma implicano che il pacchetto non era disponibile da qualsiasi origine.

   Per l'acquisizione del pacchetto può essere applicato l'ordine delle origini nella configurazione NuGet:

   - NuGet controlla la cartella locale delle origini e le condivisioni di rete prima di controllare le origini HTTP.

3. Salvare una copia del pacchetto e altre informazioni nella cartella *http-cache* come descritto in [Gestione delle cartelle dei pacchetti globali e della cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Se il pacchetto è stato scaricato, installare il pacchetto nella cartella *global-packages* per utente. NuGet crea una sottocartella per ogni identificatore di pacchetto, quindi crea sottocartelle per ogni versione installata del pacchetto.

5. NuGet installa le dipendenze dei pacchetti se necessario. Questo processo potrebbe aggiornare le versioni del pacchetto nel processo, come descritto in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).

6. Aggiornare altri file e cartelle di progetto:

    - Per i progetti che usano PackageReference, aggiornare il grafico delle dipendenze del pacchetto archiviato in `obj/project.assets.json`. Il contenuto del pacchetto stesso non viene copiato in alcuna cartella di progetto.
    - Aggiornare `app.config` e/o `web.config` se il pacchetto usa [trasformazioni di file di origine e file di configurazione](../create-packages/source-and-config-file-transformations.md).

7. (Solo Visual Studio) Visualizzare il file Leggimi del pacchetto, se disponibile, in una finestra di Visual Studio.

In conclusione, con i pacchetti NuGet la codifica è produttiva.
