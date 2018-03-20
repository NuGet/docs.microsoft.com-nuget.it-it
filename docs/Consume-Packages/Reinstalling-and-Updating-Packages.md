---
title: Reinstallazione e aggiornamento di pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2785879b-97f0-4a85-b3cc-bf4eaa5c39bf
description: "Informazioni dettagliate su quando è necessario reinstallare e aggiornare i pacchetti, ad esempio nel caso di riferimenti ai pacchetti interrotti in Visual Studio."
keywords: Installazione del pacchetto NuGet, reinstallazione del pacchetto NuGet, ripristino del pacchetto NuGet, aggiornamento del pacchetto, ripristino di pacchetti, correzione di riferimenti interrotti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e2875630b24fbe04fc7bcab52335d849e54160de
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/08/2018
---
# <a name="how-to-reinstall-and-update-packages"></a>Come reinstallare e aggiornare pacchetti

Esistono diverse situazioni, descritte di seguito in [Quando reinstallare un pacchetto](#when-to-reinstall-a-package), in cui i riferimenti a un pacchetto potrebbero essere interrotti all'interno di un progetto di Visual Studio. In questi casi la disinstallazione e la successiva reinstallazione della stessa versione del pacchetto ripristineranno tali riferimenti mettendoli in condizione di funzionare. Aggiornare un pacchetto significa semplicemente installarne una versione aggiornata, un'operazione che spesso consente di ripristinare un pacchetto rendendolo funzionante.

Le operazioni di aggiornamento e reinstallazione dei pacchetti vengono eseguite come indicato di seguito:

| Metodo | Aggiorna | Reinstallazione |
| --- | --- | --- |
| Console di Gestione pacchetti (descritta in [Uso di Update-Package](#using-update-package)) | Comando `Update-Package` | Comando `Update-Package -reinstall` |
| Interfaccia utente di Gestione pacchetti | Nella scheda **Aggiornamenti** selezionare uno o più pacchetti e selezionare **Aggiorna**. | Nella scheda **Installati** selezionare un pacchetto, registrarne il nome e quindi selezionare **Disinstalla**. Passare alla scheda **Sfoglia**, cercare il nome del pacchetto, selezionarlo e quindi selezionare **Installa**. |
| Interfaccia della riga di comando di nuget.exe | Comando `nuget update` | Per tutti i pacchetti, eliminare la cartella del pacchetto e quindi eseguire `nuget install`. Per un singolo pacchetto, eliminare la cartella del pacchetto e usare `nuget install <id>` per reinstallarla. |

Contenuto dell'articolo:

- [Quando reinstallare un pacchetto](#when-to-reinstall-a-package)
- [Limitazione delle versioni per l'aggiornamento](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Quando reinstallare un pacchetto

1. **Riferimenti interrotti dopo il ripristino del pacchetto**: se è stato aperto un progetto e i pacchetti NuGet sono stati ripristinati, ma sono ancora presenti riferimenti interrotti, provare a reinstallare ognuno dei pacchetti.
1. **Progetto interrotto in seguito all'eliminazione di file**: NuGet non impedisce di rimuovere elementi aggiunti dai pacchetti, pertanto è facile modificare inavvertitamente il contenuto installato da un pacchetto e interrompere il progetto. Per ripristinare il progetto, reinstallare i pacchetti interessati.
1. **Progetto interrotto in seguito a un aggiornamento pacchetto**: se un aggiornamento a un pacchetto comporta l'interruzione di un progetto, l'errore è causato in genere da un pacchetto di dipendenze che potrebbe essere stato a sua volta aggiornato. Per ripristinare lo stato della dipendenza, reinstallare il pacchetto specifico.
1. **Ridestinazione o aggiornamento del progetto**: può essere utile quando un progetto è stato ridestinato o aggiornato e se il pacchetto richiede la reinstallazione a causa di una modifica al framework di destinazione. In questi casi NuGet mostra un errore di compilazione immediatamente dopo la ridestinazione del progetto e avvisi di compilazione successivi informano che il pacchetto potrebbe dover essere reinstallato. Per l'aggiornamento del progetto, NuGet mostra un errore nel log di aggiornamento del progetto.
1. **Reinstallazione di un pacchetto durante lo sviluppo**: gli autori di pacchetti hanno spesso bisogno di reinstallare la stessa versione del pacchetto che stanno sviluppando per testarne il comportamento. Il comando `Install-Package` non fornisce un'opzione per forzare la reinstallazione, pertanto usare `Update-Package -reinstall` in alternativa.

## <a name="constraining-upgrade-versions"></a>Limitazione delle versioni per l'aggiornamento

Per impostazione predefinita, la reinstallazione o l'aggiornamento di un pacchetto installa *sempre* la versione più recente disponibile dall'origine del pacchetto.

Nei progetti che usano il formato di riferimento `packages.config`, tuttavia, è possibile limitare l'intervallo di versioni preso in considerazione. Ad esempio, se si è certi che l'applicazione funziona solo con la versione 1.x di un pacchetto ma non con la versione 2.0 e successive, probabilmente a causa di una modifica importante nell'API del pacchetto, è possibile limitare gli aggiornamenti alle versioni 1.x. Ciò impedisce gli aggiornamenti accidentali che potrebbero causare l'interruzione dell'applicazione.

Per impostare una limitazione, aprire `packages.config` in un editor di testo, individuare la dipendenza in questione e aggiungere l'attributo `allowedVersions` con un intervallo di versioni. Ad esempio, per limitare gli aggiornamenti alla versione 1.x, impostare `allowedVersions` su `[1,2)`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

In tutti i casi, usare la notazione descritta in [Controllo delle versioni dei pacchetti](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-update-package"></a>Uso di Update-Package

Tenendo presenti le [Considerazioni](#considerations) riportate di seguito, è possibile reinstallare facilmente un pacchetto usando il [comando Update-Package](../Tools/ps-ref-update-package.md) nella console di Gestione pacchetti di Visual Studio (**Strumenti** > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**):

```ps
Update-Package -Id <package_name> –reinstall
```

L'uso di questo comando è molto più semplice rispetto alla rimozione di un pacchetto e al successivo tentativo di individuare lo stesso pacchetto nella raccolta NuGet con la stessa versione. Si noti che l'opzione `-Id` è facoltativa.

Lo stesso comando senza `-reinstall` aggiorna un pacchetto a una versione più recente, se applicabile. Il comando restituisce un errore se il pacchetto in questione non è già installato in un progetto, vale a dire `Update-Package` non installa direttamente i pacchetti.

```ps
Update-Package <package_name>
```

Per impostazione predefinita, `Update-Package` influisce su tutti i pacchetti in una soluzione. Per limitare l'azione a un progetto specifico, usare l'opzione `-ProjectName`, con il nome del progetto come viene visualizzato in Esplora soluzioni:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Per *aggiornare* tutti i pacchetti in un progetto (o reinstallarli tramite `-reinstall`), usare `-ProjectName` senza specificare un particolare pacchetto:

```ps
Update-Package -ProjectName MyProject
```

Per aggiornare tutti i pacchetti in una soluzione, è sufficiente usare solo `Update-Package` senza altri argomenti o opzioni. Usare questo modulo con attenzione, perché può richiedere molto tempo per eseguire tutti gli aggiornamenti:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

L'aggiornamento dei pacchetti in un progetto o in una soluzione tramite [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) esegue sempre l'aggiornamento alla versione più recente del pacchetto (esclusi i pacchetti in versione non definitiva). I progetti che usano `packages.config` possono, in caso di necessità, limitare le versioni per l'aggiornamento come descritto in [Limitazione delle versioni per l'aggiornamento](#constraining-upgrade-versions).

Per informazioni dettagliate sul comando, vedere le informazioni di riferimento su [Update-Package](../Tools/ps-ref-update-package.md).

### <a name="considerations"></a>Considerazioni

Durante la reinstallazione di un pacchetto gli aspetti seguenti potrebbero risultare interessati:

1. **Reinstallazione di pacchetti in base alla ridestinazione del framework di destinazione del progetto**
    - In un caso semplice funziona solo la reinstallazione di un pacchetto tramite `Update-Package –reinstall <package_name>`. Un pacchetto che viene installato nell'ambito di un framework di destinazione precedente viene disinstallato e lo stesso pacchetto viene installato con il framework di destinazione corrente del progetto.
    - In alcuni casi potrebbe esserci un pacchetto che non supporta il nuovo framework di destinazione.
        - Se un pacchetto supporta librerie di classi portabili e il progetto viene ridestinato a una combinazione di piattaforme che non sono più supportate dal pacchetto, i riferimenti al pacchetto risulteranno mancanti dopo la reinstallazione.
        - Questo scenario può risultare visibile per i pacchetti che si usano direttamente o per i pacchetti installati come dipendenze. È possibile che il pacchetto usato direttamente supporti il nuovo framework di destinazione, al contrario della relativa dipendenza.
        - Se la reinstallazione dei pacchetti dopo la ridestinazione dell'applicazione comporta errori di runtime o di compilazione, potrebbe essere necessario ripristinare il framework di destinazione o cercare pacchetti alternativi che supportino correttamente il nuovo framework di destinazione.

1. **Aggiunta dell'attributo requireReinstallation in packages.config dopo la ridestinazione o l'aggiornamento del progetto**
    - Se NuGet rileva che i pacchetti sono stati interessati dalla ridestinazione o dall'aggiornamento di un progetto, aggiunge un attributo `requireReinstallation="true"` in `packages.config` a tutti i riferimenti ai pacchetti interessati. Per questo motivo, ogni compilazione successiva in Visual Studio genera avvisi di compilazione per tali pacchetti per ricordare di reinstallarli.

1. **Reinstallazione di pacchetti con dipendenze**
    - `Update-Package –reinstall` reinstalla la stessa versione del pacchetto originale, installando tuttavia la versione più recente delle dipendenze, a meno che non siano state specificate apposite limitazioni per le versioni. In questo modo è possibile aggiornare solo le dipendenze necessarie per risolvere un problema. Tuttavia, se ciò comporta il rollback di una dipendenza a una versione precedente, è possibile usare `Update-Package <dependency_name>` per reinstallare tale dipendenza senza che il pacchetto dipendente sia interessato.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` reinstalla la stessa versione del pacchetto originale, ma senza reinstallare le dipendenze. Usare questa opzione quando l'aggiornamento delle dipendenze del pacchetto potrebbe avere come conseguenza uno stato danneggiato.

1. **Reinstallazione di pacchetti quando sono coinvolte versioni dipendenti**
    - Come descritto in precedenza, la reinstallazione di un pacchetto non modifica le versioni di eventuali altri pacchetti installati che dipendono da esso. È quindi possibile che la reinstallazione di una dipendenza interrompa il pacchetto dipendente.
