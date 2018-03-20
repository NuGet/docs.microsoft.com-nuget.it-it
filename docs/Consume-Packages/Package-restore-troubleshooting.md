---
title: Risoluzione dei problemi relativi al ripristino dei pacchetti NuGet in Visual Studio | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Descrizione degli errori di ripristino comuni per NuGet in Visual Studio e di come risolverli.
keywords: Ripristinare pacchetti NuGet, ripristino di pacchetti, risoluzione dei problemi, risolvere problemi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a>Risoluzione degli errori relativi al ripristino dei pacchetti

Questo articolo è dedicato agli errori comuni durante il ripristino dei pacchetti e alle procedure per risolverli. Per informazioni dettagliate complete sul ripristino dei pacchetti, vedere [Ripristino di pacchetti](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

Se le istruzioni riportate qui non funzionano, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo che lo scenario possa essere esaminato in maggiore dettaglio. Non usare il controllo "Questa pagina è stata utile?" che può essere visualizzato nella pagina perché non offre la possibilità di essere contattati per ulteriori informazioni.

## <a name="quick-solution-for-visual-studio-users"></a>Soluzione rapida per gli utenti di Visual Studio

Se si usa Visual Studio, abilitare prima di tutto il ripristino dei pacchetti come indicato di seguito. In caso contrario, continuare con le sezioni successive.

1. Scegliere i comandi di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti**.
1. Impostare entrambe le opzioni in **Ripristino pacchetto**.
1. Scegliere **OK**.
1. Compilare di nuovo il progetto.

![Abilitare il ripristino dei pacchetti NuGet in Strumenti/Opzioni](../consume-packages/media/restore-01-autorestoreoptions.png)

Queste impostazioni possono essere modificate anche nel file `NuGet.config`. Vedere la sezione sul [consenso](#consent).

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a>Questo progetto fa riferimento a uno o più pacchetti NuGet che non sono presenti in questo computer

Messaggio di errore completo:

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

Questo errore si verifica quando si tenta di compilare un progetto che contiene riferimenti a uno o più pacchetti NuGet, ma tali pacchetti non sono attualmente memorizzati nella cache nel progetto. (I pacchetti vengono memorizzati nella cache in una cartella `packages` nella radice della soluzione se il progetto usa `packages.config` oppure nel file `obj/project.assets.json`, se il progetto usa il formato PackageReference.)

Generalmente questa situazione si verifica quando si ottiene il codice sorgente del progetto dal controllo del codice sorgente o tramite un altro download. I pacchetti vengono in genere omessi dal controllo del codice sorgente o dai download perché possono essere ripristinati da feed di pacchetti come nuget.org (vedere [Pacchetti e controllo del codice sorgente](Packages-and-Source-Control.md)). La loro aggiunta comporterebbe altrimenti un notevole aumento di dimensioni del repository oppure la creazione di file ZIP inutilmente grandi.

Usare uno dei metodi seguenti per ripristinare i pacchetti:

- In Visual Studio abilitare il ripristino dei pacchetti. A tale scopo, selezionare il comando di menu **Strumenti > Gestione pacchetti NuGet > Impostazioni di Gestione pacchetti**, impostare entrambe le opzioni **Ripristino pacchetto** e selezionare **OK**. Compilare quindi di nuovo la soluzione.
- Per i progetti .NET Core, eseguire `dotnet restore` o `dotnet build` (che esegue automaticamente il ripristino).
- Nella riga di comando eseguire `nuget restore` (ad eccezione dei progetti creati con `dotnet`, nel qual caso usare `dotnet restore`).
- Nella riga di comando con i progetti che usano il formato PackageReference, eseguire `msbuild /t:restore`.

Dopo il completamento di un ripristino dovrebbe essere visibile una cartella `packages` (quando si usa`packages.config`) o il file `obj/project.assets.json` (quando si usa PackageReference). La compilazione del progetto dovrebbe ora avvenire senza problemi. In caso contrario, [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da ottenere il necessario supporto.

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a>File di asset project.assets.json non trovato

Messaggio di errore completo:

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

Questo errore si verifica per gli stessi motivi descritti nella [sezione precedente](#missing) e le soluzioni sono le stesse. Ad esempio, l'esecuzione di `msbuild` su un progetto .NET Core ottenuto dal controllo del codice sorgente non comporterà automaticamente il ripristino dei pacchetti. In questo caso, eseguire `msbuild /t:restore` seguito da `msbuild` oppure usare `dotnet build` (che consente di ripristinare i pacchetti automaticamente).

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

Si noti che se si modificano le impostazioni `packageRestore` direttamente in `nuget.config`, occorre riavviare Visual Studio per visualizzare i valori correnti nella finestra di dialogo Opzioni.

## <a name="other-potential-conditions"></a>Altre condizioni potenziali

- Si potrebbero verificare errori di compilazione a causa di file mancanti, con un messaggio che indica di usare il ripristino NuGet per scaricarli. Tuttavia, se si esegue un ripristino potrebbe essere visualizzato il messaggio "Tutti i pacchetti sono già installati. Nessun elemento da ripristinare." In questo caso, eliminare la cartella `packages` (quando si usa `packages.config`) o il file `obj/project.assets.json` (quando si usa PackageReference) e ripetere il ripristino.

- Quando si ottiene un progetto dal controllo del codice sorgente, le cartelle di progetto potrebbero essere impostate in sola lettura. Modificare le autorizzazioni delle cartelle e riprovare a ripristinare i pacchetti.

- È possibile che sia in uso una versione precedente di NuGet. Controllare in [nuget.org/downloads](https://www.nuget.org/downloads) per ottenere le versioni più recenti consigliate. Per Visual Studio 2015 è consigliata la versione 3.6.0.

Se si verificano altri problemi [registrare un problema in GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) in modo da poter fornire ulteriori dettagli su richiesta.