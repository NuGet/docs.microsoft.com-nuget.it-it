---
title: Note sulla versione di NuGet 5,0 RTM
description: Note sulla versione per NuGet 5,0, inclusi problemi noti, correzioni di bug, nuove funzionalità e DCR.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 52c71c6fe1a1854d5aed229abf2ce7ddc2685ae9
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611330"
---
# <a name="nuget-50-release-notes"></a>Note sulla versione di NuGet 5,0

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16,0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installato con Visual Studio 2019 con carico di lavoro di .NET Core 

<sup>2</sup> Disponibile come installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-50"></a>Riepilogo: novità di 5,0

* Supporto per il ripristino di [soluzioni filtrate](https://docs.microsoft.com/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` cartella consente ai pacchetti di fornire in modo transitivo destinazioni/props al progetto host- [#6091](https://github.com/NuGet/Home/issues/6091)
* Supporto migliore per gli scenari PackageReference nelle API NuGet IV- [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` deprecato- [#7928](https://github.com/NuGet/Home/issues/7928)
* Il plug-in del provider di credenziali di generazione 1 è stato sostituito dalla [generazione 2](https://aka.ms/nuget-cross-platform-authentication-plugin) e sarà presto deprecato- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Quando si esegue un ripristino NoOp, evitare di scrivere *. dgspec. JSON nella directory obj- [#7854](https://github.com/NuGet/Home/issues/7854)

* Le autorizzazioni per i file creati all'interno di ~/.NuGet sono troppo aperte [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` non funziona con le origini che richiedono l'autenticazione [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet. VisualStudio. IVsPackageInstaller-la chiamata di su un progetto senza riferimenti a pacchetti usa sempre Packages. config, anche se il valore predefinito è impostato su PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package REINSTALL non riesce ("Impossibile trovare il pacchetto") nei pacchetti deelencati. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Aggiungere un avviso di terze parti nel repository e in VSIX- [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet. VisualStudio. IVsPackageInstaller. InstallPackage dovrebbe installare la versione più recente se non è stata fornita alcuna versione [#7493](https://github.com/NuGet/Home/issues/7493)

* --supporto interattivo per DotNet NuGet push- [#7519](https://github.com/NuGet/Home/issues/7519)

* Quando si esegue il ripristino con il file di blocco, non è necessario generare l'avviso NU1603. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet non deve stampare il percorso del progetto durante il ripristino con registrazione minima- [#7647](https://github.com/NuGet/Home/issues/7647)

* --supporto interattivo per la rimozione del pacchetto dotnet- [#7727](https://github.com/NuGet/Home/issues/7727)

* Aggiungere di nuovo NuGet. Packaging. Core con TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache richiede un percorso più breve per lavorare correttamente [#7770](https://github.com/NuGet/Home/issues/7770)

* Preferisce il percorso per l'individuazione di MSBuild se l'utente non ha richiesto una versione specifica di MSBuild [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` dovrebbe elencare le versioni corrette di MSBuild- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. targets (498, 5): errore: Impossibile trovare una parte del percorso '/tmp/NuGetScratch-on mono- [#7793](https://github.com/NuGet/Home/issues/7793)

* Restore inutilmente enumera il contenuto di tutte le versioni del pacchetto a cui si fa riferimento nella cache del computer- [#7639](https://github.com/NuGet/Home/issues/7639)

* Il rilevamento automatico di MSBuild seleziona sempre 16,0 dopo l'installazione di Visual Studio 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)

* il pacchetto elenco DotNet in una soluzione restituisce voci duplicate per Framework- [#7607](https://github.com/NuGet/Home/issues/7607)

* Eccezione "il nome del percorso vuoto non è valido" quando si chiama IVsPackageInstaller. InstallPackage nei progetti precedenti e la cartella dei pacchetti non esiste. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: ripristinare il livello di dettaglio minimo dovrebbe essere più [#4695](https://github.com/NuGet/Home/issues/4695) minimo

* Interfaccia utente NuGet di VS 16 con schede illeggibili a causa di problemi di colore: [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. clients License. txt delucidation- [#7629](https://github.com/NuGet/Home/issues/7629)

* Restore inutilmente enumera la cartella globale del pacchetto nel tentativo di determinare il tipo [#7596](https://github.com/NuGet/Home/issues/7596)

* Gli errori relativi all'imposizione dei file di blocco devono essere visualizzati nella finestra Elenco errori- [#7429](https://github.com/NuGet/Home/issues/7429)

* Risolvere i problemi relativi a NuGet. Configuration- [#7326](https://github.com/NuGet/Home/issues/7326)

* Adattarsi a MSBuild aggiornando il percorso di installazione [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack deve essere una dipendenza di sviluppo [#7249](https://github.com/NuGet/Home/issues/7249)

* Aggiungi punto di estensione Pack per includere i simboli di debug- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` deve mantenere l'intervallo di versioni delle dipendenze nel nupkg creato (anche se viene usata la versione mobile)- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` ha esito negativo sull'origine autenticata quando anche la configurazione a livello di utente ha origine- [#7209](https://github.com/NuGet/Home/issues/7209)

* Pack non deve limitare il set di BuildActions per i file di contenuto- [#7155](https://github.com/NuGet/Home/issues/7155)

* L'uso di un ProjectReference che richiede la riuscita di AssetTargetFallback deve essere avvisato. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock a causa di problemi di threading durante la chiamata a CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` non usa le credenziali della configurazione globale per un'origine specificata nella configurazione locale- [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemi di threading con MEF chiamato sui percorsi di codice asincrono- [#6771](https://github.com/NuGet/Home/issues/6771)

* Firma: errore segnalato due volte e senza stack di chiamate- [#6455](https://github.com/NuGet/Home/issues/6455)

* L'installazione di un pacchetto firmato con un certificato di firma non attendibile dovrebbe visualizzare l'errore [#6318](https://github.com/NuGet/Home/issues/6318)

* Il ripristino di NuGet NOOP in modo non corretto quando 2 progetti condividono la directory obj- [#6114](https://github.com/NuGet/Home/issues/6114)

* Non è possibile usare PAT con `dotnet restore` in Linux con pacchetti da [#5651](https://github.com/NuGet/Home/issues/5651) di feed autenticati

* dotnet restore ha esito negativo a causa di un feed [#5410](https://github.com/NuGet/Home/issues/5410) a livello di computer disabilitato

**DCR**

* Avvisa della rimozione futura di "DotNet Pack Project. JSON"- [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Aggiungere un avviso di deprecazione per il plug-in delle credenziali Gen1- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Firma: abilitato repository per richiedere la verifica client di ogni pacchetto come repository firmato-tramite la risorsa RepositorySignatures/5.0.0- [#7759](https://github.com/NuGet/Home/issues/7759)

* limitare il numero di richiesta HTTP per origine tramite NuGet. config- [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet deve avere come destinazione Net472 (per facilitare la pulizia della build 16,0 di VSIX)- [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: rimuovere [#7384](https://github.com/NuGet/Home/issues/7384) comando OpenPackagePage

* Eseguire il mapping di NetCoreApp 3,0 a NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762)

* Aggiungere il supporto di netstandard 2.0 ai pacchetti NuGet. *- [#6516](https://github.com/NuGet/Home/issues/6516)

* Consenti agli autori di pacchetti di definire il comportamento transitivo per gli asset di compilazione- [#6091](https://github.com/NuGet/Home/issues/6091)

* Supporto per la funzionalità filtro della soluzione di Visual Studio 2019. Supporta inoltre il progetto non presente nella soluzione o i progetti scaricati. È necessario ripristinare la soluzione completa (tramite l'interfaccia della riga di comando o Visual Studio) First- [#5820](https://github.com/NuGet/Home/issues/5820)

* Assembly NuGet 5,0 per richiedere 4.7.2 .NET (tramite modifica TFM)- [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData da NuGet. il packaging deve essere un tipo pubblico. Aggiornare i metadati delle licenze inseriti da SPDX. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Rimuovere le API delle impostazioni obsolete- [#7294](https://github.com/NuGet/Home/issues/7294)

* Timeout per il ripristino della soluzione nei sistemi con 1 [#6742](https://github.com/NuGet/Home/issues/6742) CPU

* NuGet preferisce l'autenticazione NTLM anche se sono presenti credenziali in NuGet. config-Aggiungi opzione di configurazione per filtrare i tipi di autenticazione per le credenziali- [#5286](https://github.com/NuGet/Home/issues/5286)

* Abilitare EmbedInteropTypes per PackageReference (funzionalità Packages. config corrispondente)- [#2365](https://github.com/NuGet/Home/issues/2365)

**[Elenco di tutti i problemi risolti in questa versione-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Riepilogo: novità di 5.0.2

* Sicurezza (se eseguita tramite dotnet. exe o mono. exe): la cartella obj deve essere creata con le autorizzazioni corrette [#7908](https://github.com/NuGet/Home/issues/7908)

* il ripristino di NuGet. exe in mono/MacOS ha esito negativo con NuGet. config personalizzato e `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problemi noti

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problema
Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed. Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.<br>
#### <a name="workaround"></a>Soluzione alternativa
Disabilitare l'utilizzo della cartella fallback impostando il `RestoreAdditionalProjectSources` su Nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Usare questa operazione con cautela, perché i pacchetti che verrebbero ripristinati dalla cartella di fallback verranno ora scaricati da NuGet.org.
