---
title: Note sulla versione di NuGet 2,7
description: Note sulla versione per NuGet 2,7, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780397"
---
# <a name="nuget-27-release-notes"></a>Note sulla versione di NuGet 2,7

Note sulla versione [di NuGet 2.6.1 per WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)  |  [Note sulla versione di NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2,7 è stato rilasciato il 22 agosto 2013.

## <a name="acknowledgements"></a>Riconoscimenti

Vorremmo ringraziare i collaboratori esterni seguenti per i contributi significativi a NuGet 2,7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ( [@mxrss](https://twitter.com/mxrss) )
    - Mostra l'URL della licenza quando si elencano i pacchetti e il livello di dettaglio.
2. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#1956](http://nuget.codeplex.com/workitem/1956) -aggiungere l'attributo developmentDependency a `packages.config` e usarlo nel comando Pack per includere solo i pacchetti di runtime
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ( [@tkrafael](https://twitter.com/tkrafael) )
    - Evitare la chiave delle proprietà duplicate nel comando nuget.exe Pack.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ( [@BenPhegan](https://twitter.com/benphegan) )
    - [#2610](http://nuget.codeplex.com/workitem/2610) aumentare le dimensioni della cache del computer a 200.
5. [Slavia Trenogin](http://www.codeplex.com/site/users/view/derigel) ( [@derigel](https://twitter.com/derigel) )
    - [#3217](http://nuget.codeplex.com/workitem/3217) -correggere la finestra di dialogo NuGet che Mostra gli aggiornamenti nella scheda errata
    - FIX Project. TargetFramework può essere null in ProjectManager
    - [#3248](http://nuget.codeplex.com/workitem/3248) -Fix SharedPackageRepository FindPackage/FindPackagesById avrà esito negativo in packageId non esistenti
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ( [@kevfromireland](https://twitter.com/kevfromireland) )
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Abilita il supporto per il progetto Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ( [@corinblaikie](https://twitter.com/corinblaikie) )
    - [#3252](http://nuget.codeplex.com/workitem/3252) -Fix comando Push ha esito negativo con codice di uscita 0 quando il file non esiste.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -correggere un bug con Add-BindingRedirect comando quando un progetto fa riferimento a un progetto di database.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#2891](http://nuget.codeplex.com/workitem/2891) correggere il problema relativo al carattere jolly di analisi di NuGet. Pack nell'attributo ' exclude ' in modo errato.
10. [Justin Dear](http://www.codeplex.com/site/users/view/zippy1981) ( [@zippy1981](https://twitter.com/zippy1981) )
     - [#3307](http://nuget.codeplex.com/workitem/3307) -Fix bug non `NuGet.targets` passa $ (Platform) a nuget.exe durante il ripristino dei pacchetti.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -Fix bug nel comando nuget.exe Package, che consente di aggiungere file con lo stesso nome ma con maiuscole e minuscole, causando infine l'eccezione "Item exists".
12. [Daniel CAZZULINO](http://www.codeplex.com/site/users/view/dcazzulino) ( [@kzu](https://twitter.com/kzu) )
     - [#2990](http://nuget.codeplex.com/workitem/2990) aggiunta della proprietà Version alla classe NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) correggere il bug NullReferenceException se requireApiKey = true, ma l'intestazione X-NUGET-APIKEY non è presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ( [@friism](https://twitter.com/friism) )
     - [#3278](https://nuget.codeplex.com/workitem/3278) : corregge il file di destinazioni NuGet. Build in in modo che funzioni correttamente in MonoDevelop
15. [](https://www.codeplex.com/site/users/view/pranavkm) Lamartino ( [@pranav_km](https://twitter.com/pranav_km) )
     - Migliorare le prestazioni del comando di ripristino aumentando la parallelizzazione

## <a name="notable-features-in-the-release"></a>Funzionalità rilevanti della versione

### <a name="package-restore-by-default-with-implicit-consent"></a>Ripristino dei pacchetti per impostazione predefinita (con consenso implicito)

NuGet 2,7 introduce un nuovo approccio per il ripristino dei pacchetti, oltre a superare un ostacolo principale: il consenso per il ripristino dei pacchetti è ora attiva per impostazione predefinita. La combinazione del nuovo approccio e del consenso implicito consente di semplificare notevolmente gli scenari di ripristino dei pacchetti.

#### <a name="implicit-consent"></a>Consenso implicito

Con NuGet versioni 2,0, 2,1, 2,2, 2,5 e 2,6, gli utenti hanno dovuto consentire in modo esplicito a NuGet di scaricare i pacchetti mancanti durante la compilazione. Se il consenso non è stato specificato in modo esplicito, le soluzioni che hanno abilitato il ripristino del pacchetto non vengono compilate fino a quando l'utente non ha concesso il consenso.

A partire da NuGet 2,7, il consenso per il ripristino dei pacchetti è ON per impostazione predefinita, consentendo agli utenti di *rifiutare* esplicitamente il ripristino del pacchetto, se lo si desidera, usando la casella di controllo nelle impostazioni di NuGet in Visual Studio. Questa modifica per il consenso implicito influiscono su NuGet negli ambienti seguenti:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilità di nuget.exe Command-Line

#### <a name="automatic-package-restore-in-visual-studio"></a>Ripristino automatico del pacchetto in Visual Studio

A partire da NuGet 2,7, NuGet Scarica automaticamente i pacchetti mancanti durante la compilazione in Visual Studio, anche se il ripristino del pacchetto non è stato abilitato in modo esplicito per la soluzione. Il ripristino automatico dei pacchetti avviene in Visual Studio quando si compila un progetto o la soluzione, ma prima che venga richiamato MSBuild. Questo produce alcuni vantaggi significativi:

1. Non è necessario usare il gesto "Abilita ripristino del pacchetto NuGet" nella soluzione
1. Non è necessario modificare i progetti e NuGet non apporterà modifiche al progetto per assicurarsi che il ripristino dei pacchetti sia abilitato
1. Tutti i pacchetti NuGet, inclusi quelli che includono le importazioni di MSBuild per i file props/targets, verranno ripristinati *prima* che venga richiamato MSBuild, assicurando che tali oggetti/destinazioni vengano riconosciuti correttamente durante la compilazione

Per usare il ripristino automatico del pacchetto in Visual Studio, è sufficiente eseguire un'azione (in):

1. Non archiviare la `packages` cartella

Esistono diversi modi per omettere la `packages` cartella dal controllo del codice sorgente. Per ulteriori informazioni, vedere l'argomento [pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) .

Anche se tutti gli utenti sono implicitamente esplicitamente consentiti al consenso automatico per il ripristino del pacchetto, è possibile rifiutare facilmente le impostazioni di gestione pacchetti in Visual Studio.

![Impostazioni di gestione pacchetti](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Ripristino semplificato dei pacchetti dal Command-Line

NuGet 2,7 introduce una nuova funzionalità per nuget.exe: `nuget.exe restore`

Questo nuovo comando Restore consente di ripristinare facilmente tutti i pacchetti per una soluzione con un unico comando, accettando un file o una cartella della soluzione come argomento. Inoltre, questo argomento è implicito quando è presente una sola soluzione nella cartella corrente. Ciò significa che l'operazione seguente viene eseguita da una cartella che contiene un singolo file di soluzione (la soluzione. sln):

1. nuget.exe ripristinare la soluzione. sln
1. Ripristino nuget.exe.
1. Ripristino nuget.exe

Tramite il comando Restore si aprirà il file della soluzione e si troveranno tutti i progetti all'interno della soluzione. Da qui, troveranno i `packages.config` file per ognuno dei progetti e ripristinerà tutti i pacchetti trovati. Ripristina inoltre i pacchetti a livello di soluzione trovati nel `.nuget\packages.config` file. Ulteriori informazioni sul nuovo comando Restore sono disponibili nella Guida di [riferimento alla riga di comando](../reference/cli-reference/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Nuovo flusso di lavoro di ripristino del pacchetto

Queste modifiche vengono apportate al ripristino del pacchetto, in quanto introduce un nuovo flusso di lavoro. Se si desidera omettere i pacchetti dal controllo del codice sorgente, è sufficiente non eseguire il commit della `packages` cartella. Gli utenti di Visual Studio che aprono e compilano la soluzione vedranno i pacchetti ripristinati automaticamente. Per le compilazioni da riga di comando, è sufficiente richiamare `nuget.exe restore` prima di richiamare `msbuild` . Non è più necessario ricordare di usare il gesto "Abilita ripristino del pacchetto NuGet" nella soluzione e non sarà più necessario modificare i progetti per modificare la compilazione. Questo consente anche di ottenere un'esperienza molto migliorata per i pacchetti che includono importazioni di MSBuild, in particolare per le importazioni aggiunte tramite la funzionalità recente di NuGet per l' [importazione automatica dei file props/targets](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) dalla cartella \Build.

Oltre al lavoro svolto, stiamo lavorando anche con alcuni partner importanti per aggirare questo nuovo approccio. Non sono ancora presenti sequenze temporali concrete per nessuno di questi, ma ogni partner è entusiasta del nuovo approccio.

* Team Foundation Service: lavorano per integrare la chiamata a `nuget.exe restore` negli scenari di compilazione predefiniti.
* Siti Web di Microsoft Azure: consentono di eseguire il push del progetto in Azure e di `nuget.exe restore` chiamare prima della compilazione del sito Web.
* TeamCity-aggiornano il plug-in di programma di installazione NuGet per TeamCity 8. x
* AppHarbor: lavorano per consentire di eseguire il push del repository in AppHarbor e hanno `nuget.exe restore` chiamato prima della compilazione della soluzione.

Con ogni partner precedente, utilizzerebbe la propria copia di nuget.exe e non sarebbe necessario portare nuget.exe nella soluzione.

#### <a name="known-issues"></a>Problemi noti

Si sono verificati due problemi noti con nuget.exe ripristino con la versione iniziale 2,7, ma sono stati corretti in 9/6/2013 con un aggiornamento del [pacchetto NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Questo aggiornamento è disponibile anche nella [pagina di download di NuGet 2,7](https://nuget.codeplex.com/releases/view/107605) su CodePlex.  `nuget.exe update -self`L'esecuzione di eseguirà l'aggiornamento alla versione più recente.

I corretti erano:

1. [Il ripristino di un nuovo pacchetto non funziona in mono quando si usa il file SLN](https://nuget.codeplex.com/workitem/3596)
1. [Il ripristino di un nuovo pacchetto non funziona con i progetti WiX](https://nuget.codeplex.com/workitem/3598)

Esiste anche un problema noto con il nuovo flusso di lavoro di ripristino del pacchetto, in base al quale il [Ripristino automatico dei pacchetti non funziona per i progetti in una cartella della soluzione](https://nuget.codeplex.com/workitem/3625). Questo problema è stato risolto in NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Ridestinazione del progetto e errori/avvisi di compilazione aggiornamento

Molte volte dopo aver ridestinato o aggiornato il progetto, si noterà che alcuni pacchetti NuGet non funzionano correttamente. Sfortunatamente, non è presente alcuna indicazione e non sono disponibili indicazioni su come risolverlo. Con NuGet 2,7, ora si usano alcuni eventi di Visual Studio per riconoscere quando è stata ridestinata o aggiornata il progetto in un modo che influisca sui pacchetti NuGet installati.

Se si rileva che i pacchetti sono stati interessati dalla ridestinazione o dall'aggiornamento, verranno generati errori di compilazione immediati per comunicare. Oltre all'errore di compilazione immediato, viene anche mantenuto un `requireReinstallation="true"` flag nel `packages.config` file per tutti i pacchetti interessati dalla ridestinazione e ogni compilazione successiva in Visual Studio genererà avvisi di compilazione per tali pacchetti.

Anche se NuGet non è in grado di eseguire l'azione automatica per reinstallare i pacchetti interessati, ci auguriamo che questa indicazione e avviso guideranno l'utente per individuare quando è necessario reinstallare i pacchetti. Si sta lavorando anche alla [documentazione delle linee guida per la reinstallazione di pacchetti](../consume-packages/reinstalling-and-updating-packages.md) a cui indirizzare questi messaggi di errore.

### <a name="nuget-configuration-defaults"></a>Impostazioni predefinite di configurazione NuGet

Molte aziende usano NuGet internamente, ma hanno avuto un tempo difficile per consentire agli sviluppatori di usare le origini dei pacchetti interne invece di nuget.org. NuGet 2,7 introduce una funzionalità di impostazioni predefinite di configurazione che consente di specificare valori predefiniti a livello di computer per:

1. Origini pacchetti abilitate
1. Origini pacchetti registrate, ma disabilitate
1. Origine push predefinita nuget.exe

Ognuna di queste impostazioni può ora essere configurata all'interno di un file che si trova in `%ProgramData%\NuGet\NuGetDefaults.Config` . Se questo file di configurazione specifica le origini dei pacchetti, l'origine del pacchetto nuget.org predefinita non verrà registrata automaticamente e le impostazioni in `NuGetDefaults.Config` verranno registrate.

Sebbene non sia necessario utilizzare questa funzionalità, è previsto che le aziende distribuiscano `NuGetDefaults.Config` i file utilizzando criteri di gruppo.

*Si noti che questa funzionalità non comporterà la rimozione di un'origine pacchetto dalle impostazioni NuGet di uno sviluppatore. Ciò significa che se lo sviluppatore ha già usato NuGet e pertanto ha registrato l'origine del pacchetto nuget.org, non verrà rimosso dopo la creazione di un `NuGetDefaults.Config` file.*

Per ulteriori informazioni su questa funzionalità, vedere [impostazioni predefinite della configurazione di NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) .

### <a name="renaming-the-default-package-source"></a>Ridenominazione dell'origine del pacchetto predefinita

NuGet ha sempre registrato un'origine pacchetto predefinita denominata "origine pacchetto ufficiale NuGet" che punta a nuget.org. Il nome è dettagliato e non è stato specificato il punto in cui è stato effettivamente puntato. Per risolvere questi due problemi, l'origine del pacchetto è stata rinominata semplicemente "nuget.org" nell'interfaccia utente. Anche l'URL per l'origine del pacchetto è stato modificato in modo da includere "www". biz:, Dopo aver usato NuGet 2,7, l'"origine del pacchetto ufficiale NuGet" esistente verrà automaticamente aggiornata a "nuget.org" come nome e " <https://www.nuget.org/api/v2/> " come URL.

### <a name="performance-improvements"></a>Miglioramenti alle prestazioni

Si è apportato un miglioramento delle prestazioni in 2,7 che garantisce un footprint di memoria inferiore, meno utilizzo del disco e un'installazione più rapida dei pacchetti. Sono state inoltre apportate query più intelligenti ai feed basati su OData che ridurrà il payload complessivo.

### <a name="new-extensibility-apis"></a>Nuove API di estendibilità

Sono state aggiunte nuove API ai servizi di estendibilità per colmare il gap delle funzionalità mancanti nelle versioni precedenti.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

```cs
// Checks if a NuGet package with the specified Id and version is installed in the specified project.
bool IsPackageInstalledEx(Project project, string id, string versionString);

// Get the list of NuGet packages installed in the specified project.
IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

```cs
// Installs one or more packages that exist on disk in a folder defined in the registry.
void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

// Installs one or more packages that are embedded in a Visual Studio Extension Package.
void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
```

### <a name="development-only-dependencies"></a>Dipendenze Development-Only

Questa funzionalità è stata introdotta da [Adam Ralph](https://twitter.com/adamralph) e consente agli autori di pacchetti di dichiarare dipendenze che sono state usate solo in fase di sviluppo e non richiedono le dipendenze dei pacchetti. `developmentDependency="true"`Se si aggiunge un attributo a un pacchetto in `packages.config` , il `nuget.exe pack` pacchetto non sarà più incluso come dipendenza.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Rimosso il supporto per Visual Studio 2010 Express per Windows Phone

Il nuovo modello di ripristino del pacchetto in 2,7 è implementato da un nuovo VSPackage che è diverso dal VSPackage principale di NuGet. A causa di un problema tecnico, questo nuovo pacchetto VSPackage non funziona correttamente nello SKU di *Visual studio 2010 Express per Windows Phone* perché condivide la stessa codebase con altri SKU di Visual Studio supportati. Quindi, a partire da NuGet 2,7, viene eliminato il supporto per *Visual Studio 2010 Express per Windows Phone* dall'estensione pubblicata. Il supporto per *Visual Studio 2010 Express per il Web* è ancora incluso nell'estensione primaria pubblicata nella raccolta di estensioni di Visual Studio.

Poiché non si è certi del numero di sviluppatori che usano ancora NuGet in tale versione/edizione di Visual Studio, viene pubblicata un'estensione di Visual Studio separata in modo specifico per tali utenti e la pubblicazione su CodePlex, anziché sulla raccolta di estensioni di Visual Studio. Non si prevede di continuare a mantenere questa estensione, ma se si influiscono sul problema si segnala un problema in CodePlex.

Per scaricare gestione pacchetti NuGet (per Visual Studio 2010 Express per Windows Phone), visitare la pagina [download di nuget 2,7](https://nuget.codeplex.com/releases/view/107605) .

### <a name="bug-fixes"></a>Correzioni di bug

Oltre a queste funzionalità, questa versione di NuGet include anche molte altre correzioni di bug. Nella versione sono stati rilevati 97 problemi totali. Per un elenco completo degli elementi di lavoro corretti in NuGet 2,7, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
