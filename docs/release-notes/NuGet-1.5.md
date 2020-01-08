---
title: Note sulla versione di NuGet 1,5
description: Note sulla versione per NuGet 1,5, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383349"
---
# <a name="nuget-15-release-notes"></a>Note sulla versione di NuGet 1,5

[Note sulla versione di nuget 1,4](../release-notes/nuget-1.4.md) | [Note sulla versione di NuGet 1,6](../release-notes/nuget-1.6.md)

NuGet 1,5 è stato rilasciato il 30 agosto 2011.

## <a name="features"></a>Funzionalità

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modelli di progetto con pacchetti NuGet preinstallati
Quando si crea un nuovo modello di progetto ASP.NET MVC 3, le librerie di script jQuery incluse nel progetto vengono effettivamente posizionate installando i pacchetti NuGet.

Il modello di progetto ASP.NET MVC 3 include un set di pacchetti NuGet che vengono installati quando viene richiamato il modello di progetto. Questa possibilità di includere i pacchetti NuGet con un modello di progetto è ora una funzionalità di NuGet che può ora essere sfruttata da _qualsiasi_ modello di progetto.

Per ulteriori informazioni su questa funzionalità, leggere questo [post di Blog dallo sviluppatore della funzionalità](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Riferimenti ad assembly espliciti

È stato aggiunto un nuovo elemento `<references />` usato per specificare in modo esplicito quali assembly all'interno del pacchetto deve essere fatto riferimento.

Ad esempio, se si aggiungono gli elementi seguenti:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Verrà quindi fatto riferimento solo alla `xunit.dll` e alla `xunit.extensions.dll` dalla [sottocartella del Framework/profilo](../reference/nuspec.md#explicit-assembly-references) appropriata della cartella `lib` anche se sono presenti altri assembly nella cartella.

Se questo elemento viene omesso, viene applicato il comportamento consueto, ovvero per fare riferimento a ogni assembly nella cartella `lib`.

__Per cosa si usa questa funzionalità?__

Questa funzionalità supporta solo assembly in fase di progettazione. Quando si usano contratti di codice, ad esempio, è necessario che gli assembly del contratto si trovino accanto agli assembly di runtime che aumentano, in modo che Visual Studio possa trovarli, ma gli assembly del contratto non devono essere effettivamente usati come riferimento dal progetto e non devono essere copiati nella cartella `bin`.

Analogamente, la funzionalità può essere usata per unit test Framework, ad esempio XUnit, che richiedono la posizione degli assembly degli strumenti accanto agli assembly di runtime, esclusi i riferimenti ai progetti.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Aggiunta della possibilità di escludere i file nel file con estensione NuSpec
L'elemento `<file>` all'interno di un file di `.nuspec` può essere utilizzato per includere un file specifico o un set di file utilizzando un carattere jolly. Quando si usa un carattere jolly, non è possibile escludere un subset specifico dei file inclusi. Si supponga, ad esempio, di volere tutti i file di testo all'interno di una cartella tranne uno specifico.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Usare i punti e virgola per specificare più file.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

In alternativa, usare un carattere jolly per escludere un set di file, ad esempio tutti i file di backup

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Rimozione di pacchetti utilizzando la finestra di dialogo richiesta per rimuovere le dipendenze
Quando si disinstalla un pacchetto con dipendenze, NuGet richiede, consentendo la rimozione delle dipendenze di un pacchetto insieme al pacchetto.

![Rimozione di pacchetti dipendenti](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>miglioramento del comando `Get-Package`
Il `Get-Package` comando supporta ora un parametro di `-ProjectName`. Quindi, il comando

    Get-Package –ProjectName A

Elenca tutti i pacchetti installati nel progetto A.

### <a name="support-for-proxies-that-require-authentication"></a>Supporto per proxy che richiedono l'autenticazione
Quando si usa NuGet dietro un proxy che richiede l'autenticazione, NuGet ora richiede le credenziali proxy. L'immissione di credenziali consente a NuGet di connettersi al repository remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Supporto per repository che richiedono l'autenticazione
NuGet supporta ora la connessione a [repository privati](../hosting-packages/local-feeds.md) che richiedono l'autenticazione di base o NTLM.

Il supporto per l'autenticazione del digest verrà aggiunto in una versione futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Miglioramenti delle prestazioni per il repository nuget.org
Sono stati apportati diversi miglioramenti alle prestazioni della raccolta nuget.org per rendere più veloce l'elenco e la ricerca di pacchetti.

### <a name="solution-dialog-project-filtering"></a>Filtro progetto finestra di dialogo soluzione
Nella finestra di dialogo a livello di soluzione, quando viene richiesto di specificare i progetti da installare, vengono visualizzati solo i progetti compatibili con il pacchetto selezionato.

### <a name="package-release-notes"></a>Note sulla versione del pacchetto
I pacchetti NuGet ora includono il supporto per le note sulla versione. Le note sulla versione vengono visualizzate solo quando si visualizzano _gli aggiornamenti_ per un pacchetto, pertanto non è opportuno aggiungerle alla prima versione.

![Note sulla versione nella scheda aggiornamenti](./media/manage-nuget-packages-release-notes.png)

Per aggiungere note sulla versione a un pacchetto, usare il nuovo elemento dei metadati `<releaseNotes />` nel file NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>. NuSpec & ltfiles/&gt; Improvement
Il file `.nuspec` ora consente l'elemento `<files />` vuoto, che indica a NuGet. exe di non includere alcun file nel pacchetto.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1,5 aveva un totale di 107 elementi di lavoro corretti. 103 di questi sono stati contrassegnati come bug.

Per un elenco completo degli elementi di lavoro corretti in NuGet 1,5, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug degni di Nota:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` reso più intuitivo il controllo della versione, ordinando i pacchetti alfabeticamente e rimuovendo gli spazi vuoti aggiuntivi.
* [Problema 844](http://nuget.codeplex.com/workitem/844): i numeri di versione vengono ora normalizzati in modo che `Install-Package 1.0` funzioni in un pacchetto con la versione `1.0.0`.
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): quando si crea un pacchetto con NuGet. exe, il flag di `-Version` esegue l'override dell'elemento `<version />`.
