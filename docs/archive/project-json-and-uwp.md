---
title: File project.json di NuGet con progetti UWP
description: Descrizione di come il file project.json viene usato per tenere traccia delle dipendenze di NuGet nei progetti UWP (Universal Windows Platform).
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548664"
---
# <a name="projectjson-and-uwp"></a>project.json e UWP

> [!Important]
> Questo contenuto è deprecato. I progetti devono usare i formati `packages.config` o PackageReference.

Questo documento descrive la struttura del pacchetto che usa le funzionalità di NuGet 3+ (Visual Studio 2015 e versioni successive). È possibile impostare la proprietà `minClientVersion` di `.nuspec` su 3.1 per dichiarare che sono necessarie le funzionalità descritte qui.

## <a name="adding-uwp-support-to-an-existing-package"></a>Aggiunta del supporto UWP a un pacchetto esistente

Se è presente un pacchetto e si vuole aggiungere il supporto per le applicazioni UWP, non è necessario adottare il formato dei pacchetti descritto qui. Si deve adottare questo formato solo se sono necessarie le funzionalità descritte e si prevede di usare solo client che hanno eseguito l'aggiornamento alla versione 3+ del client NuGet.

## <a name="i-already-target-netcore45"></a>Si specifica già come destinazione netcore45

Se si specifica già `netcore45` come destinazione e non si ha bisogno di sfruttare queste funzionalità, non è necessaria alcuna azione. I pacchetti `netcore45` possono essere utilizzati dalle applicazioni UWP.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Si vogliono sfruttare le API specifiche di Windows 10

In questo caso è necessario aggiungere il moniker del framework di destinazione `uap10.0` (TFM, Target Framework Moniker, o TxM) al pacchetto. Creare una nuova cartella nel pacchetto e aggiungere a tale cartella l'assembly compilato per usare Windows 10.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Non sono necessarie le API specifiche di Windows 10, ma si vogliono usare le nuove funzionalità .NET o non si ha già netcore45

In questo caso si aggiungerà il moniker TxM `dotnet` al pacchetto. Diversamente da altri TxM, `dotnet` non implica una superficie di attacco o una piattaforma. Il pacchetto funziona su tutte le piattaforme su cui funzionano le dipendenze. Quando si compila un pacchetto con il TxM `dotnet`, è probabile che si abbiano molte più dipendenze specifiche del TxM in `.nuspec`, perché è necessario definire i pacchetti BCL da cui si dipende, ad esempio `System.Text`, `System.Xml` e così via. Il pacchetto opera nelle posizioni in cui operano tali dipendenze.

### <a name="how-do-i-find-out-my-dependencies"></a>Come trovare le dipendenze

Esistono due modi per determinare le dipendenze da elencare:

1. Usare lo strumento **di terze parti** [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator). Lo strumento automatizza il processo e aggiorna il file `.nuspec` con i pacchetti dipendenti in fase di compilazione. È disponibile tramite il pacchetto NuGet [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Difficile) Usare `ILDasm` per esaminare il file `.dll` e verificare quali assembly sono effettivamente necessari in fase di esecuzione. Determinare quindi il pacchetto NuGet da cui proviene ognuno.

Per informazioni dettagliate sulla creazione di un pacchetto che supporta il TxM `dotnet`, vedere l'argomento [`project.json`](project-json.md).

> [!Important]
> Se il pacchetto deve usare progetti PCL, è consigliabile creare una cartella `dotnet` per evitare avvisi e potenziali problemi di compatibilità.

## <a name="directory-structure"></a>Struttura di directory

I pacchetti NuGet che usano questo formato presentano la cartella e i comportamenti noti seguenti:

