---
title: Note sulla versione 1.8 di NuGet
description: Note sulla versione per NuGet 1.8 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546621"
---
# <a name="nuget-18-release-notes"></a>Note sulla versione 1.8 di NuGet

[Note sulla versione di NuGet 1.7](../release-notes/nuget-1.7.md) | [note sulla versione di NuGet 2.0](../release-notes/nuget-2.0.md)

NuGet 1.8 è stato rilasciato il 23 maggio 2012.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

Per risolvere il problema è sufficiente disinstallare NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Visualizzare [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) per altre informazioni, o [passare direttamente all'hotfix di Visual Studio](http://bit.ly/vsixcertfix).

Nota: Se Visual Studio non consentirà di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), quindi probabile che sia necessario riavviare Visual Studio tramite "Esegui come amministratore".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 non compatibile con Windows XP, hotfix pubblicato

Poco dopo il rilascio di NuGet 1.8, abbiamo imparato che una modifica di crittografia in 1.8 annullino gli utenti in Windows XP.

Poiché Microsoft ha rilasciato un hotfix in grado di risolvere il problema.  Per l'aggiornamento di NuGet tramite la raccolta di estensioni di Visual Studio, si riceve questo hotfix.

## <a name="features"></a>Funzionalità

### <a name="satellite-packages-for-localized-resources"></a>Pacchetti satellite per le risorse localizzate
1.8 NuGet supporta ora la possibilità di creare pacchetti separati per le risorse localizzate, simili a quelle di assembly satellite di .NET Framework.  Viene creato un pacchetto satellite esattamente come qualsiasi altro pacchetto NuGet con l'aggiunta di alcune convenzioni:

* Il nome e ID del pacchetto satellite deve includere un suffisso che corrisponde a uno standard [sulle impostazioni cultura le stringhe utilizzate da .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* Nel relativo `.nuspec` file, il pacchetto satellite deve definire un elemento di linguaggio con la stessa stringa di impostazioni cultura utilizzata nell'ID
* Il pacchetto satellite deve definire una dipendenza nel relativo `.nuspec` file per il pacchetto principale, ovvero semplicemente il pacchetto con lo stesso ID meno il suffisso del linguaggio.  Pacchetto di base deve essere disponibile nel repository per l'installazione ha esito positivo.

Per installare un pacchetto con le risorse localizzate, lo sviluppatore seleziona in modo esplicito il pacchetto di aggiornamento dal repository. Al momento, raccolta NuGet non fornisce alcun tipo di trattamento speciale per i pacchetti satellite.

![Finestra di dialogo Gestione pacchetti con pacakges localizzato](./media/dlg-w-loc-packs.png)

Perché il pacchetto satellite elenca una dipendenza per il pacchetto di base, i pacchetti satellite sia il core sono estratti nella cartella dei pacchetti NuGet e installati.

![Cartella dei pacchetti con pacchetti localizzati](./media/fldr-loc-packs.png)

Inoltre, durante l'installazione del pacchetto satellite, NuGet riconosce inoltre la convenzione di denominazione stringa delle impostazioni cultura e quindi copia l'assembly di risorse localizzato nella sottocartella corretta all'interno del pacchetto di base in modo che possono essere selezionato da .NET Framework.

![Cartella del pacchetto principale con la cartella risorsa copiata](./media/fldr-copied-loc.png)

Un bug esistente con i pacchetti satellite notare è che NuGet non copia le risorse localizzate per le `bin` cartella per i progetti di sito Web.  Questo problema verrà risolto nella prossima versione di NuGet.

Per un esempio completo che illustra come creare e usare pacchetti satellite, vedere [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consenso di ripristino del pacchetto
In NuGet 1.8, abbiamo gettato le basi per il supporto di un vincolo importante sul ripristino dei pacchetti per proteggere la riservatezza degli utenti. Questo vincolo richiede gli sviluppatori che compilano i progetti e soluzioni che usano il ripristino dei pacchetti in modo esplicito il consenso al ripristino del pacchetto sarà online per scaricare i pacchetti da origini pacchetto configurato.

Esistono 2 modi per fornire il consenso. Il primo è reperibile nella finestra di configurazione di manager pacchetto come illustrato di seguito.  Questo metodo è destinato principalmente in computer di sviluppo.

![Finestra di dialogo Configurazione di package manager](./media/pr-consent-configdlg.png)

Il secondo metodo consiste nell'impostare l'ambiente di variabili "EnableNuGetPackageRestore" per il valore "true".  Questo metodo è destinato a automatica delle macchine, ad esempio server CI o compilazione.

A questo punto, come indicato in precedenza, abbiamo solo Stati gettato le basi per questa funzionalità in NuGet 1.8.  In pratica, ciò significa che anche se sono state aggiunte tutta la logica per abilitare la funzionalità, questa viene attualmente non imposta in questa versione. Verrà abilitata, tuttavia, entro i prossimi versione di NuGet, pertanto abbiamo deciso di rendere è consapevole appena possibile, in modo che è possibile configurare gli ambienti in modo appropriato e pertanto non essere interessate quando iniziamo a applicare il vincolo di consenso.

Per altre informazioni, vedere la [post di blog del team](http://blog.nuget.org/20120518/package-restore-and-consent.html) su questa funzionalità.

### <a name="nugetexe-performance-improvements"></a>Miglioramenti delle prestazioni NuGet.exe
Modificando il comando di installazione per scaricare e installare i pacchetti in parallelo, NuGet 1.8 sono stati introdotti miglioramenti notevolmente le prestazioni per nuget.exe – e per il ripristino di pacchetti di estensione.  Elevata a livello test Mostra un miglioramento delle prestazioni per l'installazione di 6 pacchetti in un progetto di circa il 35% in NuGet 1.8.  L'aumento del numero di pacchetti da 25 Mostra un miglioramento delle prestazioni di circa il 60%.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1.8 include alcune correzioni di bug con un'enfasi sulla console di gestione pacchetti e del flusso di lavoro di ripristino del pacchetto, soprattutto in relazione al consenso di ripristino di pacchetti e l'integrazione di Express per Windows 8.
Per un elenco completo di lavoro gli elementi corretti in NuGet 1.8, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
