---
title: Note sulla versione 5.0 RTM di NuGet
description: Note sulla versione per NuGet 5.0 inclusi i problemi noti, correzioni di bug, nuove funzionalità e dcr.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610668"
---
# <a name="nuget-50-release-notes"></a>Note sulla versione 5.0 di NuGet

Veicoli per la distribuzione di NuGet:

| Versione di NuGet | Disponibile nella versione di Visual Studio| Disponibile in .NET SDK|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 version 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>installata con Visual Studio 2019 con carico di lavoro di .NET Core 

<sup>2</sup>disponibile in un'installazione facoltativa con Visual Studio 2019 con carico di lavoro di .NET Core

## <a name="summary-whats-new-in-50"></a>Riepilogo: Quali sono le novità nella versione 5.0

* Supporto per il ripristino [filtrato solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [5820 #](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` cartella consente pacchetti di contribuire in modo transitivo destinazioni/proprietà nel progetto host - [6091 #](https://github.com/NuGet/Home/issues/6091)
* Supporto migliorato per gli scenari di PackageReference NuGet per le API interfacce IVs - [#7005](https://github.com/NuGet/Home/issues/7005), [7493 #](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` è stato deprecato - [7928 #](https://github.com/NuGet/Home/issues/7928)
* Plug-in Provider di credenziali di generazione 1 è stato sostituito da [generazione 2](https://aka.ms/nuget-cross-platform-authentication-plugin) e verrà presto deprecato - [7819 #](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug**

* Quando si esegue un ripristino NoOp, evitare *. dgspec.json scrittura nella directory obj - [7854 #](https://github.com/NuGet/Home/issues/7854)

* Autorizzazioni per i file creati all'interno di ~/.nuget sono troppo open - [7673 #](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` non funziona con origini che richiedono l'autenticazione - [7605 #](https://github.com/NuGet/Home/issues/7605)

* NuGet.VisualStudio.IVsPackageInstaller - chiamata in un progetto con alcun pacchetto fa riferimento sempre Packages. config viene utilizzato, anche se il valore predefinito è impostato su PackageReference - [7005 #](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package reinstallare ha esito negativo ("Impossibile trovare il pacchetto") nel venga rimosso dall'elenco dei pacchetti. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Aggiungi avviso di terze parti nel nostro repository e VSIX - [7409 #](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage consigliabile installare la versione più recente quando nessuna versione di base - [7493 #](https://github.com/NuGet/Home/issues/7493)

* -supporto interattivo per dotnet nuget push - [7519 #](https://github.com/NuGet/Home/issues/7519)

* Durante il ripristino con file di blocco, NU1603 avviso non deve essere generato. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet non deve essere stampata percorso del progetto durante il ripristino con registrazione minima - [7647 #](https://github.com/NuGet/Home/issues/7647)

* -supporto interattivo per dotnet remove package - [7727 #](https://github.com/NuGet/Home/issues/7727)

* Aggiungere nuovo NuGet.Packaging.Core con attrs TypeForwardedTo - [7768 #](https://github.com/NuGet/Home/issues/7768)

* plugins_cache deve percorso più breve per funzionare bene - [7770 #](https://github.com/NuGet/Home/issues/7770)

* Preferire percorso per l'individuazione di msbuild, se l'utente non richieda la versione di msbuild specifica - [7786 #](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` dovrebbe elencare le versioni corrette di msbuild - [7794 #](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error : Non è riuscito a trovare una parte del percorso "/ tmp/NuGetScratch - su mono - [7793 #](https://github.com/NuGet/Home/issues/7793)

* ripristino inutilmente enumera il contenuto di tutte le versioni del pacchetto di cui viene fatto riferimento nella cache del computer - [7639 #](https://github.com/NuGet/Home/issues/7639)

* Il rilevamento automatico MSBuild seleziona sempre 16.0 dopo l'installazione e 2019 di anteprima - [7621 #](https://github.com/NuGet/Home/issues/7621)

* elenco del pacchetto dotnet su una soluzione genera voci duplicate per framework - [7607 #](https://github.com/NuGet/Home/issues/7607)

* Eccezione "nome di percorso vuota non è valido" quando IVsPackageInstaller.InstallPackage chiamante nel vecchio progetti e pacchetti di cartella non esiste. - [#5936](https://github.com/NuGet/Home/issues/5936)

* livello di dettaglio di MSBuild /t: Restore minimo deve essere più minimo - [4695 #](https://github.com/NuGet/Home/issues/4695)

* Visual Studio alla 16.0 UI NuGet sono disponibili schede illeggibile a causa di problemi di colore - [7735 #](https://github.com/NuGet/Home/issues/7735)

* NuGet. core e un chiarimento License di NuGet. Clients - [7629 #](https://github.com/NuGet/Home/issues/7629)

* Ripristino enumera inutilmente cartella globale dei pacchetti durante il tentativo di determinare il tipo - [7596 #](https://github.com/NuGet/Home/issues/7596)

* Errori di imposizione di file di blocco verranno visualizzate nel finestra Elenco errori - [7429 #](https://github.com/NuGet/Home/issues/7429)

* Risolvere i problemi di NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)

* Adattare a MSBuild aggiornamento relativa installazione location - [7325 #](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [7249 #](https://github.com/NuGet/Home/issues/7249)

* Aggiungere il punto di estensione pack per l'inclusione di simboli - debug [7234 #](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` deve mantenere l'intervallo di versioni delle dipendenze nel pacchetto nupkg creato (anche se viene utilizzata la versione a virgola mobile) - [7232 #](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` si verifica un errore nell'origine autenticato quando config a livello di utente dispone anche di origine - [7209 #](https://github.com/NuGet/Home/issues/7209)

* Service Pack non deve limitare il set di BuildActions per i file di contenuto - [7155 #](https://github.com/NuGet/Home/issues/7155)

* Usa un ProjectReference che richiede AssetTargetFallback abbia esito positivo, deve avvisare. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock a causa di problemi relativi al threading durante la chiamata in CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` non utilizzare le credenziali nel file di configurazione globali per un'origine specificata nel file di configurazione locale - [6935 #](https://github.com/NuGet/Home/issues/6935)

* Problemi relativi al threading con MEF chiamato sul async codice percorsi - [6771 #](https://github.com/NuGet/Home/issues/6771)

* Di firma: errore rilevato due volte e senza stack di chiamate - [6455 #](https://github.com/NuGet/Home/issues/6455)

* Installazione di un pacchetto firmato con il certificato di firma non attendibile deve mostrare l'errore - [6318 #](https://github.com/NuGet/Home/issues/6318)

* NuGet in modo non corretto ripristino NOOP quando 2 progetti condividono directory obj - [6114 #](https://github.com/NuGet/Home/issues/6114)

* Non è possibile usare con PAT `dotnet restore` in Linux con i pacchetti dal feed autenticati - [5651 #](https://github.com/NuGet/Home/issues/5651)

* dotnet-restore non riesce a causa di disabilitato macchina wide feed - [5410 #](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Avvisa di futura rimozione di "dotnet pack file Project. JSON" - [7928 #](https://github.com/NuGet/Home/issues/7928)
 
* Aggiungere un avviso di deprecazione per plug-in delle credenziali Gen1 - [7819 #](https://github.com/NuGet/Home/issues/7819)
 
* Firma: Repository abilitato a richiedere la verifica di client di tutti i pacchetti come repository firmato: tramite la risorsa RepositorySignatures/5.0.0 - [7759 #](https://github.com/NuGet/Home/issues/7759)

* limitare il numero di richiesta http per ogni origine tramite NuGet. config - [4538 #](https://github.com/NuGet/Home/issues/4538)

* NuGet deve avere come destinazione Net472 (per consentire la compilazione di VSIX 16,0 pulizia) - [7143 #](https://github.com/NuGet/Home/issues/7143)

* PMC: Comando OpenPackagePage - Rimuovi [7384 #](https://github.com/NuGet/Home/issues/7384)

* Mappa di NetCoreApp 3.0 apportare a NetStandard 2.1 - [7762 #](https://github.com/NuGet/Home/issues/7762)

* Aggiungere il supporto netstandard2.0 pacchetti NuGet.* - [6516 #](https://github.com/NuGet/Home/issues/6516)

* Consentire agli autori di pacchetti di definire il comportamento transitiva gli asset di compilazione - [6091 #](https://github.com/NuGet/Home/issues/6091)

* Supporta funzionalità di filtro di soluzioni di Visual Studio 2019. Supporta anche progetto non in soluzioni o progetti scaricati. È necessario ripristinare innanzitutto - soluzione completa (tramite la CLI o Visual Studio) [5820 #](https://github.com/NuGet/Home/issues/5820)

* Gli assembly di NuGet 5.0 in modo da richiedere .NET 4.7.2 (tramite modifica TFM, target) - [7510 #](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData da NuGet.Packaging deve essere un tipo pubblico. Aggiornare i metadati di licenza acquisiti da spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Rimuovere API obsolete impostazioni - [7294 #](https://github.com/NuGet/Home/issues/7294)

* Soluzione alternativa ripristino timeout nei sistemi con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)

* NuGet preferenziale per l'autenticazione NTLM, anche se sono presenti credenziali in NuGet. config: aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)

* Abilitare EmbedInteropTypes per PackageReference (funzionalità di Packages. config corrispondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)

**[Elenco di tutti i problemi risolti in questa versione - RTM 5.0](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Riepilogo: What ' s New in 5.0.2

* Sicurezza (quando esegue tramite dotnet.exe o mono.exe) - la cartella obj deve essere creata con le autorizzazioni corrette [7908 #](https://github.com/NuGet/Home/issues/7908)

* si verifica un errore di ripristino NuGet.exe in mono/MacOS con NuGet. config personalizzata e `PackageSignatureValidity: False` [8011 #](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Problemi noti

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Problema
Quando si usa dotnet.exe 2.x per ripristinare un progetto destinato sia a netcoreapp 1.x che a netcoreapp 2.x, la cartella di fallback viene considerata come un file di feed. Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.<br>
#### <a name="workaround"></a>Soluzione alternativa
Disabilitare l'utilizzo della cartella fallback impostando la `RestoreAdditionalProjectSources` su nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Utilizzarlo con cautela come ora verranno scaricati i pacchetti che viene ripristinati dalla cartella di fallback da NuGet.org.
