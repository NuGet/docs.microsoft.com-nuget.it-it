---
title: Note sulla versione per NuGet 4.0 RC
description: Note sulla versione per NuGet 4.0 RC incluse informazioni su problemi noti, correzioni di bug e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780183"
---
# <a name="nuget-40-rc-release-notes"></a>Note sulla versione per NuGet 4.0 RC

[Note sulla versione per NuGet 3.5 RTM](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC per Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) è una versione incentrata sull'aggiunta del supporto per gli scenari principali di .NET Core, sul fornire risposte ai commenti e suggerimenti principali dei clienti e sul miglioramento delle prestazioni in svariati scenari. Questa versione offre diversi miglioramenti come il supporto di PackageReference, i comandi NuGet come destinazioni di MSBuild, il ripristino dei pacchetti in background e altro ancora.

## <a name="bug-fixes"></a>Correzioni di bug

- Modifiche del comportamento in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)

- Errore di nuget.exe restore in computer solo VS "15" - [#3834](https://github.com/NuGet/Home/issues/3834)

- Il comando per la creazione di un nuovo progetto .NETCore dovrebbe bloccare la compilazione durante il ripristino - [#3780](https://github.com/NuGet/Home/issues/3780)

- Con un'app Web ASP.NET Core migrata da VS2015 a VS "15" non è possibile eseguire il ripristino. - [#3773](https://github.com/NuGet/Home/issues/3773)

- [Errore di test] Impossibile disinstallare 'jQuery Validation' del pacchetto con l'interfaccia utente di Gestione pacchetti - [#3755](https://github.com/NuGet/Home/issues/3755)

- Quando si installa un pacchetto nel file `project.json` UWP, dovrebbero essere ripristinati anche i progetti padre - [#3731](https://github.com/NuGet/Home/issues/3731)

- Modificare le destinazioni NuGet per registrare le origini di pacchetti con livello di dettaglio alto invece di normale - [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet
  - dotnetcore pack3 dovrebbe includere la documentazione XML per impostazione predefinita - [#3698](https://github.com/NuGet/Home/issues/3698)

- L'aggiornamento in batch non riesce dall'interfaccia utente quando l'origine senza il pacchetto è la prima e si seleziona l'opzione Tutte le origini - [#3696](https://github.com/NuGet/Home/issues/3696)

- Il comando nuget pack non include tutti i file - [#3678](https://github.com/NuGet/Home/issues/3678)

- Problema di memoria insufficiente - [#3661](https://github.com/NuGet/Home/issues/3661)

- La sezione ProjectFileDependencyGroups del file di asset dovrebbe usare i nomi di libreria per i progetti - [#3611](https://github.com/NuGet/Home/issues/3611)

- "dotnet restore" e ricorsione delle directory - [#3517](https://github.com/NuGet/Home/issues/3517)

- Ripristino: 3 errori vengono registrati come avvisi anziché errori - [#3503](https://github.com/NuGet/Home/issues/3503)

- Problema di TFS: "[file] non è stato trovato nell'area di lavoro o non si dispone delle autorizzazioni per accedervi." - [#2805](https://github.com/NuGet/Home/issues/2805)

- Se si digita "nuget <packagename>" nella casella di ricerca di avvio veloce di VS viene mantenuto il prefisso "nuget " - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException: Elemento radice non riconosciuto nella parte Core Properties. Riga 2, posizione 2. - [#2718](https://github.com/NuGet/Home/issues/2718)

- `.nuspec` con caratteri di escape per &lt; o &gt; nei campi di testo non viene più compilato - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe delete non richiede le credenziali (modalità non interattiva) - [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete genera un avviso per la chiave API per le origini locali, anche se non ha senso - [#2625](https://github.com/NuGet/Home/issues/2625)

- Esperienza insoddisfacente per l'errore durante l'installazione del pacchetto EF -pre - [#2566](https://github.com/NuGet/Home/issues/2566)

- Arresto anomalo di Visual Studio durante il tentativo di modifica della selezione in Gestione pacchetti - [#2551](https://github.com/NuGet/Home/issues/2551)

- dotnet
  - dotnetcore restore esegue ricerche di ID con distinzione tra maiuscole e minuscole nei repository locali con elenco semplice quando si usano le versioni mobili - [#2516](https://github.com/NuGet/Home/issues/2516)

- nuget.exe delete non funziona per il feed V2 - [#2509](https://github.com/NuGet/Home/issues/2509)

- Per il timeout di nuget.exe push è necessario un messaggio di errore migliore - [#2503](https://github.com/NuGet/Home/issues/2503)

- Il ripristino dello strumento senza le direttive imports appropriate ha esito negativo senza messaggi. - [#2462](https://github.com/NuGet/Home/issues/2462)

- NuGet richiede di immettere le credenziali in presenza di un feed privato anche in caso di installazione da nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)

- Il pacchetto ApplicationInsights 2.0 è elencato ma non esiste ancora - [#2317](https://github.com/NuGet/Home/issues/2317)

- UIDelay nel ramo VS "15" preview 5 - [#3500](https://github.com/NuGet/Home/issues/3500)

- Il primo evento OnBuild non viene gestito per il ripristino durante la compilazione per UWP - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 non consente l'installazione di EntityFramework? - [#3312](https://github.com/NuGet/Home/issues/3312)

- Aggiungere l'origine alla registrazione dettagliata (da valutare per 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)

- Parametro NoCache non rispettato nella versione 3.4+ di NuGet - [#3074](https://github.com/NuGet/Home/issues/3074)

- Quando il caricamento di un provider di credenziali non riesce in Visual Studio, non interrompere NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>Funzionalità

- Configurare CI per l'esecuzione x86 - [#3868](https://github.com/NuGet/Home/issues/3868)

- Ripristino automatico 3/3: nessun blocco dall'interfaccia utente - [#3658](https://github.com/NuGet/Home/issues/3658)

- Ripristino automatico 2/3: ripristino in background in caso di nomina - [#3657](https://github.com/NuGet/Home/issues/3657)

- Ripristinare i riferimenti al progetto in modo che corrispondano al comportamento di compilazione (ricorsione) - [#3615](https://github.com/NuGet/Home/issues/3615)

- Supporto DPL in Visual Studio "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- Spostare il file di impostazioni in Programmi - [#3613](https://github.com/NuGet/Home/issues/3613)

- Per le proprietà e le destinazioni di ripristino generate è necessaria la partecipazione a crosstargeting - [#3496](https://github.com/NuGet/Home/issues/3496)

- Supporto di PackageTargetFallback (in precedenza imports) per il ripristino NuGet - [#3494](https://github.com/NuGet/Home/issues/3494)

- Implementazione di ToolsRef - [#3472](https://github.com/NuGet/Home/issues/3472)

- Restore3 per un RID - [#3465](https://github.com/NuGet/Home/issues/3465)

- Supporto nell'interfaccia utente di NuGet di aggiunta/rimozione/aggiornamento dei riferimenti ai pacchetti - [#3457](https://github.com/NuGet/Home/issues/3457)

- Ripristino automatico 1/3: implementazione dell'API per nominare tramite memorizzazione nella cache delle informazioni di ripristino del progetto - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] Attività e destinazioni di ripristino NuGet - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] Abilitare il ripristino a livello di soluzione in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)

- Supporto dell'estendibilità pubblica del provider di credenziali in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)

- Esecuzione ricorsiva di nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)

- Non è possibile caricare Microsoft.TeamFoundation.Client in dev15, è necessario aggiornare Microsoft.TeamFoundation.Client alla versione 15.0 per VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)

- Non è possibile installare il pacchetto di C++ nel progetto UWP C++ in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg deve supportare la cartella \buildCrossTargeting\ e importare `.targets` / `.props` per il "crosstargeting" dell'ambito MSBuild. - [#3499](https://github.com/NuGet/Home/issues/3499)

- Progettazione di ToolsReference - [#3462](https://github.com/NuGet/Home/issues/3462)

- Correggere l'interfaccia utente di NuGet per supportare il ripristino con PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)

- Aggiunta del pulsante per cancellare la cache nelle impostazioni di Gestione pacchetti in VS - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- Il ripristino della soluzione dovrebbe essere bloccato quando è in corso un ripristino automatico. - [#3797](https://github.com/NuGet/Home/issues/3797)

- L'installazione di NetCore dall'interfaccia utente di Gestione pacchetti NuGet viene eseguita in tutti i moniker TFM, invece che solo in quelli supportati dal pacchetto - [#3721](https://github.com/NuGet/Home/issues/3721)

- L'API di denominazione per il ripristino deve supportare anche DotNetCliToolsReferences. - [#3702](https://github.com/NuGet/Home/issues/3702)

- Contrassegnare VSIX "15" come systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- Eseguire la migrazione dai riferimenti a MS.VS.Services.Client a MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- Il comando restore deve rispettare $(RestoreLegacyPackagesDirectory) a livello di progetto - [#3618](https://github.com/NuGet/Home/issues/3618)

- Per il ripristino in un progetto con singolo TargetFramework non devono essere definite condizioni per le proprietà - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet
  - dotnetcore restore3 foo.csproj deve seguire le dipendenze e anche ripristinarle. Come la compilazione. - [#3577](https://github.com/NuGet/Home/issues/3577)

- "type": "platform" Dipendenze rappresentate come "type":"package" in file di blocco - [#2695](https://github.com/NuGet/Home/issues/2695)

- La modalità dettagliata di nuget.exe deve mostrare l'URL di download - [#2629](https://github.com/NuGet/Home/issues/2629)

- Spostare NuGet xplat in Microsoft.NetCore.App e netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- Push - dovrebbe essere possibile eseguire l'override del server di simboli quando di esegue il push dalla riga di comando - [#2348](https://github.com/NuGet/Home/issues/2348)

- Consolidare il codice per la ricerca del percorso dei pacchetti globale - [#2296](https://github.com/NuGet/Home/issues/2296)

- È necessario un nome migliore rispetto a suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)

- Determinare il nome della dipendenza `project.json` da usare per i progetti MSBuild - [#1914](https://github.com/NuGet/Home/issues/1914)

- Aggiungere il supporto di SemVer 2.0.0 a NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- Consentire ai pacchetti NuGet con dipendenza transitiva con `.targets` di essere disponibili in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)

- Il ripristino NuGet da riga di comando è molto più lento rispetto a Visual Studio - [#3330](https://github.com/NuGet/Home/issues/3330)

- Impostare il confronto di versione e ID dei pacchetti in modo da non fare distinzione tra maiuscole e minuscole - [#2522](https://github.com/NuGet/Home/issues/2522)

- L'opzione NoCache non funziona per operazioni di ripristino/installazione basate su `packages.config` (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- Per le risorse FindPackageByIdResource sono necessari un contesto di cache e un logger predefiniti - [#1357](https://github.com/NuGet/Home/issues/1357)
