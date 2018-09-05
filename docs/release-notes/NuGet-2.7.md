---
title: Note sulla versione 2.7 di NuGet
description: Note sulla versione per NuGet 2.7, inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550965"
---
# <a name="nuget-27-release-notes"></a>Note sulla versione 2.7 di NuGet

[NuGet 2.6.1 per WebMatrix Release Notes](../release-notes/nuget-2.6.1-for-webmatrix.md) | [note sulla versione di NuGet 2.7.1](../release-notes/nuget-2.7.1.md)

NuGet 2.7 è stato rilasciato il 22 agosto 2013.

## <a name="acknowledgements"></a>Riconoscimenti

Vorremmo ringraziare i collaboratori esterni seguenti per i contributi significativi per NuGet 2.7:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostra l'url di licenza quando elenco di pacchetti e livello di dettaglio è descritta in dettaglio.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -aggiungere attributo developmentDependency `packages.config` e usarlo nel comando pack da includere solo i pacchetti di runtime
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evitare di chiave duplicata di proprietà nel comando pack nuget.exe.
4. [Bruno Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -aumentare le dimensioni della cache macchina su 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -finestra di dialogo NuGet correggere con gli aggiornamenti nella scheda errata
    - Può essere null in ManagerProgetto Project.TargetFramework correzione
    - [#3248](http://nuget.codeplex.com/workitem/3248) -correggere SharedPackageRepository FindPackage/FindPackagesById avrà esito negativo in packageId inesistente
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -abilitare il supporto per il progetto Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -correzione push comando non riesce con exit codice 0 quando il file non esiste.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -correzione di bug con il comando Add-BindingRedirect quando un progetto fa riferimento a un progetto di database.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -correzione di bug di nuget.pack con caratteri jolly nell'attributo 'exclude' di analisi in modo non corretto.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -correzione di bug `NuGet.targets` passare $ (Platform) a nuget.exe durante il ripristino dei pacchetti.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -correzione di bug nel comando pacchetto nuget.exe che consentirà di aggiunta di file con lo stesso nome ma con maiuscole e minuscole diverse, infine causano eccezioni "Elemento esiste già".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) : proprietà aggiungere Version alla classe NetPortableProfile.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -correzione del bug NullReferenceException se requireApiKey = true, ma l'intestazione X-NUGET-APIKEY non è presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -corregge NuGet.Build destinazioni file, in modo che funzioni correttamente in MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Migliorare le prestazioni di comando di ripristino, aumentando la parallelizzazione

## <a name="notable-features-in-the-release"></a>Funzionalità di rilievo nella versione

### <a name="package-restore-by-default-with-implicit-consent"></a>Ripristino dei pacchetti per impostazione predefinita (con il consenso implicito)

Introduce un nuovo approccio per ripristino del pacchetto, NuGet 2.7 e consente anche di superare un ostacolo principale: il consenso di ripristino del pacchetto è ora attivata per impostazione predefinita. La combinazione di consenso implicito e il nuovo approccio semplificherà notevolmente gli scenari di ripristino del pacchetto.

#### <a name="implicit-consent"></a>Consenso implicito

Con le versioni di NuGet 2.0, 2.1, 2.2, 2.5 e 2.6, gli utenti necessari per consentire in modo esplicito a NuGet di scaricare i pacchetti mancanti durante la compilazione. Se questo consenso non è stato assegnato in modo esplicito, quindi soluzioni che ha attivato il ripristino dei pacchetti in grado di creare fino a quando l'utente ha concesso il consenso.

A partire da NuGet 2.7, il consenso di ripristino del pacchetto è impostata su ON per impostazione predefinita, consentendo agli utenti in modo esplicito *opt out* di ripristino del pacchetto se si desidera, usando la casella di controllo nelle impostazioni di NuGet in Visual Studio. Questa modifica per il consenso implicito interessa NuGet negli ambienti seguenti:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilità della riga di comando NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Ripristino automatico dei pacchetti in Visual Studio

A partire da NuGet 2.7, NuGet scaricherà automaticamente i pacchetti mancanti durante la compilazione in Visual Studio, anche se il ripristino del pacchetto non è ancora stato abilitato in modo esplicito per la soluzione. Questo ripristino automatico dei pacchetti avviene in Visual Studio quando si compila un progetto o la soluzione, ma prima che MSBuild viene richiamato. Ciò produce alcuni vantaggi significativi:

1. Non è necessario utilizzare il movimento "Abilita ripristino dei pacchetti NuGet" sulla tua soluzione
1. I progetti non devono essere modificati e NuGet non apportare modifiche al progetto per assicurarsi che sia abilitato il ripristino dei pacchetti
1. Tutti i pacchetti NuGet, incluse quelle incluse importazioni MSBuild per i file di proprietà/destinazioni, verranno ripristinati *prima di* MSBuild viene richiamato, assicurando tali proprietà/destinazioni sono riconosciute correttamente durante la compilazione

Per poter usare ripristino automatico dei pacchetti in Visual Studio, è sufficiente eseguire una (azione in):

1. Non si collegano i `packages` cartella

Esistono diversi modi per omettere i `packages` cartella dal controllo del codice sorgente. Per altre informazioni, vedere la [i pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) argomento.

Mentre tutti gli utenti sono implicitamente scelto di consenso di ripristino automatico dei pacchetti, è possibile facilmente rifiutare esplicitamente tramite le impostazioni di gestione pacchetti in Visual Studio.

![Impostazioni di gestione pacchetti](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Ripristino dei pacchetti semplificata dalla riga di comando

NuGet 2.7 introduce una nuova funzionalità per nuget.exe: `nuget.exe restore`

Questo nuovo comando di ripristino consente di ripristinare facilmente tutti i pacchetti per una soluzione con un singolo comando, mediante l'accettazione di un file di soluzione o una cartella come argomento. Inoltre, tale argomento è implicito quando esiste solo un'unica soluzione nella cartella corrente. Ciò significa che tutti i seguenti Usa una cartella che contiene un singolo file di soluzione (soluzione. sln):

1. ripristino NuGet.exe soluzione. sln
1. ripristino NuGet.exe.
1. ripristino NuGet.exe

Il comando Restore verrà aprire il file della soluzione e trovare tutti i progetti all'interno della soluzione. Da qui, verrà trovato il `packages.config` file per ognuno dei progetti e ripristina tutti i pacchetti disponibili. Consente inoltre di ripristinare i pacchetti a livello di soluzione trovata nel `.nuget\packages.config` file. Altre informazioni sul nuovo comando di ripristino sono reperibile nel [Command-Line Reference](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Il nuovo flusso di lavoro ripristino pacchetto

Siamo entusiasti di queste modifiche al ripristino dei pacchetti, perché introduce un nuovo flusso di lavoro. Se si desidera omettere i pacchetti dal controllo del codice sorgente è semplicemente non eseguire il commit di `packages` cartella. Visual Studio utenti aprire e compilare la soluzione visualizzeranno i pacchetti vengono ripristinati automaticamente. Per le compilazioni da riga di comando, è sufficiente richiamare `nuget.exe restore` prima di richiamare `msbuild`. Non è più necessario ricordare di usare il movimento "Abilita ripristino dei pacchetti NuGet" sulla tua soluzione e non sarà non è più necessario modificare i progetti per modificare la compilazione. E anche il risultato è un'esperienza di gran lunga migliore per i pacchetti che includono importazioni MSBuild, in particolare per le importazioni aggiunte tramite funzionalità recenti di NuGet per [automaticamente l'importazione di proprietà/destinazioni file](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) dalla cartella di \build.

Oltre il lavoro che svolto noi stessi, anche lavoriamo con alcuni partner importante per questo nuovo approccio. Non esiste ancora concrete sequenze temporali per ognuno di questi, ma ogni partner è come entusiasti come in questo caso sul nuovo approccio.

* Team Foundation Service - funzionano per integrare la chiamata a `nuget.exe restore` nell'impostazione predefinita gli scenari di compilazione.
* Siti Web di Azure di Windows - funzionano per consentire di eseguire il push al progetto Azure e avere `nuget.exe restore` chiamato prima che il sito web è stato creato.
* TeamCity - si sta aggiornando i plug-in di programma di installazione NuGet per TeamCity 8.x
* AppHarbor - funzionano per consentire di eseguire il push nel repository AppHarbor e avere `nuget.exe restore` chiamato prima che la soluzione sia di compilazione.

Con ogni partner precedente, si utilizzerebbe la propria copia dei nuget.exe e non è necessario eseguire nuget.exe nella soluzione.

#### <a name="known-issues"></a>Problemi noti

Si sono verificati due problemi noti con ripristino nuget.exe con la versione 2.7 iniziale, ma sono stati corretti 9 luglio 6/2013 con un aggiornamento per il [il pacchetto NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/).  Questo aggiornamento è disponibile in anche il [pagina di download di NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) su CodePlex.  Esecuzione `nuget.exe update -self` verrà aggiornato alla versione più recente.

Sono stati fissi:

1. [Nuovo ripristino dei pacchetti non funziona su Mono, quando si usano file SLN](https://nuget.codeplex.com/workitem/3596)
1. [Nuovo ripristino dei pacchetti non funziona con i progetti di Wix](https://nuget.codeplex.com/workitem/3598)

È inoltre disponibile un problema noto con il nuovo pacchetto ripristino del flusso di lavoro in base al quale [ripristino automatico dei pacchetti non funziona per i progetti in una cartella della soluzione](https://nuget.codeplex.com/workitem/3625). Questo problema è stato risolto in NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Gli errori/avvisi di compilazione di ridestinazione del progetto e aggiornamento

Numero di volte dopo la ridestinazione o l'aggiornamento del progetto, individuare che alcuni pacchetti NuGet non funzionino correttamente. Sfortunatamente, è presente alcuna indicazione di questo oggetto e non vi sarà alcuna indicazione su come risolvere il problema. Con NuGet 2.7, è ora usare alcuni eventi di Visual Studio per riconoscere quando è stato ridestinato o aggiornato il progetto in modo che interessa i pacchetti NuGet installati.

Se si rileva che i pacchetti sono stati interessati dalla ridestinazione o aggiornamento, si saranno producono errori di compilazione immediata per informare gli utenti. Oltre all'errore di compilazione immediato, abbiamo inoltre salvare in modo permanente un `requireReinstallation="true"` flag nel `packages.config` file per tutti i pacchetti che sono stati interessati dal reindirizzamento e ogni successivo di compilazione in Visual Studio genera avvisi di compilazione per tali pacchetti.

Anche se NuGet non può intraprendere l'azione automatica per reinstallare i pacchetti interessati, ci auguriamo che questa indicazione e avviso forniranno assistenza è individuare quando è necessario reinstallare i pacchetti. Stiamo anche lavorando [documentazione di materiale sussidiario reinstallazione del pacchetto](../consume-packages/reinstalling-and-updating-packages.md) che questi messaggi di errore indirizzato a.

### <a name="nuget-configuration-defaults"></a>Impostazioni predefinite di configurazione NuGet

Molte aziende usano NuGet internamente, ma hanno avuto difficoltà ad arrivare agli sviluppatori per l'uso dell'origine del pacchetto interno invece di nuget.org. NuGet 2.7 introduce una funzionalità di impostazioni predefinite di configurazione che consente a livello di computer il valore predefinito è possibile specificare per:

1. Origini dei pacchetti abilitata
1. Registrato ma origini pacchetto disabilitate
1. Origine push predefinita nuget.exe

Ognuno di questi è ora possibile configurare all'interno di un file che si trova in `%ProgramData%\NuGet\NuGetDefaults.Config`. Se questo file di configurazione specifica dell'origine del pacchetto, quindi l'origine del pacchetto nuget.org predefinita non verranno registrato automaticamente, mentre quelle in `NuGetDefaults.Config` verrà registrato.

Sebbene non sia necessario per usare questa funzionalità, si prevede che alle aziende di distribuire `NuGetDefaults.Config` di file usando criteri di gruppo.

*Si noti che questa funzionalità non causerà mai un'origine pacchetto essere rimosso dalle impostazioni di NuGet di uno sviluppatore. Ciò significa che se lo sviluppatore è già usato NuGet e pertanto è l'origine del pacchetto nuget.org è registrato, non verrà rimossa dopo la creazione di un `NuGetDefaults.Config` file.*

Visualizzare [impostazioni predefinite di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) per altre informazioni su questa funzionalità.

### <a name="renaming-the-default-package-source"></a>Ridenominazione di origine del pacchetto predefinito

NuGet ha sempre registrato un'origine di pacchetto predefinito denominata "Origine pacchetto ufficiale NuGet" che punta a nuget.org. Questo nome è stato dettagliato e inoltre non specifica dove cui stava puntando effettivamente. Per risolvere tali due problemi, è stata rinominata questa origine pacchetto per semplicemente "nuget.org" nell'interfaccia utente. L'URL per l'origine del pacchetto è stata anche modificata per includere il "www". prefisso group. Dopo aver usato NuGet 2.7, l'origine pacchetto ufficiale"NuGet esistente" verrà aggiornato automaticamente su "nuget.org" come nome e "<https://www.nuget.org/api/v2/>" come l'URL corrispondente.

### <a name="performance-improvements"></a>Miglioramenti delle prestazioni

Abbiamo apportato alcuni miglioramenti delle prestazioni in 2.7 che restituirà footprint di memoria più piccolo, meno l'utilizzo del disco e l'installazione più veloce del pacchetto. Abbiamo anche le query più intelligenti ai feed basato su OData che consentiranno di ridurre il payload complessivo.

### <a name="new-extensibility-apis"></a>Nuove API di estendibilità

Abbiamo aggiunto alcune nuove API per i servizi di estendibilità per riempire i gap di funzionalità mancanti nelle versioni precedenti.

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

### <a name="development-only-dependencies"></a>Dipendenze solo allo sviluppo

Questa funzionalità è stato reso disponibile da [Adam Ralph](https://twitter.com/adamralph) e consente agli autori di dichiarare dipendenze che sono state usate solo in fase di sviluppo di tempo e non richiedono le dipendenze dei pacchetti. Aggiungendo un `developmentDependency="true"` dell'attributo a un pacchetto in `packages.config`, `nuget.exe pack` non comprenderanno più che il pacchetto come dipendenza.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Rimosso il supporto per Visual Studio 2010 Express per Windows Phone

Il nuovo modello di ripristino di pacchetti in 2.7 è implementato da un nuovo pacchetto VSPackage che è diverso dal NuGet VSPackage principale. A causa di un problema tecnico, non funziona correttamente in questo nuovo VSPackage la *Visual Studio 2010 Express per Windows Phone* SKU come si condividono la stessa base di codice con altri SKU di Visual Studio è supportata. Pertanto, a partire da NuGet 2.7, si sta eliminando il supporto per *Visual Studio 2010 Express per Windows Phone* dall'estensione pubblicato. Supporto per *Visual Studio 2010 Express per Web* è ancora incluso nell'estensione primario pubblicato per la raccolta di estensioni di Visual Studio.

Poiché si è certi di quanti sviluppatori siano ancora usando NuGet in quella versione/edizione di Visual Studio, stiamo pubblicazione di un'estensione di Visual Studio separata in modo specifico per gli utenti e pubblicarlo su CodePlex (anziché la raccolta di estensioni di Visual Studio) . Non si intende continuare a mantenere tale estensione, ma se questa influenza è possibile comunicarlo inviando un problema nel sito CodePlex.

Per scaricare Gestione pacchetti NuGet (per Visual Studio 2010 Express per Windows Phone), visitare il [download di NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) pagina.

### <a name="bug-fixes"></a>Correzioni di bug

Oltre a queste funzionalità, questa versione di NuGet include anche molte altre correzioni di bug. Si sono verificati 97 totali problemi risolti nella versione. Per un elenco completo di lavoro elementi di risolti in NuGet 2.7, vista la [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
