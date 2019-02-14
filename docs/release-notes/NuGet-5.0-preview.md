---
title: Note sulla versione 5.0-preview di NuGet
description: Note sulla versione per le anteprime di NuGet 5.0, inclusi i problemi noti, correzioni di bug, nuove funzionalità e dcr.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247659"
---
# <a name="nuget-50-preview-release-notes"></a>Note sulla versione di NuGet 5.0 Preview

## <a name="nuget-50-preview-releases"></a>Versioni di anteprima 5.0 di NuGet

* 13 febbraio 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)
* 23 gennaio 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-3"></a>Riepilogo: What ' s New in NuGet 5.0 Preview 3

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione 

**Bug:**

* nuget.exe /? dovrebbe elencare le versioni corrette di msbuild - [7794 #](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): error : Non è riuscito a trovare una parte del percorso "/ tmp/NuGetScratch - su mono - [7793 #](https://github.com/NuGet/Home/issues/7793)

* ripristino inutilmente enumera il contenuto di tutte le versioni del pacchetto di cui viene fatto riferimento nella cache del computer - [7639 #](https://github.com/NuGet/Home/issues/7639)

* Il rilevamento automatico MSBuild seleziona sempre 16.0 dopo l'installazione e 2019 di anteprima - [7621 #](https://github.com/NuGet/Home/issues/7621)

* elenco del pacchetto dotnet su una soluzione genera voci duplicate per framework - [7607 #](https://github.com/NuGet/Home/issues/7607)

* Eccezione "nome di percorso vuota non è valido" quando IVsPackageInstaller.InstallPackage chiamante nel vecchio progetti e pacchetti di cartella non esiste. - [#5936](https://github.com/NuGet/Home/issues/5936)

* livello di dettaglio di MSBuild /t: Restore minimo deve essere più minimo - [4695 #](https://github.com/NuGet/Home/issues/4695)

**DCRs**

* Consentire agli autori di pacchetti di definire il comportamento transitiva gli asset di compilazione - [6091 #](https://github.com/NuGet/Home/issues/6091)

* Abilitare il ripristino in VS abbia esito positivo se un progetto non fa parte della soluzione o non è stato caricato, ma è stato ripristinato in precedenza - [5820 #](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>Riepilogo: What ' s New in 5.0 Preview 2

### <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

**Bug:**

* Visual Studio alla 16.0 UI NuGet sono disponibili schede illeggibile a causa di problemi di colore - [7735 #](https://github.com/NuGet/Home/issues/7735)

* NuGet. core e un chiarimento License di NuGet. Clients - [7629 #](https://github.com/NuGet/Home/issues/7629)

* Ripristino enumera inutilmente cartella globale dei pacchetti durante il tentativo di determinare il tipo - [7596 #](https://github.com/NuGet/Home/issues/7596)

* Errori di imposizione di file di blocco verranno visualizzate nel finestra Elenco errori - [7429 #](https://github.com/NuGet/Home/issues/7429)

* Risolvere i problemi di NuGet.Configuration - [7326 #](https://github.com/NuGet/Home/issues/7326)

* Adattare all'aggiornamento di MSBuild relativo percorso di installazione.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet.Build.Tasks.Pack deve essere una dipendenza di sviluppo - [7249 #](https://github.com/NuGet/Home/issues/7249)

* Aggiungere il punto di estensione pack per l'inclusione di simboli - debug [7234 #](https://github.com/NuGet/Home/issues/7234)

* dotnet pack deve mantenere l'intervallo di versioni delle dipendenze nel pacchetto nupkg creato. (anche se viene utilizzata la versione a virgola mobile) - [7232 #](https://github.com/NuGet/Home/issues/7232)

* dotnet-restore non riesce in origine autenticata quando config a livello di utente dispone anche di origine - [7209 #](https://github.com/NuGet/Home/issues/7209)

* Service Pack non deve limitare il set di BuildActions per i file di contenuto - [7155 #](https://github.com/NuGet/Home/issues/7155)

* Usa un projectreference che richiede AssetTargetFallback abbia esito positivo, deve avvisare. - [#7137](https://github.com/NuGet/Home/issues/7137)

* Deadlock a causa di problemi relativi al threading durante la chiamata in CPS (CommonProjectSystem) - [7103 #](https://github.com/NuGet/Home/issues/7103)

* aggiungere dotnet pacchetto non verrà usate le credenziali nel file di configurazione globali per un'origine specificata nel file di configurazione locale - [6935 #](https://github.com/NuGet/Home/issues/6935)

* I problemi con MEF in corso di threading chiamato su percorsi del codice asincrono - [6771 #](https://github.com/NuGet/Home/issues/6771)

* Di firma: errore rilevato due volte e senza stack di chiamate - [6455 #](https://github.com/NuGet/Home/issues/6455)

* Installazione di un pacchetto firmato con il certificato di firma non attendibile deve mostrare l'errore - [6318 #](https://github.com/NuGet/Home/issues/6318)

* NuGet in modo non corretto ripristino NOOP quando 2 progetti condividono directory obj - [6114 #](https://github.com/NuGet/Home/issues/6114)

* Non è possibile usare token di accesso personale con dotnet restore in Linux con i pacchetti dal feed autenticati - [5651 #](https://github.com/NuGet/Home/issues/5651)

* dotnet-restore non riesce a causa di disabilitato macchina wide feed - [5410 #](https://github.com/NuGet/Home/issues/5410)

**DCRs**

* Gli assembly di NuGet 5.0 in modo da richiedere .NET 4.7.2 (tramite modifica TFM, target) - [7510 #](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData da NuGet.Packaging deve essere un tipo pubblico. Aggiornare i metadati di licenza acquisiti da spdx. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Rimuovere API obsolete impostazioni - [7294 #](https://github.com/NuGet/Home/issues/7294)

* Soluzione alternativa ripristino timeout nei sistemi con 1 cpu - [6742 #](https://github.com/NuGet/Home/issues/6742)

* NuGet preferenziale per l'autenticazione NTLM, anche se sono presenti credenziali in NuGet. config: aggiungere l'opzione di configurazione per filtrare i tipi di autenticazione per le credenziali - [#5286](https://github.com/NuGet/Home/issues/5286)

* Abilitare EmbedInteropTypes per PackageReference (funzionalità di Packages. config corrispondente) - [2365 #](https://github.com/NuGet/Home/issues/2365)

[Elenco di tutti i problemi risolti in questa versione 5.0.0-preview2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Problemi noti

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>dotnet nuget push --interactive genera un errore in Mac. - [#7519](https://github.com/NuGet/Home/issues/7519)
**Problema** il `--interactive` argomento non viene inoltrato da dotnet cli e genera l'errore `error: Missing value for option 'interactive'` 
 **soluzione alternativa** eseguire qualsiasi altro comando di dotnet con l'opzione interattiva, ad esempio `dotnet restore --interactive` ed eseguire l'autenticazione. L'autenticazione potrebbe essere così memorizzata nella cache dal provider di credenziali. Eseguire quindi `dotnet nuget push`.

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>I pacchetti in FallbackFolders installati da .NET Core SDK hanno un'installazione personalizzata e non superano la convalida della firma. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Problema** quando si usa dotnet.exe 2.x in modo da ripristinare tale netcoreapp a più destinazioni di un progetto 1.x e netcoreapp 2.x, la cartella di fallback viene considerato come un file di feed. Questo significa che, durante il ripristino, NuGet selezionerà il pacchetto dalla cartella di fallback e tenterà di installarlo nella cartella dei pacchetti globale e di eseguire la consueta convalida delle firme che avrà esito negativo.
**Soluzione alternativa** disabilita l'utilizzo della cartella fallback impostando la `RestoreAdditionalProjectSources` su nothing. `<RestoreAdditionalProjectSources/>` Usare con cautela perché ciò causerà il download di numerosi pacchetti da NuGet.org che altrimenti verrebbero ripristinati dalla cartella di fallback.
