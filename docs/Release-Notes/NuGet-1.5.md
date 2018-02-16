---
title: Note sulla versione 1.5 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Note sulla versione per NuGet 1.5 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti."
keywords: "1.5 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9f93000cd5e86cb8f3798e32daf6a4ded0d4e9c3
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-15-release-notes"></a>Note sulla versione 1.5 di NuGet

[Note sulla versione 1.4 NuGet](../release-notes/nuget-1.4.md) | [note sulla versione 1.6 NuGet](../release-notes/nuget-1.6.md)

1.5 NuGet è stata rilasciata il 30 agosto 2011.

## <a name="features"></a>Funzionalità

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modelli di progetto con i pacchetti NuGet preinstallati
Quando si crea un nuovo modello di progetto ASP.NET MVC 3, le librerie di script jQuery è incluse nel progetto sono effettivamente memorizzate da installazione dei pacchetti NuGet.

Il modello di progetto ASP.NET MVC 3 include un set di pacchetti NuGet a cui viene installato quando viene richiamato il modello di progetto. La possibilità di includere i pacchetti NuGet con un modello di progetto è ora una funzionalità di NuGet che _qualsiasi_ modello di progetto può ora sfruttare.

Per ulteriori informazioni su questa funzionalità, leggere questo [post di blog di sviluppo della funzionalità](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Riferimenti agli Assembly esplicita

Aggiunta di un nuovo `<references />` elemento utilizzato per specificare in modo esplicito gli assembly all'interno del pacchetto deve essere fatto riferimento.

Ad esempio, se si aggiungono le operazioni seguenti:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Quindi solo il `xunit.dll` e `xunit.extensions.dll` verrà fatto riferimento da appropriata [sottocartella/profilo del framework](../reference/nuspec.md#explicit-assembly-references) del `lib` cartella anche se sono presenti altri assembly nella cartella.

Se questo elemento viene omesso, si applica al normale funzionamento, ovvero per fare riferimento a tutti gli assembly nel `lib` cartella.

__Per ciò che viene utilizzata questa funzionalità?__

Questa funzionalità supporta solo ad assembly in fase di progettazione. Ad esempio, quando si utilizzano contratti di codice, i contratto gli assembly devono essere accanto agli assembly di runtime che essi aumentano in modo che Visual Studio è possibile trovarli, ma gli assembly di contratto non devono effettivamente essere fatto riferimento dal progetto e non devono essere copiati nella il `bin` cartella.

Analogamente, la funzionalità utilizzabile per il framework di unit test, ad esempio XUnit che richiedono i relativi assembly strumenti si trova accanto agli assembly di runtime, ma escluso da riferimenti al progetto.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Aggiunta la capacità di escludere i file del. nuspec
Il `<file>` elemento all'interno di un `.nuspec` file può essere utilizzato per includere un file specifico o un set di file mediante un carattere jolly. Quando si utilizza un carattere jolly, non è possibile escludere un sottoinsieme specifico di file inclusi. Si supponga, ad esempio, che si desidera che tutti i file di testo all'interno di una cartella, ad eccezione di uno specifico.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Utilizzare un punto e virgola per specificare più file.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Oppure usare un carattere jolly per escludere un set di file, ad esempio tutti i file di backup

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Rimozione dei pacchetti tramite la finestra di dialogo viene chiesto di rimuovere le dipendenze
Quando si disinstalla un pacchetto con dipendenze, NuGet richiesto, consentendo la rimozione delle dipendenze di un pacchetto insieme al pacchetto.

![Rimozione dei pacchetti dipendenti](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` miglioramento di comando
Il `Get-Package` comando supporta ora un `-ProjectName` parametro. Pertanto, il comando

    Get-Package –ProjectName A

verranno elencati tutti i pacchetti installati nel progetto A.

### <a name="support-for-proxies-that-require-authentication"></a>Supporto per i proxy che richiede l'autenticazione
Quando si usa NuGet dietro un proxy che richiede l'autenticazione, NuGet verrà ora richiesto per le credenziali del proxy. Immissione delle credenziali consente NuGet per la connessione al repository remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Supporto per i repository che richiede l'autenticazione
NuGet supporta ora la connessione a [repository privati](../hosting-packages/local-feeds.md) che richiedono l'autenticazione di base o NTLM.

Verrà aggiunto il supporto per l'autenticazione del Digest in una versione futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Miglioramenti delle prestazioni per il repository nuget.org
Sono stati apportati diversi miglioramenti delle prestazioni per la raccolta di nuget.org per rendere pacchetto elenco e la ricerca veloce.

### <a name="solution-dialog-project-filtering"></a>Progetto di soluzione finestra di dialogo Filtro
Nella finestra di dialogo, a livello di soluzione quando viene richiesto per i progetti per l'installazione, vengono dimostrati solo i progetti che sono compatibili con il pacchetto selezionato.

### <a name="package-release-notes"></a>Note sulla versione del pacchetto
Pacchetti NuGet includono ora il supporto per le note sulla versione. Le note sulla versione Mostra solo backup quando si visualizzano _aggiornamenti_ per un pacchetto, in modo non ha senso per aggiungerli al primo rilascio.

![Note sulla versione all'interno della scheda di aggiornamenti](./media/manage-nuget-packages-release-notes.png)

Per aggiungere note sulla versione a un pacchetto, usare il nuovo `<releaseNotes />` elemento dei metadati nel file NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>. nuspec & ltfiles /&gt; analisi utilizzo software
Il `.nuspec` file consente ora vuota `<files />` elemento, che indica a nuget.exe non includere tutti i file nel pacchetto.

## <a name="bug-fixes"></a>Correzioni di bug
1.5 NuGet era un totale di 107 fissati di elementi di lavoro. 103 di quelli contrassegnati come bug.

Per un elenco completo di lavoro gli elementi corretti in NuGet 1.5,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug non degni di nota:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): apportate `packages.config` controllo della versione più descrittivo per l'ordinamento in ordine alfabetico i pacchetti e la rimozione di uno spazio vuoto aggiuntivo.
* [Problema 844](http://nuget.codeplex.com/workitem/844): i numeri di versione ora vengono normalizzati in modo che `Install-Package 1.0` funziona su un pacchetto con la versione `1.0.0`.
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): durante la creazione di un pacchetto utilizzando nuget.exe, il `-Version` flag esegue l'override di `<version />` elemento.
