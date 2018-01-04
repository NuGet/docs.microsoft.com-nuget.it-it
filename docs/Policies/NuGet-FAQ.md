---
title: Domande frequenti su NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: Domande e risposte frequenti per l'uso di NuGet nella riga di comando e in Visual Studio e per l'uso della raccolta NuGet.
keywords: Domande frequenti NuGet, domande e risposte, problemi comuni, versioni di NuGet, versioni dei pacchetti
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 105fa6e1cad3d163b673376c74ce9c835a0b5059
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-frequently-asked-questions"></a>Domande frequenti su NuGet

Contenuto dell'argomento:

- [Introduzione](#getting-started)
- [NuGet in Visual Studio](#nuget-in-visual-studio)
- [Riga di comando di NuGet](#nuget-command-line)
- [Console di Gestione pacchetti NuGet](#nuget-package-manager-console)
- [Creazione e pubblicazione di pacchetti](#creating-and-publishing-packages)
- [Utilizzo dei pacchetti](#working-with-packages)
- [Gestione dei pacchetti in nuget.org](#managing-packages-on-nugetorg)
- [nuget.org non accessibile](#nugetorg-not-accessible)

## <a name="getting-started"></a>Per iniziare

**Che cos'è richiesto per eseguire NuGet?**

Tutte le informazioni sia sull'interfaccia utente che sugli strumenti da riga di comando sono disponibili in [Installazione degli strumenti client di NuGet](../guides/install-nuget.md).

**NuGet supporta Mono?**

Lo strumento da riga di comando, `nuget.exe`, supporta l'esecuzione e la compilazione in Mono 3.2+ e consente di creare pacchetti in Mono.

Anche se `nuget.exe` funziona in modo ottimale in Windows, esistono alcuni problemi noti in Linux e OS X. Vedere i [problemi relativi a Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) su GitHub.

È disponibile un [client grafico](https://github.com/mrward/monodevelop-nuget-addin) come componente aggiuntivo per MonoDevelop.

**Come è possibile determinare il contenuto di un pacchetto e se è stabile e utile per la mia applicazione?**

La fonte principale di informazioni su un pacchetto è la relativa pagina di presentazione in nuget.org (o un altro feed privato). Ogni pagina di pacchetto in nuget.org include una descrizione del pacchetto, la cronologia delle versioni e le statistiche di utilizzo. La sezione **Info** nella pagina del pacchetto contiene anche un collegamento al sito Web del progetto in cui è in genere possibile trovare numerosi esempi e documentazione per scoprire di più su come viene usato il pacchetto.

Per altre informazioni, vedere [Ricerca e scelta di pacchetti](../Consume-Packages/Finding-and-Choosing-Packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet in Visual Studio

**Come viene supportato NuGet nei diversi prodotti Visual Studio?**

- Visual Studio in Windows supporta l'[interfaccia utente di Gestione pacchetti](../tools/Package-Manager-UI.md) e la [console di Gestione pacchetti](../tools/Package-Manager-Console.md).
- Visual Studio per Mac include funzionalità incorporate di NuGet come descritto in [Inserimento di un pacchetto NuGet nel progetto](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (tutte le piattaforme) non include alcuna integrazione diretta di NuGet. Usare l'[interfaccia della riga di comando di NuGet](../tools/nuget-exe-CLI-Reference.md) o l'[interfaccia della riga di comando di dotnet](../tools/dotnet-commands.md).
- Visual Studio Team Services offre [un passaggio di compilazione per il ripristino dei pacchetti NuGet](https://docs.microsoft.com/vsts/build-release/tasks/package/nuget). È anche possibile [ospitare feed di pacchetti NuGet privati in Team Services](https://www.visualstudio.com/docs/package/nuget/publish).

**Come è possibile controllare la versione esatta degli strumenti di NuGet installati?**

In Visual Studio, usare il comando **Guida > informazioni su Microsoft Visual Studio** e controllare la versione visualizzata accanto a **Gestione pacchetti NuGet**.

In alternativa, avviare la console di Gestione pacchetti (**Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**) e immettere `$host` per visualizzare informazioni su NuGet, compresa la versione.

**Quali linguaggi di programmazione sono supportati da NuGet?**

NuGet funziona in generale per i linguaggi .NET ed è progettato per integrare le librerie .NET in un progetto. Dato che supporta anche l'automazione di MSBuild e Visual Studio in alcuni tipi di progetto, sono supportati anche altri progetti e linguaggi a vari livelli.

La versione più recente di NuGet supporta C#, Visual Basic, F#, WiX e C++.

**Quali modelli di progetto sono supportati da NuGet?**

NuGet offre il supporto completo per un'ampia gamma di modelli di progetto come Windows, Web, Cloud, SharePoint, Wix e così via.

**Qual è la procedura per aggiornare i pacchetti che fanno parte di modelli di Visual Studio?**

Passare alla scheda **Aggiornamenti** nell'interfaccia utente di Gestione pacchetti e selezionare **Aggiorna tutto** oppure usare il [comando `Update-Package`](../Tools/ps-ref-update-package.md) dalla console di Gestione pacchetti.

Per aggiornare il modello stesso, è necessario aggiornare manualmente il repository del modello. Vedere il [blog di Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) su questo argomento. Si noti che questa operazione viene eseguita a proprio rischio, poiché gli aggiornamenti manuali potrebbero danneggiare il modello, se le versioni più recenti di tutte le dipendenze non sono compatibili tra loro.

**È possibile usare NuGet all'esterno di Visual Studio?**

Sì, NuGet funziona direttamente dalla riga di comando. Vedere la [guida all'installazione](../guides/install-nuget.md) e le [informazioni di riferimento sull'interfaccia della riga di comando](../tools/nuget-exe-CLI-Reference.md).

## <a name="nuget-command-line"></a>Riga di comando di NuGet

**Qual è la procedura per ottenere la versione più recente dello strumento da riga di comando di NuGet?**

Vedere la [guida all'installazione](../guides/install-nuget.md).

**È possibile estendere lo strumento da riga di comando di NuGet?**

Sì, è possibile aggiungere comandi personalizzati a `nuget.exe`, come descritto nel [post di Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Console di Gestione pacchetti Nuget (Visual Studio in Windows)

**Qual è la procedura per ottenere l'accesso all'oggetto DTE nella console di Gestione pacchetti**

L'oggetto di primo livello nel modello a oggetti di automazione di Visual Studio viene chiamato oggetto DTE (Development Tools Environment). La console rende disponibile questo oggetto tramite una variabile denominata `$DTE`. Per altre informazioni, vedere [Cenni preliminari sul modello di automazione](https://docs.microsoft.com/visualstudio/extensibility/internals/automation-model-overview) nella documentazione sull'estendibilità di Visual Studio.

**Quando si tenta di eseguire il cast della variabile $DTE al tipo DTE2 viene visualizzato un errore: Impossibile convertire il valore "EnvDTE.DTEClass" di tipo "EnvDTE.DTEClass" al tipo "EnvDTE80.DTE2". Qual è il problema?**

Si tratta di un problema noto correlato alla modalità di interazione di PowerShell con un oggetto COM. Provare quanto segue:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` è una funzione helper aggiunta dall'host di PowerShell di NuGet.

## <a name="creating-and-publishing-packages"></a>Creazione e pubblicazione di pacchetti

**Qual è la procedura per presentare un pacchetto in un feed?**

Vedere [Creare e pubblicare un pacchetto](../quickstart/create-and-publish-a-package.md).

**Sono disponibili più versioni di una libreria destinate a versioni diverse di .NET Framework. Qual è la procedura per compilare un singolo pacchetto che supporti questo scenario?**

Vedere [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Qual è la procedura per configurare un repository o un feed personale?**

Vedere la [panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).

**Qual è la procedura per caricare i pacchetti per il feed di NuGet in blocco?**

Vedere [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Pubblicazione in blocco di pacchetti NuGet) (jeffhandly.com).

## <a name="working-with-packages"></a>Utilizzo dei pacchetti

**Qual è la differenza tra un pacchetto a livello di progetto e un pacchetto a livello di soluzione?**

Un pacchetto a livello di soluzione (NuGet 3.x+) viene installato una sola volta in una soluzione e diventa quindi disponibile per tutti i progetti nella soluzione. Un pacchetto a livello di progetto viene installato in ogni progetto che lo usa. Un pacchetto a livello di soluzione potrebbe anche installare nuovi comandi che possono essere chiamati dall'interno della console di Gestione pacchetti.

**È possibile installare i pacchetti NuGet senza connettività Internet?**

Sì, vedere il post di blog di Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Come accedere a NuGet quando il sito nuget.org non è disponibile oppure sei in aereo) (hanselman.com).

**Qual è la procedura per installare i pacchetti in un percorso diverso rispetto alla cartella packages predefinita?**

Configurare l'impostazione [`repositoryPath`](../Schema/nuget-config-file.md#config-section) in `Nuget.Config` con `nuget config -set repositoryPath=<path>`.

**Come è possibile evitare di aggiungere la cartella dei pacchetti NuGet nel controllo del codice sorgente?**

Impostare [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` su `true`. Questa chiave funziona a livello di soluzione e quindi deve essere aggiunta al file `$(Solutiondir)\.nuget\Nuget.Config`. Quando si abilita il ripristino dei pacchetti da Visual Studio, questo file viene creato automaticamente.

**Qual è la procedura per disattivare il ripristino dei pacchetti?**

Vedere [Abilitazione e disabilitazione del ripristino dei pacchetti](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Perché viene visualizzato un errore "Non è possibile risolvere la dipendenza" durante l'installazione di un pacchetto locale con dipendenze remote?**

È necessario selezionare l'origine **Tutti** quando si installa un pacchetto locale nel progetto. In questo modo vengono aggregati tutti i feed anziché usarne solo uno. Il motivo per cui viene visualizzato questo errore è che gli utenti di un repository locale spesso vogliono evitare l'installazione accidentale di un pacchetto remoto a causa di criteri aziendali.

**Se sono disponibili più progetti nella stessa cartella, in che modo è possibile usare file packages.config separati per ogni progetto?**

Nella maggior parte dei progetti in cui progetti separati risiedono in cartelle separate, questo non costituisce un problema perché NuGet identifica i file `packages.config` in ogni progetto. Con NuGet 3.3 + e più progetti nella stessa cartella, è possibile inserire il nome del progetto nei nomi di file `packages.config` usando il modello `packages.{project-name}.config`, e NuGet usa tale file.

Questo non è un problema quando si usa PackageReference, perché ogni file di progetto contiene il proprio elenco di dipendenze.

**Se nuget.org non compare più nell'elenco dei repository, come è possibile ottenerlo di nuovo?**

- Aggiungere `https://api.nuget.org/v3/index.json` all'elenco di origini, o
- Eliminare `%appdata%\.nuget\NuGet.Config` in modo che NuGet lo crei di nuovo.

**Quali sono le condizioni di licenza predefinite se un pacchetto non include informazioni di licenza specifiche?**

Ogni pacchetto è disciplinato dalle condizioni incluse nel pacchetto. È necessario leggere le condizioni applicabili prima di accedere, scaricare o acquisire qualsiasi pacchetto. In nuget.org, usare il collegamento **License Info** (Informazioni di licenza) nella pagina del pacchetto.

Se per un pacchetto non sono specificate le condizioni di licenza, contattare il proprietario del pacchetto direttamente usando il collegamento **Contact owners** (Contatta proprietari) nella pagina del pacchetto su nuget.org. Microsoft non concede in licenza all'utente alcuna proprietà intellettuale dei provider di pacchetti di terze parti e non è responsabile per le informazioni fornite da terze parti.


## <a name="managing-packages-on-nugetorg"></a>Gestione dei pacchetti in nuget.org

**È possibile modificare i metadati del pacchetto dopo che è stato caricato? Per quale motivo si consiglia di modificare il file nuspec e di caricare un nuovo pacchetto per apportare modifiche ai metadati del pacchetto?**

NuGet implementerà la firma dei pacchetti. Uno dei principi di progettazione della firma dei pacchetti è che il contenuto del pacchetto firmato non deve essere modificabile e ciò include il file nuspec. La modifica dei metadati del pacchetto comporta modifiche al file nuspec, invalidando le firme esistenti. Si consiglia di modificare i flussi di lavoro esistenti in modo da non richiedere la modifica dei metadati del pacchetto dopo aver creato il pacchetto.

Si noti che le dipendenze elencate per il pacchetto vengono generate automaticamente dal pacchetto stesso e non possono essere modificate.

Inoltre, il caricamento dei pacchetti in [staging.nuget.org](http://staging.nuget.org) è un ottimo modo per testare e convalidare il pacchetto senza rendere disponibile un pacchetto nella raccolta pubblica.

**È possibile riservare nomi per i pacchetti che verranno pubblicati in futuro?**

Sì. È possibile riservare ID per i pacchetti in [nuget.org](https://www.nuget.org/) richiedendo un prefisso per l'ID dei pacchetti per l'account. Per richiedere un prefisso per l'ID dei pacchetti, inviare un messaggio di posta elettronica all'account (@) nuget.org con il nome visualizzato del proprietario del pacchetto e il prefisso richiesto.  

**Come è possibile ottenere l'attestazione di proprietà per i pacchetti?**

Vedere [Gestione dei proprietari dei pacchetti in nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Qual è la procedura per gestire il caso di un proprietario di pacchetto che viola una licenza di software?**

Microsoft incoraggia la collaborazione tra i membri della community di NuGet per risolvere eventuali controversie tra i proprietari di pacchetti e i proprietari di altro software. È stato elaborato un [processo di risoluzione delle controversie](../policies/dispute-resolution.md) da seguire prima di chiedere l'intercessione degli amministratori di nuget.org.

**È consigliabile caricare i pacchetti di test in nuget.org?**

Per scopi di test, è possibile usare [staging.nuget.org](http://staging.nuget.org) o server NuGet pubblici alternativi, come [myget.org](https://myget.org) o [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Si noti che i pacchetti caricati in staging.nuget.org potrebbero non essere conservati. Vedere [Goodbye preview.nuget.org](http://blog.nuget.org/20130419/goodbye-preview.html) (Addio preview.nuget.org).

**Quali sono le dimensioni massime per i pacchetti che è possibile caricare in nuget.org?**

nuget.org consente pacchetti fino a 250 MB, ma è consigliabile mantenere dimensioni inferiori a 1 MB per i pacchetti se possibile e usare le dipendenze per collegare i pacchetti. Come regola generale, i pacchetti contengono un solo assembly per evitare conflitti.

NuGet usa HTTP per scaricare i pacchetti, pertanto per i pacchetti di dimensioni maggiori sono più probabili errori di installazione rispetto a quelli più piccoli.

È possibile condividere le dipendenze tra più pacchetti, riducendo le dimensioni totali del download per i consumer dei pacchetti NuGet.

Le dipendenze sono prevalentemente statiche e non cambiano mai. Quando si corregge un bug nel codice, è possibile che non occorra aggiornare le dipendenze. Se si aggregano le dipendenze, alla fine diventa necessario ripubblicare ogni volta pacchetti più grandi. Suddividendo i pacchetti NuGet in dipendenze correlate, gli aggiornamenti sono molto più selezionati per i consumer del pacchetto.

## <a name="nugetorg-not-accessible"></a>nuget.org non accessibile

**Perché non è possibile scaricare o caricare pacchetti in nuget.org?**

Verificare innanzitutto di usare le versioni più recenti di NuGet. Se il problema persiste anche con la versione più recente, [contattare il supporto tecnico](https://www.nuget.org/policies/Contact) e fornire informazioni aggiuntive per la risoluzione del problema di connessione, tra cui:

- Versione di NuGet in uso
- Origini dei pacchetti in uso
- Log di ripristino con livello di dettaglio massimo
- Tracce MTR o Fiddler (vedere più avanti)
- Area geografica
- Versione del sistema operativo
- Configurazione del computer (CPU, rete, disco rigido)
- Se il computer è protetto da proxy o firewall
- Versioni di .NET installate nel computer
- Versioni di strumenti multipiattaforma in uso, ad esempio interfaccia della riga di comando di .NET o DNU

*Per acquisire una traccia MTR:*

- Scaricare WinMTR da [http://winmtr.net/download/](http://winmtr.net/)
- Immettere `api.nuget.org` come nome host e fare clic su **Start** (Avvia).
- Attendere fino a quando il valore indicato nella colonna **Sent** (Inviati) è > = 100.

    ![Acquisizione di una traccia MTR](media/mtr.png)

- Copiare il testo negli Appunti.

*Per acquisire una traccia Fiddler:*

- Installare la versione più recente di [Fiddler](http://www.telerik.com/download/fiddler).
- Avviare Fiddler e disabilitare l'acquisizione del traffico tramite il menu **File > Capture Traffic** (File > Acquisisci traffico).
- Rimuovere tutte le sessioni (selezionare tutti gli elementi nell'elenco e premere **CANC**).
- Configurare Fiddler per acquisire il traffico HTTPS selezionando **Decrypt HTTPS traffic** (Decrittografa traffico HTTPS) nella scheda **HTTPS** nel menu **Tools > Fiddler Options** (Strumenti > Opzioni Fiddler).
- Chiudere Visual Studio.
- Abilitare il menu **File > Capture Traffic** (File > Acquisisci traffico).
- Avviare Visual Studio o nuget.exe ed eseguire le azioni che non funzionano. Il traffico generato da queste azioni dovrebbe essere visualizzato in Fiddler.
- Dopo aver eseguito le azioni, usare **File > Save > All Sessions** (File > Salva > Tutte le sessioni) per archiviare le sessioni acquisite.

Nota: può essere richiesto di impostare la variabile di ambiente `HTTP_PROXY` su `http://127.0.0.1:8888` per il routing del traffico NuGet attraverso Fiddler.

Se il problema persiste, provare i [suggerimenti indicati in questo post di StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Quali sono gli endpoint API per nuget.org?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Si noti che l'API V2 è deprecata e non funziona con NuGet 4+.)
