---
title: Note sulla versione 2.7 di NuGet
description: Note sulla versione per NuGet 2.7 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b7cea360764e1b069afacabadd9b94d87e21ecc
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044984"
---
# <a name="nuget-27-release-notes"></a>Note sulla versione 2.7 di NuGet

[NuGet 2.6.1 delle note sulla versione di WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 note](../release-notes/nuget-2.7.1.md)

2.7 NuGet è stato rilasciato il 22 agosto 2013.

## <a name="acknowledgements"></a>Riconoscimenti

Si ringraziano i collaboratori esterni seguenti per il loro contributo significativo a 2.7 NuGet:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Mostra url licenza quando l'elenco di pacchetti e il livello di dettaglio è dettagliato.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -aggiungere attributo developmentDependency `packages.config` e usarlo nel comando pack includere solo i pacchetti di runtime
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Evitare di chiave duplicata di proprietà nel comando di nuget.exe pack.
4. [Federico Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -aumentare la dimensione della cache di macchina a 200.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -finestra di dialogo NuGet correggere che mostra gli aggiornamenti nella scheda corretta
    - Correzione Project.TargetFramework può essere null in ManagerProgetto
    - [#3248](http://nuget.codeplex.com/workitem/3248) -FindPackage/FindPackagesById correggere SharedPackageRepository avrà esito negativo packageId inesistente
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -abilitare il supporto per il progetto Nomad
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -correzione push comando non riesce con exit codice 0 quando il file non esiste.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -correzione di bug con il comando Add-BindingRedirect quando un progetto fa riferimento a un progetto di database.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -correzione di bug di nuget.pack analisi non corretta di caratteri jolly dell'attributo 'exclude'.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -correzione di bug `NuGet.targets` non passa a nuget.exe $(Platform) durante il ripristino dei pacchetti.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -correzione di bug nel comando di nuget.exe pacchetto cui consentirebbe l'aggiunta di file con lo stesso nome ma con maiuscole/minuscole, alla fine causare eccezione "Elemento esiste già".
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -proprietà Aggiungi versione NetPortableProfile classe.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -correggere bug NullReferenceException se requireApiKey = true, ma l'intestazione X-NUGET-APIKEY non è presente
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -NuGet.Build correzioni destinazioni di file in modo che funzioni correttamente su MonoDevelop
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Migliorare le prestazioni di comando di ripristino, aumentando la parallelizzazione

## <a name="notable-features-in-the-release"></a>Importanti funzionalità nella versione

### <a name="package-restore-by-default-with-implicit-consent"></a>Ripristino del pacchetto per impostazione predefinita (con il consenso implicito)

Introduce un nuovo approccio per il ripristino dei pacchetti NuGet 2.7 e anche supera un ostacolo principale: consenso di ripristino del pacchetto è ora attivata per impostazione predefinita. La combinazione di nuovo approccio e il consenso implicito drasticamente semplifica gli scenari di ripristino del pacchetto.

#### <a name="implicit-consent"></a>Consenso implicito

Con le versioni di NuGet 2.0, 2.1, 2.2, 2.5 e 2.6, gli utenti necessari per consentire in modo esplicito a NuGet di scaricare i pacchetti mancanti durante la compilazione. Se il proprio consenso era stato assegnato in modo esplicito, quindi soluzioni che è stata abilitata ripristino del pacchetto avrà esito negativo compilare fino a quando l'utente ha concesso il consenso.

A partire da NuGet 2.7, consenso di ripristino del pacchetto è impostata su ON per impostazione predefinita, consentendo agli utenti di in modo esplicito *rifiuto* di ripristino del pacchetto se si desidera, utilizzando la casella di controllo nelle impostazioni di NuGet in Visual Studio. Questa modifica il consenso implicito interessa NuGet negli ambienti seguenti:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* Utilità della riga di comando di NuGet.exe

#### <a name="automatic-package-restore-in-visual-studio"></a>Ripristino automatico di pacchetti in Visual Studio

A partire da NuGet 2.7, NuGet scaricherà automaticamente i pacchetti mancanti durante la compilazione in Visual Studio, anche se ripristino del pacchetto non è stato abilitato in modo esplicito per la soluzione. Il ripristino dei pacchetti automatica viene eseguita in Visual Studio quando si compila un progetto o soluzione, ma prima che venga richiamato MSBuild. Questo offre alcuni vantaggi significativi:

1. Senza ulteriore necessario utilizzare l'azione "Abilita ripristino pacchetto NuGet" nella soluzione di
1. Progetti non devono essere modificate e NuGet non apportare modifiche al progetto per assicurarsi di ripristino del pacchetto è abilitato
1. Tutti i pacchetti NuGet, inclusi quelli inclusi importazioni di MSBuild per i file props e le destinazioni, verranno ripristinati *prima* MSBuild viene richiamato, assicurando tali props e le destinazioni sono riconosciute correttamente durante la compilazione

Per utilizzare il ripristino automatico del pacchetto in Visual Studio, è sufficiente eseguire una (operazione in):

1. Non archiviare il `packages` cartella

Esistono diversi modi per omettere i `packages` cartella dal controllo del codice sorgente. Per ulteriori informazioni, vedere il [pacchetti e controllo del codice sorgente](../consume-packages/packages-and-source-control.md) argomento.

Mentre tutti gli utenti sono implicitamente scelto di consenso di ripristino automatico del pacchetto, è possibile facilmente rifiutare esplicitamente tramite le impostazioni di gestione dei pacchetti in Visual Studio.

![Impostazioni di gestione pacchetti](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Ripristino del pacchetto semplificata dalla riga di comando

2.7 NuGet introduce una nuova funzionalità di nuget.exe: `nuget.exe restore`

Questo nuovo comando di ripristino consente di ripristinare facilmente tutti i pacchetti per una soluzione con un unico comando, mediante l'accettazione di un file di soluzione o una cartella come argomento. Inoltre, l'argomento è implicita quando è presente solo una singola soluzione nella cartella corrente. Ciò significa che tutti i seguenti di lavoro da una cartella che contiene un singolo file di soluzione (soluzione. sln):

1. ripristino di NuGet.exe soluzione. sln
1. NuGet.exe restore.
1. ripristino di NuGet.exe

Il comando Restore verrà aprire il file di soluzione e trovare tutti i progetti all'interno della soluzione. Da qui, verranno individuati il `packages.config` per ognuno dei progetti e ripristino di tutti i pacchetti di trovare i file. Consente inoltre di ripristinare i pacchetti a livello di soluzione, vedere il `.nuget\packages.config` file. Ulteriori informazioni sul nuovo comando di ripristino, vedere il [riferimento della riga di comando](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Il nuovo flusso di lavoro ripristino pacchetto

Siamo entusiasti di queste modifiche per il ripristino del pacchetto, come introduce un nuovo flusso di lavoro. Se si desidera omettere i pacchetti dal controllo del codice sorgente è semplicemente non eseguire il commit di `packages` cartella. Gli utenti di Visual Studio aprono e compilano la soluzione visualizzeranno i pacchetti vengono ripristinati automaticamente. Per le compilazioni da riga di comando, è sufficiente richiamare `nuget.exe restore` prima di richiamare `msbuild`. Non è più necessario ricordare di utilizzare l'azione "Abilita ripristino pacchetto NuGet" sulla soluzione e non è necessario modificare i progetti per modificare la compilazione. E questo genera inoltre un'esperienza notevolmente migliorata per i pacchetti che includono le importazioni di MSBuild, in particolare per le importazioni aggiunte tramite funzionalità di recente di NuGet per [importare automaticamente props e le destinazioni file](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) dalla cartella \build.

Oltre a quelle che abbiamo realizzato effettuata, si sta lavorando alcuni partner importante di questo nuovo approccio arrotondare. Per ognuno di questi non sono ancora concrete sequenze temporali, ma ogni partner è interessato poiché sul nuovo approccio.

* Servizio di Team Foundation - lavorano per integrare la chiamata a `nuget.exe restore` nel valore predefinito di scenari di compilazione.
* Siti Web di Azure di Windows - lavorano per consentire di effettuare il push del progetto in Azure e hanno `nuget.exe restore` chiamato prima che il sito web viene compilato.
* TeamCity - si sta aggiornando i plug-in programma di installazione NuGet per TeamCity 8. x
* AppHarbor - lavorano per consentire di eseguire il push del repository in AppHarbor e `nuget.exe restore` chiamato prima che la soluzione sia di compilazione.

Con ogni partner precedente, utilizzerebbe la propria copia di nuget.exe e non è necessario eseguire nuget.exe nella soluzione.

#### <a name="known-issues"></a>Problemi noti

Si sono verificati due problemi noti con nuget.exe restore con la versione 2.7 iniziale, ma sono stati risolti in 6/9/2013 con un aggiornamento per il [NuGet.CommandLine pacchetto](http://www.nuget.org/packages/NuGet.CommandLine/).  Questo aggiornamento è disponibile anche la [pagina di download di NuGet 2.7](https://nuget.codeplex.com/releases/view/107605) su CodePlex.  Esecuzione `nuget.exe update -self` verrà aggiornato alla versione più recente.

Sono stati predefinito:

1. [Ripristino del nuovo pacchetto non viene eseguita sui Mono quando si utilizza il file SLN](https://nuget.codeplex.com/workitem/3596)
1. [Ripristino del pacchetto nuovo non funziona con i progetti di Wix](https://nuget.codeplex.com/workitem/3598)

È inoltre disponibile un problema noto con il nuovo pacchetto ripristino del flusso di lavoro in base al quale [il ripristino automatico del pacchetto non funziona per i progetti in una cartella della soluzione](https://nuget.codeplex.com/workitem/3625). Questo problema è stato risolto in NuGet 2.7.1.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Reindirizzamento e aggiornamento errori o avvisi di compilazione del progetto

Numero di volte dopo il reindirizzamento o l'aggiornamento del progetto, disponibili che alcuni pacchetti NuGet non funzionino correttamente. Sfortunatamente, sarà presente alcuna indicazione di questo oggetto e non vi sarà alcuna indicazione su come risolvere il problema. 2.7 NuGet, è ora utilizzare alcuni eventi di Visual Studio per riconoscere quando è stato ridestinato o aggiornato il progetto in modo che interessa i pacchetti NuGet installati.

Se viene rilevato che uno qualsiasi dei pacchetti sono stato interessato il reindirizzamento o l'aggiornamento, si saranno produrre errori di compilazione immediato per informare gli utenti. Oltre a tale errore immediato, è anche mantengono un `requireReinstallation="true"` flag nel `packages.config` file per tutti i pacchetti che sono stati modificati per il reindirizzamento e ogni successivo di compilazione in Visual Studio genererà avvisi di compilazione per i pacchetti.

Sebbene NuGet non è possibile intervenire automatico per Reinstalla i pacchetti interessati, ci auguriamo che questa indicazione e avviso fornisce le istruzioni della Guida è individuare quando è necessario reinstallare i pacchetti. Anche Microsoft è impegnata [documentazione materiale sussidiario per la reinstallazione del pacchetto](../consume-packages/reinstalling-and-updating-packages.md) che questi messaggi di errore indicato.

### <a name="nuget-configuration-defaults"></a>Impostazioni predefinite di configurazione NuGet

Molte società utilizzano NuGet internamente, ma hanno difficoltà a guidare gli sviluppatori per l'utilizzo dell'origine del pacchetto interno invece nuget.org. 2.7 NuGet introduce una funzionalità di configurazione predefinite che consente valori predefiniti a livello di computer per:

1. Origini pacchetto abilitate
1. Origini pacchetti registrate, ma è disabilitato
1. Origine predefinita nuget.exe push

Ognuno di questi può essere configurato in un file si trova in `%ProgramData%\NuGet\NuGetDefaults.Config`. Se il file di configurazione specifica dell'origine del pacchetto, quindi l'origine del pacchetto nuget.org predefinito non verrà registrato automaticamente, mentre quelle in `NuGetDefaults.Config` verrà registrato.

Sebbene non sia necessario per usare questa funzionalità, è probabile che alle aziende di distribuire `NuGetDefaults.Config` file utilizzando criteri di gruppo.

*Si noti che questa funzionalità non causerà mai un'origine pacchetto essere rimosso dalle impostazioni di NuGet dello sviluppatore. Ciò significa che se lo sviluppatore è già utilizzato NuGet e pertanto è l'origine del pacchetto nuget.org registrato, non verrà rimosso dopo la creazione di un `NuGetDefaults.Config` file.*

Vedere [impostazioni predefinite di configurazione NuGet](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) per ulteriori informazioni su questa funzionalità.

### <a name="renaming-the-default-package-source"></a>Ridenominazione di origine del pacchetto predefinito

NuGet è sempre registrato un'origine del pacchetto predefinito denominata "Origine pacchetto ufficiale NuGet" che punta a nuget.org. Tale nome è stato dettagliato e inoltre non sono state specificate in cui è stato effettivamente verso. Per risolvere i problemi di due, è stato rinominato questa origine pacchetto semplicemente "nuget.org" nell'interfaccia utente. Anche l'URL per l'origine del pacchetto è stato modificato per includere "www". prefisso group. Dopo aver sperimentato 2.7 NuGet, l'origine pacchetto ufficiale"NuGet esistente" verrà automaticamente aggiornato al "nuget.org" come nome e "<https://www.nuget.org/api/v2/>" come relativo URL.

### <a name="performance-improvements"></a>Miglioramenti delle prestazioni

Sono stati apportati alcuni miglioramenti di prestazioni in 2.7 che restituirà footprint di memoria più piccolo, minore utilizzo del disco e l'installazione del pacchetto più veloce. Le query in modo più semplice sono anche apportati ai feed basato su OData che consentiranno di ridurre il payload complessivo.

### <a name="new-extensibility-apis"></a>Nuove API di estensibilità

Abbiamo aggiunto alcune nuove API per i servizi di estendibilità per riempire il gap di funzionalità mancanti nelle versioni precedenti.

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

Questa funzionalità è stato reso disponibile da [Adam Ralph](https://twitter.com/adamralph) e consente agli autori di pacchetti di dichiarare dipendenze utilizzati solo in fase di sviluppo di tempo e non richiedono le dipendenze del pacchetto. Aggiungendo un `developmentDependency="true"` attributo a un pacchetto in `packages.config`, `nuget.exe pack` non includerà il pacchetto come dipendenza.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Rimosso il supporto per Visual Studio 2010 Express per Windows Phone

Il nuovo modello di ripristino del pacchetto in 2.7 è implementato da un nuovo pacchetto VSPackage che è diverso dal NuGet VSPackage principale. A causa di un problema tecnico, non funziona correttamente in questo nuovo VSPackage il *Visual Studio 2010 Express per Windows Phone* SKU come si condivide lo stesso codice di base con altri supportato SKU di Visual Studio. Pertanto, a partire da NuGet 2.7, ci stiamo eliminazione supporto per *Visual Studio 2010 Express per Windows Phone* dall'estensione pubblicata. Supporto per *Visual Studio 2010 Express per Web* è ancora incluso nell'estensione primario pubblicato per la raccolta di estensioni di Visual Studio.

Poiché si è certi quanti gli sviluppatori utilizzano ancora NuGet in tale versione di Visual Studio, stiamo la pubblicazione di un'estensione di Visual Studio separata in modo specifico per gli utenti e pubblicarlo su CodePlex (anziché la raccolta di estensioni di Visual Studio) . Non si intende continuare a mantenere tale estensione, ma se questo si verifica, segnalarlo presentando un problema nel sito Web CodePlex.

Per scaricare Gestione pacchetti NuGet (per Visual Studio 2010 Express per Windows Phone), visitare il [NuGet 2.7 Scarica](https://nuget.codeplex.com/releases/view/107605) pagina.

### <a name="bug-fixes"></a>Correzioni di bug

Oltre a queste funzionalità, questa versione di NuGet include anche molte altre correzioni di bug. Si sono verificati problemi di totali 97 risolti nella versione. Per un elenco completo di lavoro gli elementi corretti in NuGet 2.7,. visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
