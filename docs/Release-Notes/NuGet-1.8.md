---
title: Note sulla versione 1.8 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Note sulla versione per NuGet 1.8 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
keywords: 1.8 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: b94382f79143cac6bd5deccb5e5253ba8c6f60ec
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-18-release-notes"></a>Note sulla versione 1.8 di NuGet

[Note sulla versione 1.7 NuGet](../release-notes/nuget-1.7.md) | [note sulla versione di NuGet 2.0](../release-notes/nuget-2.0.md)

È stata rilasciata NuGet 1.8 23 maggio 2012.

## <a name="known-installation-issue"></a>Problema di installazione noti
Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Vedere [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) per altre informazioni, o [andare direttamente all'hotfix di Visual Studio](http://bit.ly/vsixcertfix).

Nota: Se Visual Studio non consente di disinstallare l'estensione (il pulsante di disinstallazione è disabilitato), quindi probabile che sia necessario riavviare Visual Studio utilizzando "Esegui come amministratore".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 compatibile con Windows XP, hotfix pubblicato

Subito dopo il rilascio di NuGet 1.8, abbiamo appreso che una modifica della crittografia in 1.8 annullino gli utenti in Windows XP.

Poiché è stato rilasciato un hotfix che risolve questo problema.  Aggiornando NuGet tramite la raccolta di estensioni di Visual Studio, si riceve questo aggiornamento rapido.

## <a name="features"></a>Funzionalità

### <a name="satellite-packages-for-localized-resources"></a>Pacchetti satellite per le risorse localizzate
1.8 NuGet supporta ora la possibilità di creare pacchetti separati per le risorse localizzate, simili a quelle di assembly satellite di .NET Framework.  Viene creato un pacchetto di satellite esattamente come qualsiasi altro pacchetto NuGet con l'aggiunta di alcune convenzioni:

* Il nome file e l'ID del pacchetto satellite deve includere un suffisso che corrisponde a uno degli standard [culture stringhe utilizzate da .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* Nel relativo `.nuspec` file, il pacchetto satellite deve definire un elemento di linguaggio con la stessa stringa di impostazioni cultura utilizzata nell'ID
* Il pacchetto satellite devono essere definiti da una dipendenza nel relativo `.nuspec` file relativo pacchetto di base, è semplicemente il pacchetto con lo stesso ID meno il suffisso di linguaggio.  Il pacchetto principale deve essere disponibile nel repository per il completamento dell'installazione.

Per installare un pacchetto con le risorse localizzate, uno sviluppatore seleziona in modo esplicito del pacchetto dal repository. Al momento, raccolta NuGet non fornisce alcun tipo di un trattamento speciale per i pacchetti satellite.

![Finestra di dialogo Gestione pacchetto con pacakges localizzata](./media/dlg-w-loc-packs.png)

Perché il pacchetto satellite elenca una dipendenza per il pacchetto di base, i pacchetti di base sia il satellite sono estratta nella cartella pacchetti NuGet e installati.

![Cartella di pacchetti con pacchetti localizzati](./media/fldr-loc-packs.png)

Inoltre, durante l'installazione del pacchetto satellite, NuGet riconosce inoltre la convenzione di denominazione di stringa delle impostazioni cultura e quindi copia l'assembly di risorse localizzato nella sottocartella corretta all'interno del pacchetto di base in modo che possono essere selezionato da .NET Framework.

![Cartella principale del pacchetto con cartella risorsa copiata](./media/fldr-copied-loc.png)

È di un bug esistente da tenere presente i pacchetti satellite che NuGet non copia le risorse localizzate per il `bin` cartella per i progetti di sito Web.  Questo problema verrà risolto nella versione successiva di NuGet.

Per un esempio completo che illustra come creare e utilizzare pacchetti satellite, vedere [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Consenso ripristino pacchetto
1.8 NuGet, cui è la base per il supporto di un vincolo importante sul ripristino del pacchetto per proteggere la riservatezza degli utenti. Questo vincolo viene richiesto sarà online per scaricare i pacchetti dalle origini pacchetto configurato gli sviluppatori che creano i progetti e soluzioni che utilizzano ripristino del pacchetto per il consenso esplicito per ripristino dei pacchetti.

Sono disponibili 2 modi per fornire il consenso. Il primo è reperibile nella finestra package manager configuration, come illustrato di seguito.  Questo metodo viene usata principalmente per computer di sviluppo.

![Finestra di dialogo Configurazione di package manager](./media/pr-consent-configdlg.png)

Il secondo metodo consiste nell'impostare l'ambiente di variabile "EnableNuGetPackageRestore" al valore "true".  Questo metodo è destinato a computer automatico, ad esempio i server di compilazione o di elemento di configurazione.

A questo punto, come descritto in precedenza, è stata solo di cui i presupposti per questa funzionalità NuGet 1.8.  In pratica, ciò significa che anche se sono stati aggiunti tutta la logica per abilitare la funzionalità, non è attualmente applicato in questa versione. Verrà abilitata, tuttavia, nella prossima versione di NuGet, pertanto si voleva informare l'utente ne appena possibile in modo che è possibile configurare gli ambienti in modo appropriato e pertanto non essere interessati quando si avvia il vincolo consenso.

Per ulteriori informazioni, vedere il [post di blog del team](http://blog.nuget.org/20120518/package-restore-and-consent.html) su questa funzionalità.

### <a name="nugetexe-performance-improvements"></a>Miglioramenti delle prestazioni di NuGet.exe
Modificando il comando di installazione per scaricare e installare i pacchetti in parallelo, NuGet 1.8 offre miglioramenti notevolmente le prestazioni di nuget.exe – e da un ripristino del pacchetto di estensione.  Test di livello elevato Mostra un miglioramento delle prestazioni per l'installazione di 6 pacchetti in un progetto del 35% circa in NuGet 1.8.  Aumentando il numero di pacchetti a 25 Mostra un miglioramento delle prestazioni di circa 60%.

## <a name="bug-fixes"></a>Correzioni di bug
1.8 NuGet include alcune correzioni di bug con un'enfasi sulla console di gestione di pacchetto e del flusso di lavoro di ripristino del pacchetto, in particolare per quanto riguarda il consenso di ripristino del pacchetto e integrazione Express per Windows 8.
Per un elenco completo di lavoro gli elementi corretti in NuGet 1.8,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