| Cartella | comportamenti |
| --- | --- |
| Compilazione | Contiene i file di destinazioni e proprietà MSBuild che vengono integrati in modo diverso nel progetto, senza altre modifiche. |
| Strumenti | `install.ps1` e `uninstall.ps1` non vengono eseguiti. `init.ps1` funziona come sempre. |
| Content | Il contenuto non viene copiato automaticamente nel progetto di un utente. Il supporto per l'inclusione di contenuto nel progetto è previsto per una versione successiva. |
| Lib | Per molti pacchetti `lib` funziona come in NuGet 2.x, ma con opzioni espanse per i nomi che possono essere usati e una logica migliore per la selezione della sottocartella corretta quando si utilizzano i pacchetti. Se usata in combinazione con `ref`, la cartella `lib` contiene tuttavia assembly che implementano la superficie di attacco definita dagli assembly nella cartella `ref`. |
| Rif | `ref` è una cartella facoltativa che contiene assembly .NET che definiscono la superficie pubblica (tipi e metodi pubblici) per un'applicazione in cui eseguire la compilazione. Gli assembly in questa cartella possono non avere implementazioni. Vengono usati esclusivamente per definire la superficie di attacco per il compilatore. Se il pacchetto non ha cartelle `ref`, `lib` è sia l'assembly di riferimento che l'assembly di implementazione. |
| Runtimes | `runtimes` è una cartella facoltativa contenente il codice specifico del sistema operativo, ad esempio l'architettura della CPU e i file binari specifici del sistema operativo o in altro modo dipendenti dalla piattaforma. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>File di destinazioni e proprietà MSBuild nei pacchetti

I pacchetti NuGet possono contenere file `.targets` e `.props` che vengono importati nei progetti di MSBuild in cui il pacchetto viene installato. In NuGet 2.x a questo scopo venivano inserite istruzioni `<Import>` nel file `.csproj`. In NuGet 3.0 non è disponibile una specifica azione di "installazione nel progetto". Il processo di ripristino del pacchetto scrive invece due file, `[projectname].nuget.props` e `[projectname].NuGet.targets`.

