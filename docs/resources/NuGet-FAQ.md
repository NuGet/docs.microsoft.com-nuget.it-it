---
title: Domande frequenti su NuGet
description: Domande frequenti e relative risposte per l'uso di NuGet dalla riga di comando e in Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: be24660d05f34242e45f223e2248b943ecc38616
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699650"
---
# <a name="nuget-frequently-asked-questions"></a>Domande frequenti su NuGet

Per le domande frequenti relative a NuGet.org, ad esempio domande sull'account NuGet.org, vedere [Domande frequenti su NuGet.org](../nuget-org/nuget-org-faq.md).

**Che cos'è richiesto per eseguire NuGet?**

Tutte le informazioni sia sull'interfaccia utente che sugli strumenti da riga di comando sono disponibili in [Installazione degli strumenti client di NuGet](../install-nuget-client-tools.md).

**NuGet supporta Mono?**

Lo strumento da riga di comando, `nuget.exe`, supporta l'esecuzione e la compilazione in Mono 3.2+ e consente di creare pacchetti in Mono.

Anche se `nuget.exe` funziona in modo ottimale in Windows, esistono alcuni problemi noti in Linux e OS X. Vedere i [problemi relativi a Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) su GitHub.

È disponibile un [client grafico](https://github.com/mrward/monodevelop-nuget-addin) come componente aggiuntivo per MonoDevelop.

**Come è possibile determinare il contenuto di un pacchetto e se è stabile e utile per la mia applicazione?**

La fonte principale di informazioni su un pacchetto è la relativa pagina di presentazione in nuget.org (o un altro feed privato). Ogni pagina di pacchetto in nuget.org include una descrizione del pacchetto, la cronologia delle versioni e le statistiche di utilizzo. La sezione **Info** nella pagina del pacchetto contiene anche un collegamento al sito Web del progetto in cui è in genere possibile trovare numerosi esempi e documentazione per scoprire di più su come viene usato il pacchetto.

Per altre informazioni, vedere [Ricerca e scelta di pacchetti](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet in Visual Studio

**Come viene supportato NuGet nei diversi prodotti Visual Studio?**

- Visual Studio in Windows supporta l'[interfaccia utente di Gestione pacchetti](../consume-packages/install-use-packages-visual-studio.md) e la [console di Gestione pacchetti](../consume-packages/install-use-packages-powershell.md).
- Visual Studio per Mac include funzionalità incorporate di NuGet come descritto in [Inserimento di un pacchetto NuGet nel progetto](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (tutte le piattaforme) non include alcuna integrazione diretta di NuGet. Usare l'[interfaccia della riga di comando di NuGet](../reference/nuget-exe-cli-reference.md) o l'[interfaccia della riga di comando di dotnet](../reference/dotnet-commands.md).
- Azure DevOps offre [un passaggio di compilazione per il ripristino dei pacchetti NuGet](/vsts/build-release/tasks/package/nuget). È anche possibile [ospitare feed di pacchetti NuGet privati in Azure DevOps](/azure/devops/artifacts/nuget/publish).

**Come è possibile controllare la versione esatta degli strumenti di NuGet installati?**

In Visual Studio, usare il comando **Guida > informazioni su Microsoft Visual Studio** e controllare la versione visualizzata accanto a **Gestione pacchetti NuGet**.

In alternativa, avviare la console di Gestione pacchetti (**Strumenti > Gestione pacchetti NuGet > Console di Gestione pacchetti**) e immettere `$host` per visualizzare informazioni su NuGet, compresa la versione.

**Quali linguaggi di programmazione sono supportati da NuGet?**

NuGet funziona in generale per i linguaggi .NET ed è progettato per integrare le librerie .NET in un progetto. Dato che supporta anche l'automazione di MSBuild e Visual Studio in alcuni tipi di progetto, sono supportati anche altri progetti e linguaggi a vari livelli.

La versione più recente di NuGet supporta C#, Visual Basic, F#, WiX e C++.

**Quali modelli di progetto sono supportati da NuGet?**

NuGet offre il supporto completo per un'ampia gamma di modelli di progetto come Windows, Web, Cloud, SharePoint, Wix e così via.

**Qual è la procedura per aggiornare i pacchetti che fanno parte di modelli di Visual Studio?**

Passare alla scheda **Aggiornamenti** nell'interfaccia utente di Gestione pacchetti e selezionare **Aggiorna tutto** oppure usare il [comando `Update-Package`](../reference/ps-reference/ps-ref-update-package.md) dalla console di Gestione pacchetti.

Per aggiornare il modello stesso, è necessario aggiornare manualmente il repository del modello. Vedere il [blog di Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) su questo argomento. Si noti che questa operazione viene eseguita a proprio rischio, poiché gli aggiornamenti manuali potrebbero danneggiare il modello, se le versioni più recenti di tutte le dipendenze non sono compatibili tra loro.

**È possibile usare NuGet all'esterno di Visual Studio?**

Sì, NuGet funziona direttamente dalla riga di comando. Vedere la [guida all'installazione](../install-nuget-client-tools.md) e le [informazioni di riferimento sull'interfaccia della riga di comando](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>Riga di comando di NuGet

**Qual è la procedura per ottenere la versione più recente dello strumento da riga di comando di NuGet?**

Vedere la [guida all'installazione](../install-nuget-client-tools.md). Per controllare la versione installata corrente dello strumento, usare `nuget help`.

**Che cos'è la licenza per nuget.exe?**

È possibile ridistribuire nuget.exe ai sensi della licenza MIT. L'utente è responsabile dell'aggiornamento e della manutenzione di qualsiasi copia di nuget.exe che si sceglie di ridistribuire.

**È possibile estendere lo strumento da riga di comando di NuGet?**

Sì, è possibile aggiungere comandi personalizzati a `nuget.exe`, come descritto nel [post di Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Console di Gestione pacchetti Nuget (Visual Studio in Windows)

**Qual è la procedura per ottenere l'accesso all'oggetto DTE nella console di Gestione pacchetti**

L'oggetto di primo livello nel modello a oggetti di automazione di Visual Studio viene chiamato oggetto DTE (Development Tools Environment). La console rende disponibile questo oggetto tramite una variabile denominata `$DTE`. Per altre informazioni, vedere [Cenni preliminari sul modello di automazione](/visualstudio/extensibility/internals/automation-model-overview) nella documentazione sull'estendibilità di Visual Studio.

**Si tenta di eseguire il cast della variabile $DTE al tipo DTE2, ma viene ricevuto un errore: Impossibile convertire il valore "EnvDTE. DTEClass" di tipo "EnvDTE. DTEClass" nel tipo "EnvDTE80. DTE2". Cosa c'è che non va?**

Si tratta di un problema noto correlato alla modalità di interazione di PowerShell con un oggetto COM. Attenersi alla procedura seguente:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` è una funzione helper aggiunta dall'host di PowerShell di NuGet.

## <a name="creating-and-publishing-packages"></a>Creazione e pubblicazione di pacchetti

**Qual è la procedura per presentare un pacchetto in un feed?**

Vedere [Creare e pubblicare un pacchetto](../quickstart/create-and-publish-a-package-using-visual-studio.md).

**Sono disponibili più versioni della libreria destinate a versioni diverse della .NET Framework. Ricerca per categorie compilare un singolo pacchetto che supporta questa operazione?**

Vedere [Supporto di più versioni di .NET Framework](../create-packages/supporting-multiple-target-frameworks.md).

**Qual è la procedura per configurare un repository o un feed personale?**

Vedere la [panoramica dell'hosting dei pacchetti](../hosting-packages/overview.md).

**Qual è la procedura per caricare i pacchetti per il feed di NuGet in blocco?**

Vedere [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (Pubblicazione in blocco di pacchetti NuGet) (jeffhandly.com).

## <a name="working-with-packages"></a>Utilizzo dei pacchetti

**È possibile installare i pacchetti NuGet senza connettività Internet?**

Sì, vedere il post di blog di Scott Hanselman [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Come accedere a NuGet quando il sito nuget.org non è disponibile oppure sei in aereo) (hanselman.com).

**Qual è la procedura per installare i pacchetti in un percorso diverso rispetto alla cartella packages predefinita?**

Impostare l' [`repositoryPath`](../reference/nuget-config-file.md#config-section) impostazione in `Nuget.Config` utilizzando `nuget config -set repositoryPath=<path>` .

**Come è possibile evitare di aggiungere la cartella dei pacchetti NuGet nel controllo del codice sorgente?**

Impostare [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` su `true` . Questa chiave funziona a livello di soluzione e quindi deve essere aggiunta al file `$(Solutiondir)\.nuget\Nuget.Config`. Quando si abilita il ripristino dei pacchetti da Visual Studio, questo file viene creato automaticamente.

**Qual è la procedura per disattivare il ripristino dei pacchetti?**

Vedere [Abilitazione e disabilitazione del ripristino dei pacchetti](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Perché viene visualizzato un errore "Non è possibile risolvere la dipendenza" durante l'installazione di un pacchetto locale con dipendenze remote?**

È necessario selezionare l'origine **Tutti** quando si installa un pacchetto locale nel progetto. In questo modo vengono aggregati tutti i feed anziché usarne solo uno. Il motivo per cui viene visualizzato questo errore è che gli utenti di un repository locale spesso vogliono evitare l'installazione accidentale di un pacchetto remoto a causa di criteri aziendali.

**Se sono disponibili più progetti nella stessa cartella, in che modo è possibile usare file packages.config separati per ogni progetto?**

Nella maggior parte dei progetti in cui progetti separati risiedono in cartelle separate, questo non costituisce un problema perché NuGet identifica i file `packages.config` in ogni progetto. Con NuGet 3.3 + e più progetti nella stessa cartella, è possibile inserire il nome del progetto nei nomi di file `packages.config` usando il modello `packages.{project-name}.config`, e NuGet usa tale file.

Questo non è un problema quando si usa PackageReference, perché ogni file di progetto contiene il proprio elenco di dipendenze.

**Se nuget.org non compare più nell'elenco dei repository, come è possibile ottenerlo di nuovo?**

- Aggiungere `https://api.nuget.org/v3/index.json` all'elenco di origini, o
- Eliminare `%appdata%\.nuget\NuGet.Config` (Windows) o `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) e consentire a NuGet di ricrearlo.

**È stata eseguita la migrazione a PackageReference, perché la compilazione ha esito negativo `This project references NuGet package(s) that are missing on this computer.` ?**

Nei progetti di packages.config, quando `build` è stato installato un pacchetto con Props o targets, NuGet aggiunge una `EnsureNuGetPackageBuildImports` destinazione per verificare che i pacchetti di contenuto MSBuild siano stati importati prima della compilazione.
Se `target` è stato modificato manualmente, NuGet potrebbe non essere in grado di rilevare che è necessario rimuovere durante la migrazione.

Se il progetto è `PackageReference` e la destinazione è ancora presente nel file di progetto, è consigliabile rimuoverla.
