---
title: Note sulla versione per NuGet 4.8 RTM
description: Note sulla versione per NuGet 4.8.1 incluse informazioni su problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: d23c4a8874d3d2e1a9ea721c66b15bb458de88a3
ms.sourcegitcommit: 47858da1103848cc1b15bdc00ac7219c0ee4a6a0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/12/2018
ms.locfileid: "44516232"
---
# <a name="nuget-48-rtm-release-notes"></a>Note sulla versione per NuGet 4.8 RTM

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) include la funzionalità NuGet 4.8.

Sono disponibili anche le versioni da riga di comando della stessa funzionalità:
* NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-this-release"></a>Riepilogo: Novità di questa versione
* NuGet.exe supporta ora i nomi lunghi dei file in Windows 10 - [#6937](https://github.com/NuGet/Home/issues/6937)
* I plug-in di autenticazione possono ora essere usati in MSBuild, DotNet.exe, NuGet.exe e Visual Studio, anche tra più piattaforme. La prima generazione di plug-in di autenticazione non era supportata in MSBuild, DotNet.exe. Nota: le build di Visual Studio 2017 15.9 Preview includono il plug-in di autenticazione di Visual Studio Team Services. [#6486](https://github.com/NuGet/Home/issues/6486)
* Il resolver SDK di MSBuild è ora disponibile come parte di NuGet e viene installato con gli strumenti NuGet per Visual Studio. In questo modo si evitano problemi di sincronizzazione delle versioni. [#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference supporta ora i metadati DevelopmentDependency - [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="known-issues"></a>Problemi noti
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>L'installazione di pacchetti firmati in un computer CI o in un ambiente offline richiede più tempo del solito

#### <a name="issue"></a>Problema
Se il computer ha accesso limitato a Internet (ad esempio un computer di compilazione in uno scenario CI/CD), l'installazione o il ripristino di un pacchetto NuGet firmato genererà un avviso ([NU3028](https://docs.microsoft.com/en-us/nuget/reference/errors-and-warnings/nu3028)) dal momento che i server di revoca non sono raggiungibili. Si tratta di una condizione prevista. In alcuni casi, tuttavia, ciò può avere conseguenze impreviste, ad esempio l'installazione o il ripristino del pacchetto richiede più tempo del solito.

#### <a name="workaround"></a>Soluzione alternativa
Eseguire l'aggiornamento a Visual Studio 15.8.4 e NuGet.exe 4.8.1, in cui è stata introdotta una variabile di ambiente per attivare la modalità di controllo delle revoche.
L'impostazione della variabile di ambiente `NUGET_CERT_REVOCATION_MODE` su `offline` forzerà NuGet a controllare lo stato di revoca del certificato solo a fronte dell'elenco di revoche di certificati memorizzato nella cache, pertanto NuGet non tenterà di raggiungere i server di revoca. Quando la modalità di controllo delle revoche è impostata su `offline`, verrà effettuato il downgrade dell'avviso a informazione.

> [!Warning]
> In circostanze normali non è consigliabile impostare la modalità di controllo delle revoche su offline. Così facendo, infatti, NuGet ignorerà il controllo delle revoche online ed eseguirà solo un controllo delle revoche offline a fronte dell'elenco di revoche di certificati memorizzato nella cache, che potrebbe non essere aggiornato. Questo significa che i pacchetti in cui è possibile che il certificato di firma sia stato revocato continueranno a essere installati/ripristinati, mentre non avrebbero dovuto superare il controllo delle revoche ed essere installati.

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>L'opzione `Migrate packages.config to PackageReference...` non è disponibile nel menu di scelta rapida

#### <a name="issue"></a>Problema

Alla prima apertura di un progetto, NuGet potrebbe non essere inizializzato fino all'esecuzione di un'operazione NuGet. Per questo motivo, l'opzione di migrazione non viene visualizzata nel menu di scelta rapida per `packages.config` o `References`.

#### <a name="workaround"></a>Soluzione alternativa

Eseguire una delle azioni NuGet seguenti:
* Aprire l'interfaccia utente di Gestione pacchetti - fare clic con il pulsante destro del mouse su `References` e scegliere `Manage NuGet Packages...`
* Aprire la console di Gestione pacchetti - Da `Tools > NuGet Package Manager` selezionare `Package Manager Console`
* Eseguire un ripristino NuGet - Fare clic con il pulsante destro del mouse sul nodo della soluzione in Esplora soluzioni e scegliere `Restore NuGet Packages`
* Compilare il progetto, ovvero un altro modo per attivare un ripristino NuGet

A questo punto, l'opzione di migrazione dovrebbe essere visibile. Si noti che questa opzione non è supportata e non verrà visualizzata per i tipi di progetto ASP.NET e C++.
Nota: questo problema è stato risolto in Visual Studio 2017 15.9 Preview 3.

## <a name="issues-fixed-in-this-release"></a>Problemi corretti in questa versione

### <a name="bugs"></a>Bug
#### <a name="signing"></a>Firma
* Firma: installazione di un pacchetto firmato in un ambiente offline [#7008](https://github.com/NuGet/Home/issues/7008) - Corretto nella versione 4.8.1
* Firma: controllo dell'URL non corretto - [#7174](https://github.com/NuGet/Home/issues/7174)
* Firma: controllo dell'integrità di un pacchetto in RepositorySignatureVerifier quando il pacchetto è controfirmato nel repository - [#6926](https://github.com/NuGet/Home/issues/6926)
* "Il controllo dell'integrità del pacchetto non è riuscito" dovrebbe includere nel messaggio l'ID pacchetto (e il codice di errore) - [#6944](https://github.com/NuGet/Home/issues/6944)
* Il controllo del pacchetto firmato nel repository consente pacchetti firmati da un certificato diverso - [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - Firma - L'URL di timestamp non può essere https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* Assenza di NullRef in uno scenario di creazione di pacchetti NuSpec, opzioni migliorate - [#6866](https://github.com/NuGet/Home/issues/6866)
* La memoria non è valida durante l'aggiornamento delle informazioni sul firmatario in caso di aggiunta di timestamp alla controfirma - [#6840](https://github.com/NuGet/Home/issues/6840)
* Firma: rimuovere le eccezioni CTL - [#6794](https://github.com/NuGet/Home/issues/6794)
* Firma: contentUrl DEVE essere HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* Firma: SignedPackageVerifierSettings.VSClientDefaultPolicy è inutilizzato - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>Pacchetto
* Il ripristino e la compilazione non sono necessari quando si usa dotnet.exe per comprimere nuspec - [#6866](https://github.com/NuGet/Home/issues/6866)
* Consentire token di sostituzione vuoti in NuspecProperties - [#6722](https://github.com/NuGet/Home/issues/6722)
* PackTask genera un'eccezione NullReferenceException quando viene specificato NuspecProperties - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>Accessibilità
* [Accessibilità] La stringa "Versione provvisoria" sotto il pulsante del pacchetto è coperta dalla descrizione del pacchetto nell'interfaccia utente di Gestione pacchetti - [#4504](https://github.com/NuGet/Home/issues/4504)
* [Accessibilità] Il menu a discesa e il pulsante Impostazioni dell'origine del pacchetto sono troncati quando si seleziona "Microsoft Visual Studio Offline Packages" nell'interfaccia utente di Gestione pacchetti - [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Console di gestione di PowerShell (PMC)
* `Update-Package` ignora l'intervallo di versioni PackageReference - [#6775](https://github.com/NuGet/Home/issues/6775)
* Problema di reinstallazione a livello di soluzione con `Update-Package -reinstall` - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` reinstalla tutti i pacchetti anziché solo quello denominato - [#737](https://github.com/NuGet/Home/issues/737)
* Possibilità di eseguire l'aggiornamento a un pacchetto NuGet non in elenco dalla console di Gestione pacchetti - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>Varie
* Per correggere `NuGet update self` NuGet.Commandline nupkg non deve essere semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* Migliorare le esperienze con gli errori di installazione di NU1107 - [#7107](https://github.com/NuGet/Home/issues/7107)
* La serializzazione di GetAuthenticationCredentialRequest è errata - [#6983](https://github.com/NuGet/Home/issues/6983)
* NuGet Visual Studio AsyncPackage non viene caricato quando è inizializzato all'esterno del thread dell'interfaccia utente - [#6976](https://github.com/NuGet/Home/issues/6976)
* Durante il ripristino vengono segnalati errori fuorvianti sulla necessità di project.json - [#6959](https://github.com/NuGet/Home/issues/6959)
* Interfaccia utente di Gestione pacchetti: pulsante OK in Anteprima modifiche non utilizzabile automaticamente dalla tastiera - [#6893](https://github.com/NuGet/Home/issues/6893)
* RestoreSources ignorati per il progetto con riferimenti p2p - [#6776](https://github.com/NuGet/Home/issues/6776)
* La creazione di un progetto di unit test con il modello .NET Framework aprirà un modello di progetto precedente con packages.config - [#6736](https://github.com/NuGet/Home/issues/6736)
* Consentire al riferimento progetto di eseguire l'override delle dipendenze del pacchetto - [#6536](https://github.com/NuGet/Home/issues/6536)
* Esporre NoDefaultExcludes nell'attività di MSBuild - [#6450](https://github.com/NuGet/Home/issues/6450)
* Il messaggio di stato per "Cancella tutte le cache NuGet" può essere nascosto nel ridimensionamento della finestra - [#5938](https://github.com/NuGet/Home/issues/5938)


[Elenco di tutti i problemi corretti in questa versione](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
