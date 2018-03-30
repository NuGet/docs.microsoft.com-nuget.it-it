---
title: Note sulla versione per NuGet 4.4 RTM | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Note sulla versione per NuGet 4.3 RTM incluse informazioni su problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
keywords: Note sulla versione per NuGet 4.3 RTM, correzioni di bug, problemi noti, funzionalità aggiunte, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6c122dc3d9b576a2ea5f094746a830e5fab5637e
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-44-rtm-release-notes"></a>Note sulla versione per NuGet 4.4 RTM

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include NuGet 4.4 RTM.

## <a name="known-issues"></a>Problemi noti

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>Problemi relativi a .NET 2.0 Standard con .NET Framework e NuGet 

.NET Standard e i relativi strumenti sono stati progettati in modo che i progetti destinati a .NET Framework 4.6.1 possano utilizzare pacchetti e progetti NuGet destinati a .NET Standard 2.0 o versioni precedenti. [Questo documento](https://github.com/dotnet/standard/issues/481) riepiloga i problemi relativi a questo scenario, i piani per risolverli e le soluzioni alternative implementabili allo stato attuale degli strumenti.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Durante l'uso della console di Gestione pacchetti è possibile che il tasto 'INVIO' non funzioni

#### <a name="issue"></a>Problema

A volte, nella console di Gestione pacchetti il tasto INVIO non funziona. Se si riscontra questo problema, controllare lo stato di avanzamento della correzione e fornire altre informazioni utili sui passaggi per riprodurre la condizione di errore. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Soluzione alternativa

Riavviare Visual Studio e aprire la console di Gestione pacchetti prima di aprire la soluzione. In alternativa, provare a eliminare `project.lock.json` e ripetere il ripristino.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Non è possibile visualizzare, aggiungere o aggiornare DotNetCLITools usando Gestione pacchetti NuGet

#### <a name="issue"></a>Problema

Gestione pacchetti NuGet non visualizza e non consente l'aggiunta e/o l'aggiornamento di DotNetCLITools. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Soluzione alternativa

È necessario modificare manualmente DotNetCLIToolReferences nel file di progetto.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>La ridestinazione della versione framework di destinazione può portare a informazioni Intellisense incomplete

#### <a name="issue"></a>Problema

Se in Visual Studio si ridefinisce la destinazione della versione framework di destinazione, le informazioni Intellisense possono risultare incomplete. Questo accade quando si usa PackageReferences come formato di gestione dei pacchetti. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Soluzione alternativa

Eseguire un ripristino manuale.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>Un pacchetto in un progetto .NET Core contenente un assembly con una firma non valida, può causare un ciclo infinito di ripristino

#### <a name="issue"></a>Problema

A volte, quando si usa un pacchetto contenente un assembly con una firma non valida o quando la versione del pacchetto è impostata con tick 'DateTime', è possibile che il processo di ripristino automatico del pacchetto entri in un ciclo infinito (dotnet/project-system#1457).

#### <a name="workaround"></a>Soluzione alternativa

Attualmente non esiste alcuna soluzione.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>Problemi risolti nell'intervallo di tempo NuGet 4.4 RTM

[Note sulla versione per NuGet 4.3 RTM](../release-notes/nuget-4.3-RTM.md) - Vengono elencati tutti i problemi risolti per NuGet 4.3 RTM

### <a name="features"></a>Funzionalità

- Supporto per il caricamento leggero delle soluzioni nella console di Gestione pacchetti e nell'interfaccia utente di Gestione pacchetti NuGet - [#5180](https://github.com/NuGet/Home/issues/5180)

- La destinazione pack di MSBuild deve avere un hook pubblico per l'esecuzione delle destinazioni dell'utente prima di se stessa - [#5143](https://github.com/NuGet/Home/issues/5143)

- Funzionalità: Aggiunta dell'opzione dependencyVersion al comando nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 deve essere mappato a .NET Standard 2.0 per NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)

- Supporto di Visual Studio Build Tools SKU con msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Durante il ripristino viene generato un errore se il supporto di .NET 4.6.1 il per .NET Standard 2.0 è richiesto ma non è installato - [#5325](https://github.com/NuGet/Home/issues/5325)

- Interfaccia utente client per la prenotazione del prefisso dell'ID del pacchetto [#5572](https://github.com/NuGet/Home/issues/5572)

- Distribuire componenti NuGet localizzati per supportare la localizzazione di dotnet.exe - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Bug

- Combinazioni di maiuscole/minuscole diverse nel percorso del progetto possono causare la perdita di riferimenti PackageReference durante il ripristino - [#5855](https://github.com/NuGet/Home/issues/5855)

- Spostare i codici di errore con numeri di avviso nell'intervallo degli errori - [#5824](https://github.com/NuGet/Home/issues/5824)

- Errore fuorviante quando la versione di .NET Standard non è notoriamente compatibile con il framework di destinazione - [#5818](https://github.com/NuGet/Home/issues/5818)

- File di test con testo di licenza confuso: [#5776](https://github.com/NuGet/Home/issues/5776)

- Intestazioni di licenza mancanti in modelli di test EndToEnd - [#5774](https://github.com/NuGet/Home/issues/5774)

- Per il ripristino di packages.config gli errori vengono visualizzati come NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

- Per nuget.exe install è necessario DisableParallelProcessing su Mono - [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe install disabilita in modo non corretto la memorizzazione nella cache - [#5737](https://github.com/NuGet/Home/issues/5737)

- VS: quando si esegue il comando restore per packages.config quando il ripristino è disabilitato viene visualizzato un messaggio non corretto - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS: quando si esegue il comando restore quando il ripristino è disabilitato viene visualizzato un messaggio confuso - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask non riesce quando mancano i metadati della versione - [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet add package può cancellare le righe vuote da un csproj - [#5697](https://github.com/NuGet/Home/issues/5697)

- Per i nomi di origine delle impostazioni delle credenziali in NuGet.config viene fatta distinzione tra maiuscole e minuscole - [#5695](https://github.com/NuGet/Home/issues/5695)

- In seguito all'abilitazione di GeneratePackageOnBuild viene eliminata l'intera cronologia di pacchetti - [#5676](https://github.com/NuGet/Home/issues/5676)

- Il ripristino non consentirà di ripristinare i pacchetti mono.cecil o semver, ma tutti gli altri pacchetti vengono ripristinati. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Errori e avvisi - errore grave quando un'origine non è disponibile.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [Coerenza della progettazione] Attualmente, il testo dello stato di installazione di NuGet non viene visualizzato in modo corretto con il tema scuro. - [#5642](https://github.com/NuGet/Home/issues/5642)

- L'aggiornamento dei pacchetti a livello di soluzione esegue l'aggiornamento/installazione per tutti i progetti - [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet pack si comporta diversamente con TargetFramework o TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)

- Le DLL incluse nella cartella Tools generano avvisi - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel utilizza troppa memoria per le operazioni su stringhe - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux restituisce true per OSX - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet pack' posiziona nuspec in obj invece che in obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget: aggiornamento dei pacchetti estremamente lento - [#4534](https://github.com/NuGet/Home/issues/4534)

- CPS non sincronizzato per il ripristino con soluzioni grandi senza il ripristino leggero delle soluzioni attivato - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - nuget pack con la versione specificata ignora i metadati (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3.+): l'installazione di un pacchetto con numero di versione e flag ExcludeVersion non aggiorna il pacchetto alla versione più recente - [#2405](https://github.com/NuGet/Home/issues/2405)

- Il ripristino di project.json dovrebbe generare un avviso quando i pacchetti di livello superiore violano i vincoli - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile non imposta la configurazione personalizzata per il comando install - [#1646](https://github.com/NuGet/Home/issues/1646)

- L'installazione di nuget.exe non rispetta l'opzione '-DisableParallelProcessing' - [#1556](https://github.com/NuGet/Home/issues/1556)

- Origini disabilitate usate comunque da DotNet.exe o msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)

- Correzione dei blocchi nello scenario di caricamento leggero delle soluzioni - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCR

- Supporto di TargetFramework per nuget.exe install - [#5736](https://github.com/NuGet/Home/issues/5736)

- Aggiungere stringhe diverse per l'agente utente per l'attività MSBuild (.NET Core o Desktop) - [&#5709;](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName deve essere virtuale - [#5700](https://github.com/NuGet/Home/issues/5700)

- [Coerenza della progettazione] Messaggio non chiaro durante l'aggiunta di un pacchetto NuGet - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Avvisi ed errori] NoWarn non viene trasferito in modo transitivo attraverso riferimenti P2P - [#5501](https://github.com/NuGet/Home/issues/5501)

- Caricamento leggero delle soluzioni: core comune per interfaccia utente di Gestione pacchetti, console di Gestione pacchetti e interfacce IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)

- Caricamento leggero delle soluzioni: supporto - Console di Gestione pacchetti - [#5053](https://github.com/NuGet/Home/issues/5053)

- Aggiunta del supporto di una destinazione di MSBuild pre-ripristino attivata da Visual Studio - [#4781](https://github.com/NuGet/Home/issues/4781)

- Aggiunta di una destinazione pubblica a NuGet.targets a cui è possibile fare riferimento tramite BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)

- La destinazione Pack non consente di creare correttamente file di contenuto con le azioni di compilazione - [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blocca thread del pool di thread - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Documentazione per i flag DependencyVersion e Framework del comando Install - [#5858](https://github.com/NuGet/Home/issues/5858)

- Aggiornamento della documentazione per gli avvisi e gli errori NuGet - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>Collegamenti ai problemi di GitHub risolti nella versione 4.4 RTM

[Elenco di problemi 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Elenco di problemi 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Elenco di problemi 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
