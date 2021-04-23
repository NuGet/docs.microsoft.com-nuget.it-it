---
title: Note sulla versione di NuGet 5.0 RTM
description: Note sulla versione per NuGet 5.0, inclusi problemi noti, correzioni di bug, nuove funzionalità e controller di dominio.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 19173d2be7cd66b65651655385466b40f5e08352
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901746"
---
# <a name="nuget-50-release-notes"></a>Note sulla versione di NuGet 5.0

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 versione 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1,</sup> [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installato con il Visual Studio 2019 con carico di lavoro .NET Core 

<sup>2</sup> Disponibile come installazione facoltativa con un carico Visual Studio 2019 con .NET Core

## <a name="summary-whats-new-in-50"></a>Riepilogo: Novità nella versione 5.0

* Supporto per il [ripristino di soluzioni](/visualstudio/ide/filtered-solutions) filtrate in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` la cartella consente ai pacchetti di fornire in modo transitivo destinazioni/proprietà al progetto host [#6091](https://github.com/NuGet/Home/issues/6091)
* Supporto migliore per gli scenari PackageReference nelle API IVs NuGet [-](https://github.com/NuGet/Home/issues/7005)#7005 , [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` è stato deprecato - [#7928](https://github.com/NuGet/Home/issues/7928)
* Il plug-Provider di credenziali gen 1 è stato sostituito da [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) e verrà presto deprecato- [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Quando si esegue un ripristino NoOp, evitare *.dgspec.jsin scrittura nella directory obj - [#7854](https://github.com/NuGet/Home/issues/7854)

* Le autorizzazioni per i file creati all'interno di ~/.nuget sono troppo aperte- [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` non funziona con le origini che necessitano di autenticazione - [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller: la chiamata a un progetto senza riferimenti al pacchetto usa sempre packages.config, anche se il valore predefinito è impostato su PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package reinstallazione non riesce ("Impossibile trovare il pacchetto") nei pacchetti delisted. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Aggiungere un avviso di terze parti nel nostro repo e VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage deve installare la versione più recente quando non viene specificata alcuna [versione, #7493](https://github.com/NuGet/Home/issues/7493)

* Supporto interattivo per dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)

* Quando si esegue il ripristino con il file di blocco, l'avviso NU1603 non deve essere generato. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet non deve stampare il percorso del progetto durante il ripristino con registrazione [minima- #7647](https://github.com/NuGet/Home/issues/7647)

* --interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)

* Aggiungere di nuovo NuGet.Packaging.Core con attr TypeForwardedTo - [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache percorso più breve per funzionare correttamente- [#7770](https://github.com/NuGet/Home/issues/7770)

* Preferire il percorso per l'individuazione msbuild se l'utente non ha chiesto una versione specifica di [msbuild- #7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` dovrebbe elencare le versioni corrette di msbuild [- #7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): errore: Impossibile trovare una parte del percorso '/tmp/NuGetScratch - in mono - [#7793](https://github.com/NuGet/Home/issues/7793)

* restore enumera inutilmente il contenuto di tutte le versioni del pacchetto a cui si fa riferimento nella cache del [computer- #7639](https://github.com/NuGet/Home/issues/7639)

* Il rilevamento automatico di MSBuild seleziona sempre la versione 16.0 dopo l'installazione di VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)

* dotnet list package in una soluzione restituisce voci duplicate per framework - [#7607](https://github.com/NuGet/Home/issues/7607)

* Eccezione "Il nome del percorso vuoto non è valido" quando si chiama IVsPackageInstaller.InstallPackage in progetti e cartella pacchetti non esistenti. - [#5936](https://github.com/NuGet/Home/issues/5936)

* msbuild /t:restore il livello di dettaglio minimo deve essere più minimo [#4695](https://github.com/NuGet/Home/issues/4695)

* L'interfaccia utente NuGet di VS 16.0 ha schede illeggibili a causa di problemi di colore [- #7735](https://github.com/NuGet/Home/issues/7735)

* Chiarimento di NuGet.Core & NuGet.Clients License.txt - [#7629](https://github.com/NuGet/Home/issues/7629)

* Il ripristino enumera inutilmente la cartella globale del pacchetto nel tentativo di determinare il tipo [#7596](https://github.com/NuGet/Home/issues/7596)

* Gli errori di imposizione del file di blocco dovrebbero essere visualizzati nella finestra Elenco errori - [#7429](https://github.com/NuGet/Home/issues/7429)

* Risolvere NuGet.Configproblemi di uration - [#7326](https://github.com/NuGet/Home/issues/7326)

* Adattare a MSBuild aggiornando il percorso di installazione - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [#7249](https://github.com/NuGet/Home/issues/7249)

* Aggiungere il punto di estensione di tipo pack per includere i simboli di debug - [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` deve mantenere l'intervallo di versioni delle dipendenze nell'nupkg creato (anche se viene usata la versione mobile) - [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` ha esito negativo nell'origine autenticata quando anche la configurazione a livello di utente ha origine [#7209](https://github.com/NuGet/Home/issues/7209)

* Pack non deve limitare il set di BuildActions per i file di contenuto - [#7155](https://github.com/NuGet/Home/issues/7155)

* L'uso di projectReference che richiede l'esito positivo di AssetTargetFallback dovrebbe essere avvisato. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock causato da problemi di threading durante la chiamata a CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` non usa le credenziali della configurazione globale per un'origine specificata nella configurazione locale - [#6935](https://github.com/NuGet/Home/issues/6935)

* Problemi di threading relativi alla chiamata di MEF in percorsi di codice asincroni - [#6771](https://github.com/NuGet/Home/issues/6771)

* Firma: errore segnalato due volte e senza stack di chiamate - [#6455](https://github.com/NuGet/Home/issues/6455)

* L'installazione di un pacchetto firmato con un certificato di firma non attendibile dovrebbe visualizzare l'errore [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)

* Non è possibile usare PAT `dotnet restore` con in Linux con pacchetti dal feed autenticato - [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore si verifica un errore a causa di un feed a livello di computer [disabilitato - #5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* Avvisa della rimozione futura di "dotnet pack project.js" - [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Aggiungere un avviso di deprecazione per il plug-in delle credenziali Gen1 - [#7819](https://github.com/NuGet/Home/issues/7819)
 
* Firma: il repository abilitato per richiedere la verifica client di ogni pacchetto come repository firmato -- tramite la risorsa RepositorySignatures/5.0.0 - [#7759](https://github.com/NuGet/Home/issues/7759)

* limitare il numero di richiesta HTTP per ogni origine NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet deve avere come destinazione Net472 (per facilitare la pulizia della build 16.0 di VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: Rimuovere il comando OpenPackagePage - [#7384](https://github.com/NuGet/Home/issues/7384)

* Eseguire il mapping di NetCoreApp 3.0 a NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)

* Aggiungere il supporto netstandard2.0 ai pacchetti NuGet.* - [#6516](https://github.com/NuGet/Home/issues/6516)

* Consentire agli autori di pacchetti di definire il comportamento transitivo degli asset di compilazione [- #6091](https://github.com/NuGet/Home/issues/6091)

* Supporto della funzionalità Filtro soluzione di VS 2019. Supporta anche progetti non presenti nella soluzione o progetti scaricati. È necessario ripristinare prima la soluzione completa (tramite l'interfaccia della riga di comando o Visual [Studio)](https://github.com/NuGet/Home/issues/5820) - #5820

* Assembly NuGet 5.0 per richiedere .NET 4.7.2 (tramite modifica TFM) - [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData di NuGet.Packaging deve essere un tipo pubblico. Aggiornare i metadati delle licenze inseriti da spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Rimuovere le API delle impostazioni obsolete - [#7294](https://github.com/NuGet/Home/issues/7294)

* Soluzione alternativa: timeout di ripristino nei sistemi con 1 cpu [- #6742](https://github.com/NuGet/Home/issues/6742)

* NuGet preferisce l'autenticazione NTLM anche se sono presenti credenziali in NuGet.config - aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)

* Abilitare EmbedInteropTypes per PackageReference (Packages.Config funzionalità) - [#2365](https://github.com/NuGet/Home/issues/2365)

**[Elenco di tutti i problemi risolti in questa versione - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Riepilogo: Novità nella versione 5.0.2

* Sicurezza (se eseguita tramite dotnet.exe o mono.exe): la cartella obj deve essere creata con le autorizzazioni [#7908](https://github.com/NuGet/Home/issues/7908)

* nuget.exe ripristino in mono/MacOS ha esito negativo con nuget.config e `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problemi noti

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problema
Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed. Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.<br>
#### <a name="workaround"></a>Soluzione alternativa
Disabilitare l'utilizzo della cartella di fallback impostando `RestoreAdditionalProjectSources` su nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Usare questa opzione con cautela perché i pacchetti che verrebbero ripristinati dalla cartella di fallback verranno scaricati da NuGet.org.