MSBuild cerca questi due file e li importa automaticamente verso l'inizio e verso la fine del processo di compilazione del progetto. Il comportamento è molto simile a quello di NuGet 2.x, ma con un'importante differenza: *in questo caso non esiste un ordine garantito dei file di destinazioni/proprietà*. MSBuild consente tuttavia di ordinare le destinazioni tramite gli attributi `BeforeTargets` e `AfterTargets` della definizione `<Target>`. Vedere [Elemento Target (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib e Ref

Il comportamento della cartella `lib` non è cambiato di molto in NuGet v3. Tutti gli assembly devono tuttavia essere in sottocartelle denominate in base a un TxM e non possono più essere inseriti direttamente sotto la cartella `lib`. Un TxM è il nome di una piattaforma per cui si suppone che funzioni un determinato asset in un pacchetto. Si tratta ovviamente di un'estensione del moniker del framework di destinazione (TFM, Target Framework Moniker). `net45`, `net46`, `netcore50` e `dnxcore50` sono tutti esempi di TxM. Vedere [Framework di destinazione](../reference/target-frameworks.md). TxM può indicare un framework (TFM), oltre ad altre superfici di attacco specifiche della piattaforma. Il TxM UWP (`uap10.0`), ad esempio, rappresenta la superficie di attacco .NET, oltre alla superficie di attacco Windows per le applicazioni UWP.

Struttura lib di esempio:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

La cartella `lib` contiene assembly usati in fase di esecuzione. Per la maggior parte dei pacchetti, è sufficiente una cartella sotto `lib` per ogni TxM di destinazione.

## <a name="ref"></a>Rif

A volte è necessario usare un assembly diverso durante la compilazione, in questo caso un assembly di riferimento .NET. In questi casi, usare una cartella di primo livello denominata `ref` (abbreviazione per "assembly di riferimento").

La maggior parte degli autori di pacchetti non richiede la cartella `ref`. È utile per i pacchetti che devono fornire una superficie di attacco coerente per la compilazione e IntelliSense, ma hanno implementazioni diverse a seconda del TxM. Il caso d'uso principale sono i pacchetti `System.*` che vengono generati nell'ambito dell'invio di .NET Core in NuGet. Questi pacchetti hanno svariate implementazioni che vengono unificate da un set coerente di assembly di riferimento.

Gli assembly inclusi nella cartella `ref` sono ovviamente gli assembly di riferimento che vengono passati al compilatore. Per chi ha usato csc.exe si tratta degli assembly passati all'[opzione /reference di C#](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option).

La struttura della cartella `ref` è la stessa di `lib`, ad esempio:

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

In questo esempio gli assembly nelle directory `ref` saranno tutti identici.

## <a name="runtimes"></a>Runtimes

La cartella runtimes contiene assembly e librerie native necessari per l'esecuzione in specifici "runtime", definiti in genere dal sistema operativo e dall'architettura della CPU. Questi runtime vengono identificati usando gli [identificatori di runtime](/dotnet/core/rid-catalog), ad esempio `win`, `win-x86`, `win7-x86`, `win8-64` e così via.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Helper nativi per usare API specifiche della piattaforma

L'esempio seguente illustra un pacchetto che ha solo un'implementazione gestita per più piattaforme, ma usa helper nativi in Windows 8 dove può chiamare le API native specifiche di Windows 8.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

Con il pacchetto precedente si verifica quanto segue:

- Se non in Windows 8, viene usato l'assembly `lib/net40/MyLibrary.dll`.

- Se in Windows 8, viene usato `runtimes/win8-<architecture>/lib/MyLibrary.dll` e `native/MyNativeHelper.dll` viene copiato nell'output della compilazione.

Nell'esempio precedente l'assembly `lib/net40` è solo codice gestito, mentre gli assembly nella cartella runtimes useranno p/invoke nell'assembly degli helper nativi per chiamare le API specifiche di Windows 8.

Poiché viene sempre selezionata una sola cartella `lib`, se è presente una cartella specifica del runtime, questa viene preferita a una cartella `lib` non specifica del runtime. La cartella nativa è additiva. Se esiste, viene copiata nell'output della compilazione.

## <a name="managed-wrapper"></a>Wrapper gestito

Un altro modo per usare i runtime consiste nell'inviare un pacchetto che è solo un wrapper gestito tramite un assembly nativo. In questo scenario si crea un pacchetto simile al seguente:

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

In questo caso non sono presenti cartelle `lib` di primo livello uguali a tale cartella perché non esistono implementazioni di questo pacchetto che non si basano sull'assembly nativo corrispondente. Se l'assembly gestito, `MyLibrary.dll`, fosse esattamente lo stesso in entrambi i casi, sarebbe possibile inserirlo in una cartella `lib` di primo livello, ma, poiché l'assenza di un assembly nativo non impedisce la corretta installazione del pacchetto se venisse installato in una piattaforma diversa da win-x86 o win-x64, la cartella lib di primo livello verrebbe usata, ma nessun assembly nativo verrebbe copiato.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>Creazione di pacchetti per NuGet 2 e NuGet 3

Se si vuole creare un pacchetto che possa essere utilizzato dai progetti che usano `packages.config`, oltre a pacchetti che usano `project.json`, si applica quanto descritto di seguito:

- Ref e runtimes funzionano solo in NuGet 3. Vengono entrambi ignorati da NuGet 2.

- Non è possibile basarsi su `install.ps1` o su `uninstall.ps1` per il funzionamento. Questi file vengono eseguiti quando si usa `packages.config`, ma vengono ignorati con `project.json`. È quindi necessario che i pacchetti siano utilizzabili senza eseguirli. `init.ps1` viene ancora eseguito in NuGet 3.

- Poiché l'installazione di file di destinazioni e proprietà è diversa, verificare che il pacchetto funzioni come previsto in entrambi i client.

- Le sottodirectory di lib devono essere un TxM in NuGet 3. Non è possibile inserire librerie nella radice della cartella `lib`.

- Il contenuto non viene copiato automaticamente con NuGet 3. Gli utenti del pacchetto possono copiare manualmente i file o usare uno strumento, ad esempio uno strumento di esecuzione attività, per automatizzare la copia dei file.

- Le trasformazioni dei file di configurazione e di origine non vengono eseguite da NuGet 3.

Se si supportano NuGet 2 e 3, `minClientVersion` dovrà essere la versione più bassa del client NuGet 2 in cui il pacchetto funziona. Nel caso di un pacchetto esistente, non deve essere modificata.
