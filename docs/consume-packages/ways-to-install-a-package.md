---
title: Modi per installare pacchetti NuGet
description: Descrive il processo di installazione dei pacchetti NuGet in un progetto, incluso cosa accade sul disco e ai file di progetto applicabili.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 0f59c3b7f1e32ae34889921c13d15074ef5c1260
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843381"
---
# <a name="different-ways-to-install-a-nuget-package"></a>Diversi modi per installare un pacchetto NuGet

I pacchetti NuGet possono essere scaricati e installati usando uno dei metodi nella tabella seguente (vedere [Installare gli strumenti client di NuGet](../install-nuget-client-tools.md) se non sono già installati). Il pacchetto può essere recuperato da una cache anziché scaricato.

| Metodo | Descrizione |
| --- | --- |
| Interfaccia della riga di comando di dotnet.exe<br/>`dotnet add package <package_name>` | (Tutte le piattaforme) Recupera il pacchetto identificato da \<package_name\>, espande il relativo contenuto in una cartella nella directory corrente e aggiunge un riferimento al file di progetto. Inoltre, recupera e installa le dipendenze.<ul><li>[Installare e usare un pacchetto (interfaccia della riga di comando di dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Comando dotnet add package](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Interfaccia utente di Gestione pacchetti (Visual Studio) | (Windows e Mac) Offre un'interfaccia utente tramite la quale è possibile esplorare, selezionare e installare i pacchetti e le relative dipendenze in un progetto da un'origine di pacchetti specificata. Aggiunge i riferimenti ai pacchetti installati nel file di progetto.<ul><li>[Installare e usare un pacchetto (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Package Manager UI reference (Windows)](../tools/package-manager-ui.md) (Informazioni di riferimento sull'interfaccia utente di Gestione pacchetti in Windows)</li><li>[Inserimento di un pacchetto NuGet nel progetto (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Console di Gestione pacchetti (Visual Studio)<br/>`Install-Package <package_name>` | (Solo Windows) Recupera e installa il pacchetto identificato da \<package_name\> da un'origine selezionata in un progetto specificato nella soluzione, quindi aggiunge un riferimento al file di progetto. Inoltre, recupera e installa le dipendenze.<ul><li>[Installare e usare un pacchetto (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Package Manager Console Guide](../tools/package-manager-console.md) (Guida alla console di Gestione pacchetti)</li></ul> |
| Interfaccia della riga di comando di nuget.exe<br/>`nuget install <package_name>` | (Tutte le piattaforme) Recupera il pacchetto identificato da \<package_name\> e ne espande il contenuto in una cartella nella directory corrente. Può anche recuperare tutti i pacchetti elencati in un file `packages.config`. Inoltre, recupera e installa le dipendenze, ma non apporta modifiche ai file di progetto o a `packages.config`.<ul><li>[Comando install](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Cosa accade quando viene installato un pacchetto

Per semplificare, i diversi strumenti di NuGet creano in genere un riferimento a un pacchetto nel file di progetto o in `packages.config`, quindi eseguono un ripristino del pacchetto, che corrisponde in effetti all'installazione del pacchetto. L'eccezione è `nuget install`, che espande solo il pacchetto in una cartella `packages` e non modifica altri file.

Il processo generale è il seguente:

1. (Tutti gli strumenti eccetto `nuget.exe`) Registrare l'identificatore di pacchetto e la versione nel file di progetto o in `packages.config`.

2. Acquisire il pacchetto:
   - Controllare se il pacchetto (in base all'identificatore esatto e al numero versione) è già installato nella cartella *global-packages* come descritto in [Gestione delle cartelle dei pacchetti globali e della cache](managing-the-global-packages-and-cache-folders.md).

   - Se il pacchetto non è presente nella cartella *global-packages*, tentare di recuperarlo dalle origini elencate nei [file di configurazione](Configuring-NuGet-Behavior.md). Per le origini online, tentare prima di tutto di recuperare il pacchetto dalla cache, a meno che non si specifichi `-NoCache` con i comandi `nuget.exe` o non si specifichi `--no-cache` con `dotnet restore`. (Visual Studio e `dotnet add package` usano sempre la cache.) Se un pacchetto viene usato dalla cache, nell'output compare "CACHE". La cache ha una scadenza di 30 minuti.

   - Se il pacchetto non è presente nella cache, tentare di scaricarlo dalle origini elencate nella configurazione. Se un pacchetto viene scaricato, nell'output compaiono "GET" e "OK".

   - Se il pacchetto non può essere acquisito correttamente da qualsiasi origine, l'installazione non riesce a questo punto con un errore come [NU1103](../reference/errors-and-warnings/NU1103.md). Si noti che gli errori dai comandi `nuget.exe` indicano solo l'ultima origine controllata, ma implicano che il pacchetto non era disponibile da qualsiasi origine.

   Per l'acquisizione del pacchetto può essere applicato l'ordine delle origini nella configurazione NuGet:

   - Per i progetti che usano il formato PackageReference, NuGet controlla la cartella locale delle origini e le condivisioni di rete prima di controllare le origini HTTP.

   - Per i progetti che usano il formato di gestione `packages.config`, NuGet usa l'ordine delle origini nella configurazione. Le operazioni di ripristino rappresentano un'eccezione. In questo caso, l'ordine delle origini viene ignorato e NuGet usa il pacchetto da qualsiasi origine risponde per prima.

   - In generale, l'ordine in cui NuGet controlla le origini non è particolarmente significativo, perché qualsiasi pacchetto con uno specifico identificatore e numero di versione è esattamente lo stesso in qualsiasi origine venga trovato.

3. (Tutti gli strumenti eccetto `nuget.exe`) Salvare una copia del pacchetto e altre informazioni nella cartella *http-cache* come descritto in [Gestione delle cartelle dei pacchetti globali e della cache](managing-the-global-packages-and-cache-folders.md).

4. Se il pacchetto è stato scaricato, installare il pacchetto nella cartella *global-packages* per utente. NuGet crea una sottocartella per ogni identificatore di pacchetto, quindi crea sottocartelle per ogni versione installata del pacchetto.

5. Aggiornare altri file e cartelle di progetto:

    - Per i progetti che usano PackageReference, aggiornare il grafico delle dipendenze del pacchetto archiviato in `obj/project.assets.json`. Il contenuto del pacchetto stesso non viene copiato in alcuna cartella di progetto.
    - Per i progetti che usano `packages.config`, copiare queste parti del pacchetto espanso che corrisponde al framework di destinazione del progetto nella cartella `packages` del progetto. Quando si usa `nuget install`, viene copiato l'intero pacchetto espanso perché `nuget.exe` non esamina i file di progetto per identificare il framework di destinazione.
    - Aggiornare `app.config` e/o `web.config` se il pacchetto usa [trasformazioni di file di origine e file di configurazione](../create-packages/source-and-config-file-transformations.md).

6. Installare eventuali dipendenze di livello inferiore se non sono già presenti nel progetto. Questo processo potrebbe aggiornare le versioni del pacchetto nel processo, come descritto in [Risoluzione delle dipendenze](../consume-packages/dependency-resolution.md).

7. (Solo Visual Studio) Visualizzare il file Leggimi del pacchetto, se disponibile, in una finestra di Visual Studio.

## <a name="related-articles"></a>Articoli correlati

- [Panoramica e flusso di lavoro dell'utilizzo di pacchetti](../consume-packages/overview-and-workflow.md)
- [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md)
- [Managing the NuGet cache and global-packages folders](managing-the-global-packages-and-cache-folders.md) (Gestione della cache NuGet e delle cartelle global-packages)
- [Configurazione del comportamento di NuGet](../consume-packages/configuring-nuget-behavior.md)
