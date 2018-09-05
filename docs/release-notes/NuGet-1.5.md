---
title: Note sulla versione 1.5 di NuGet
description: Note sulla versione per NuGet 1.5 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548725"
---
# <a name="nuget-15-release-notes"></a>Note sulla versione 1.5 di NuGet

[Note sulla versione di NuGet 1.4](../release-notes/nuget-1.4.md) | [note sulla versione di NuGet 1.6](../release-notes/nuget-1.6.md)

NuGet 1.5 è stato rilasciato il 30 agosto 2011.

## <a name="features"></a>Funzionalità

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Modelli di progetto con i pacchetti NuGet preinstallati
Quando si crea un nuovo modello di progetto ASP.NET MVC 3, le librerie di script jQuery è incluse nel progetto vengono effettivamente inserite da installazione di pacchetti NuGet.

Il modello di progetto ASP.NET MVC 3 include un set di pacchetti NuGet che vengono installati quando viene richiamato il modello di progetto. La possibilità di includere i pacchetti NuGet con un modello di progetto è ora una funzionalità di NuGet che _qualsiasi_ modello di progetto possa ora sfruttare.

Per altre informazioni su questa funzionalità, leggi questo [post di blog dallo sviluppatore della funzionalità](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Riferimenti espliciti agli Assembly

Aggiunto un nuovo `<references />` elemento usato per specificare in modo esplicito gli assembly all'interno del pacchetto deve essere fatto riferimento.

Ad esempio, se si aggiungere il codice seguente:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Quindi solo le `xunit.dll` e `xunit.extensions.dll` verrà fatto riferimento da appropriato [sottocartella/profilo del framework](../reference/nuspec.md#explicit-assembly-references) del `lib` cartella anche se sono presenti altri assembly nella cartella.

Se questo elemento viene omesso, quindi si applica al normale funzionamento, che consiste nel fare riferimento a tutti gli assembly nel `lib` cartella.

__Cosa serve per questa funzionalità?__

Questa funzionalità supporta gli assembly soli in fase di progettazione. Ad esempio, quando si utilizzano contratti di codice, gli assembly del contratto devono essere in prossimità degli assembly di runtime che essi aumentano in modo che Visual Studio possa trovarli, ma gli assembly di contratto non devono effettivamente essere fatto riferimento dal progetto e non devono essere copiati nella il `bin` cartella.

Analogamente, la funzionalità è utilizzabile per Framework di unit test, come XUnit che necessitano di relativi assembly di strumenti che si trova accanto agli assembly di runtime, ma escluso da riferimenti del progetto.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Aggiunta di funzionalità per escludere i file nei file con estensione nuspec
Il `<file>` elemento all'interno di un `.nuspec` file può essere utilizzato per includere un file specifico o un set di file usando un carattere jolly. Quando si usa un carattere jolly, non è possibile escludere un subset specifico di file inclusi. Ad esempio, si supponga di che voler tutti i file di testo all'interno di una cartella, ad eccezione di uno specifico.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Usare un punto e virgola per specificare più file.

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

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Rimozione di pacchetti tramite la finestra di dialogo chiede se si desidera per rimuovere le dipendenze
Quando si disinstalla un pacchetto con dipendenze, NuGet richiede, consentendo la rimozione delle dipendenze del pacchetto insieme al pacchetto.

![Rimozione di pacchetti dipendenti](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` miglioramento di comando
Il `Get-Package` comando supporta ora un `-ProjectName` parametro. Pertanto, il comando

    Get-Package –ProjectName A

Elenca tutti i pacchetti installati nel progetto r.

### <a name="support-for-proxies-that-require-authentication"></a>Supporto per i proxy che richiedono l'autenticazione
Quando si usa NuGet dietro un proxy che richiede l'autenticazione, NuGet ora richiederà di credenziali del proxy. Immissione delle credenziali consente a NuGet per la connessione al repository remoto.

### <a name="support-for-repositories-that-require-authentication"></a>Supporto per i repository che richiede l'autenticazione
NuGet supporta ora la connessione a [repository privati](../hosting-packages/local-feeds.md) che richiedono l'autenticazione di base o NTLM.

Verrà aggiunto il supporto per l'autenticazione del Digest in una versione futura.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Miglioramenti delle prestazioni per il repository nuget.org
Sono stati apportati diversi miglioramenti delle prestazioni per la raccolta nuget.org per rendere pacchetto listato e la ricerca più velocemente.

### <a name="solution-dialog-project-filtering"></a>Progetto di soluzione finestra di dialogo Filtro
Nella finestra di livello di soluzione, quando vengono richieste per i quali progetti per l'installazione, viene illustrato solo i progetti che sono compatibili con il pacchetto selezionato.

### <a name="package-release-notes"></a>Note sulla versione del pacchetto
I pacchetti NuGet includono ora il supporto per le note sulla versione. Le note sulla versione Mostra solo backup quando si visualizzano _aggiornamenti_ per un pacchetto, pertanto non ha senso per aggiungerli al primo rilascio.

![Note sulla versione all'interno della scheda degli aggiornamenti](./media/manage-nuget-packages-release-notes.png)

Per aggiungere note sulla versione per un pacchetto, usare il nuovo `<releaseNotes />` elemento dei metadati nel file NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>file con estensione nuspec & ltfiles /&gt; analisi utilizzo software
Il `.nuspec` file consente ora vuota `<files />` elemento, che indica a nuget.exe di non includere tutti i file nel pacchetto.

## <a name="bug-fixes"></a>Correzioni di bug
1.5 NuGet ha un totale di 107 fisso di elementi di lavoro. 103 di questi sono stati contrassegnati come bug.

Per un elenco completo di lavoro gli elementi corretti in 1.5, NuGet, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug la pena notare:

* [Problema 1273](http://nuget.codeplex.com/workitem/1273): apportate `packages.config` controllo della versione più descrittivo ordinando alfabeticamente i pacchetti e la rimozione di uno spazio vuoto aggiuntivo.
* [Problema 844](http://nuget.codeplex.com/workitem/844): i numeri di versione ora vengono normalizzati in modo che `Install-Package 1.0` funziona in un pacchetto con la versione `1.0.0`.
* [Problema 1060](http://nuget.codeplex.com/workitem/1060): quando si crea un pacchetto utilizzando nuget.exe, il `-Version` flag sostituzioni di `<version />` elemento.
