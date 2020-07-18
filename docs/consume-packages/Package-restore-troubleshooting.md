---
title: Risoluzione dei problemi relativi al ripristino dei pacchetti NuGet in Visual Studio
description: Descrizione degli errori di ripristino comuni per NuGet in Visual Studio e di come risolverli.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: b162990eae2160961f560b6c6ee73e47cb4121d6
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451151"
---
# <a name="troubleshooting-package-restore-errors"></a>Risoluzione degli errori relativi al ripristino dei pacchetti

Questo articolo è dedicato agli errori comuni durante il ripristino dei pacchetti e alle procedure per risolverli. 

Ripristino pacchetto tenta di installare tutte le dipendenze del pacchetto nello stato corretto che corrisponde ai riferimenti al pacchetto nel file di progetto (con estensione *csproj*) o nel file *packages.config*. In Visual Studio i riferimenti vengono visualizzati in Esplora soluzioni sotto le **dipendenze \ NuGet** o il nodo **riferimenti** . Per eseguire i passaggi necessari per ripristinare i pacchetti, vedere [ripristinare i pacchetti](../consume-packages/package-restore.md#restore-packages). Se i riferimenti al pacchetto nel file di progetto (con estensione *csproj*) o nel file *packages.config* non sono corretti (non corrispondono allo stato desiderato dopo il ripristino del pacchetto), è necessario installare o aggiornare i pacchetti invece di usare Ripristino pacchetti.

Se le istruzioni riportate qui non funzionano, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo che lo scenario possa essere esaminato in maggiore dettaglio. Non usare il controllo "Questa pagina è stata utile?" che può essere visualizzato nella pagina perché non offre la possibilità di essere contattati per ulteriori informazioni.

## <a name="quick-solution-for-visual-studio-users"></a>Soluzione rapida per gli utenti di Visual Studio

Se si usa Visual Studio, abilitare prima di tutto il ripristino dei pacchetti come indicato di seguito. In caso contrario, continuare con le sezioni successive.

1. Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti**.
1. Impostare entrambe le opzioni in **Ripristino pacchetto**.
1. Selezionare **OK**.
1. Compilare di nuovo il progetto.

![Abilitare il ripristino dei pacchetti NuGet in Strumenti/Opzioni](../consume-packages/media/restore-01-autorestoreoptions.png)

Queste impostazioni possono essere modificate anche nel file `NuGet.config`. Vedere la sezione sul [consenso](#consent). Se il progetto è un progetto precedente che usa il ripristino dei pacchetti integrato in MSBuild, potrebbe essere necessario [eseguire la migrazione](package-restore.md#migrate-to-automatic-package-restore-visual-studio) al ripristino dei pacchetti automatico.

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer

Messaggio di errore completo:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Questo errore si verifica quando si tenta di compilare un progetto che contiene riferimenti a uno o più pacchetti NuGet, ma tali pacchetti non sono attualmente installati nel computer o nel progetto.

- Quando si usa il formato di gestione [PackageReference](package-references-in-project-files.md) , l'errore indica che il pacchetto non è installato nella cartella *Global-Packages* come descritto in [gestione delle cartelle dei pacchetti globali e della cache](managing-the-global-packages-and-cache-folders.md).
- Quando si usa [packages.config](../reference/packages-config.md), questo errore indica che il pacchetto non è installato nella cartella `packages` nella radice della soluzione.

Generalmente questa situazione si verifica quando si ottiene il codice sorgente del progetto dal controllo del codice sorgente o tramite un altro download. I pacchetti vengono in genere omessi dal controllo del codice sorgente o dai download perché possono essere ripristinati da feed di pacchetti come nuget.org (vedere [Pacchetti e controllo del codice sorgente](Packages-and-Source-Control.md)). La loro aggiunta comporterebbe altrimenti un notevole aumento di dimensioni del repository oppure la creazione di file ZIP inutilmente grandi.

L'errore può verificarsi anche se il file di progetto contiene percorsi assoluti ai percorsi dei pacchetti e il progetto viene spostato.

Usare uno dei metodi seguenti per ripristinare i pacchetti:

- Se è stato spostato il file di progetto, modificare il file direttamente per aggiornare i riferimenti ai pacchetti.
- [Visual Studio](package-restore.md#restore-using-visual-studio) ([ripristino automatico](package-restore.md#restore-packages-automatically-using-visual-studio) o [ripristino manuale](package-restore.md#restore-packages-manually-using-visual-studio))
- [Interfaccia della riga di comando di dotnet](package-restore.md#restore-using-the-dotnet-cli)
- [Interfaccia della riga di comando di nuget.exe](package-restore.md#restore-using-the-nugetexe-cli)
- [MSBuild](package-restore.md#restore-using-msbuild)
- [Azure Pipelines](package-restore.md#restore-using-azure-pipelines)
- [Azure DevOps Server](package-restore.md#restore-using-azure-devops-server)

Dopo un ripristino corretto, il pacchetto deve essere presente nella cartella *global-packages*. Per i progetti che usano PackageReference, un ripristino deve ricreare il file `obj/project.assets.json`. Per i progetti che usano `packages.config`, il pacchetto deve essere visualizzato nella cartella `packages` del progetto. La compilazione del progetto dovrebbe ora avvenire senza problemi. In caso contrario, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da ottenere il necessario supporto.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>File di asset project.assets.json non trovato

Messaggio di errore completo:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Il file `project.assets.json` gestisce un grafico delle dipendenze del progetto quando si usa il formato di gestione PackageReference, che consente di assicurarsi che tutti i pacchetti necessari siano installati nel computer. Dato che questo file viene generato in modo dinamico tramite il ripristino del pacchetto, in genere non viene aggiunto al controllo del codice sorgente. Di conseguenza, questo errore si verifica quando si compila un progetto con uno strumento, ad esempio `msbuild`, che non ripristina automaticamente i pacchetti.

In questo caso, eseguire `msbuild -t:restore` seguito da `msbuild` oppure usare `dotnet build` (che consente di ripristinare i pacchetti automaticamente). È anche possibile usare uno dei metodi di ripristino dei pacchetti nella [sezione precedente](#missing).

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a>Non è possibile ripristinare uno o più pacchetti NuGet perché il consenso non è stato concesso

Messaggio di errore completo:

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

Questo errore indica che il ripristino dei pacchetti è disabilitato nella configurazione di NuGet.

È possibile modificare le impostazioni applicabili in Visual Studio, come descritto in precedenza in [Soluzione rapida per gli utenti di Visual Studio](#quick-solution-for-visual-studio-users).

È anche possibile modificare queste impostazioni direttamente nel file `nuget.config` applicabile (in genere `%AppData%\NuGet\NuGet.Config` in Windows e `~/.nuget/NuGet/NuGet.Config` in Mac/Linux). Assicurarsi che le chiavi `enabled` e `automatic` in `packageRestore` siano impostate su True:

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> Se si modificano le impostazioni `packageRestore` direttamente in `nuget.config`, riavviare Visual Studio per visualizzare i valori correnti nella finestra di dialogo Opzioni.

## <a name="other-potential-conditions"></a>Altre condizioni potenziali

- Si potrebbero verificare errori di compilazione a causa di file mancanti, con un messaggio che indica di usare il ripristino NuGet per scaricarli. Tuttavia, se si esegue un ripristino potrebbe essere visualizzato il messaggio "Tutti i pacchetti sono già installati. Nessun elemento da ripristinare." In questo caso, eliminare la cartella `packages` (quando si usa `packages.config`) o il file `obj/project.assets.json` (quando si usa PackageReference) e ripetere il ripristino. Se l'errore persiste, usare `nuget locals all -clear` o `dotnet nuget locals all --clear` dalla riga di comando per cancellare le cartelle *global-packages* e della cache come descritto in [Gestione dei pacchetti globali e delle cartelle della cache](managing-the-global-packages-and-cache-folders.md).

- Quando si ottiene un progetto dal controllo del codice sorgente, le cartelle di progetto potrebbero essere impostate in sola lettura. Modificare le autorizzazioni delle cartelle e riprovare a ripristinare i pacchetti.

- È possibile che sia in uso una versione precedente di NuGet. Controllare in [nuget.org/downloads](https://www.nuget.org/downloads) per ottenere le versioni più recenti consigliate. Per Visual Studio 2015 è consigliata la versione 3.6.0.

Se si verificano altri problemi [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da poter fornire ulteriori dettagli su richiesta.
