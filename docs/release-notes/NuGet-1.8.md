---
title: Note sulla versione di NuGet 1,8
description: Note sulla versione per NuGet 1,8, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8dd0fff88424c516d8b894412d07dcc53af19265
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777101"
---
# <a name="nuget-18-release-notes"></a>Note sulla versione di NuGet 1,8

Note sulla versione di [NuGet 1,7](../release-notes/nuget-1.7.md)  |  [Note sulla versione di NuGet 2,0](../release-notes/nuget-2.0.md)

NuGet 1,8 è stato rilasciato il 23 maggio 2012.

## <a name="known-installation-issue"></a>Problema di installazione noto
Se si esegue VS 2010 SP1, potrebbe essere rilevato un errore di installazione quando si tenta di aggiornare NuGet se è installata una versione precedente.

La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Vedere <https://support.microsoft.com/kb/2581019> per altre informazioni oppure [passare direttamente all'hotfix di Visual](http://bit.ly/vsixcertfix)Studio.

Nota: se Visual Studio non consente di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), probabilmente è necessario riavviare Visual Studio usando "Esegui come amministratore".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1,8 incompatibile con Windows XP, hotfix pubblicato

Poco dopo il rilascio di NuGet 1,8, si è appreso che un cambiamento di crittografia in 1,8 ha interrotto gli utenti in Windows XP.

Poiché è stato rilasciato un hotfix che risolve questo problema.  Con l'aggiornamento di NuGet tramite la raccolta di estensioni di Visual Studio, viene visualizzato questo hotfix.

## <a name="features"></a>Funzionalità

### <a name="satellite-packages-for-localized-resources"></a>Pacchetti satellite per le risorse localizzate
NuGet 1,8 supporta ora la possibilità di creare pacchetti distinti per le risorse localizzate, in modo analogo alle funzionalità di assembly satellite del .NET Framework.  Un pacchetto satellite viene creato allo stesso modo di qualsiasi altro pacchetto NuGet con l'aggiunta di alcune convenzioni:

* L'ID e il nome file del pacchetto satellite devono includere un suffisso che corrisponde a una delle [stringhe di impostazioni cultura standard utilizzate dal .NET Framework](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).
* Nel `.nuspec` file, il pacchetto satellite deve definire un elemento del linguaggio con la stessa stringa di impostazioni cultura usata nell'ID
* Il pacchetto satellite deve definire una dipendenza nel relativo `.nuspec` file al relativo pacchetto principale, che è semplicemente il pacchetto con lo stesso ID meno il suffisso della lingua.  Per eseguire correttamente l'installazione, il pacchetto di base deve essere disponibile nel repository.

Per installare un pacchetto con risorse localizzate, uno sviluppatore seleziona in modo esplicito il pacchetto localizzato dal repository. Attualmente, la raccolta NuGet non fornisce alcun tipo di trattamento speciale per i pacchetti satellite.

![Finestra di dialogo Gestione pacchetti con pacakges localizzato](./media/dlg-w-loc-packs.png)

Poiché il pacchetto satellite elenca una dipendenza per il pacchetto principale, i pacchetti satellite e core vengono estratti nella cartella pacchetti NuGet e installati.

![Cartella pacchetti con pacchetti localizzati](./media/fldr-loc-packs.png)

Inoltre, durante l'installazione del pacchetto satellite, NuGet riconosce anche la convenzione di denominazione delle stringhe di impostazioni cultura e quindi copia l'assembly di risorse localizzato nella sottocartella corretta all'interno del pacchetto principale, in modo che possa essere selezionato dal .NET Framework.

![Cartella del pacchetto principale con cartella delle risorse copiata](./media/fldr-copied-loc.png)

Un bug esistente da notare con i pacchetti satellite è che NuGet non copia le risorse localizzate nella `bin` cartella per i progetti di siti Web.  Questo problema verrà risolto nella prossima versione di NuGet.

Per un esempio completo che illustra come creare e usare pacchetti satellite, vedere [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) .

### <a name="package-restore-consent"></a>Consenso per il ripristino del pacchetto
In NuGet 1,8 abbiamo gettato le basi per supportare un vincolo importante nel ripristino dei pacchetti per proteggere la privacy degli utenti. Questo vincolo richiede agli sviluppatori di creare progetti e soluzioni che usano il ripristino dei pacchetti per acconsentire esplicitamente al ripristino del pacchetto in linea per scaricare i pacchetti dalle origini dei pacchetti configurate.

Sono disponibili 2 modi per fornire questo consenso. Il primo si trova nella finestra di dialogo di configurazione di gestione pacchetti, come illustrato di seguito.  Questo metodo è destinato principalmente ai computer di sviluppo.

![Finestra di dialogo di configurazione di gestione pacchetti](./media/pr-consent-configdlg.png)

Il secondo metodo consiste nell'impostare la variabile di ambiente "EnableNuGetPackageRestore" sul valore "true".  Questo metodo è destinato alle macchine automatiche, ad esempio CI o server di compilazione.

Ora, come indicato in precedenza, abbiamo solo gettato le basi per questa funzionalità in NuGet 1,8.  In pratica, ciò significa che, anche se è stata aggiunta tutta la logica per abilitare la funzionalità, attualmente non viene applicata in questa versione. Questa funzionalità verrà abilitata, tuttavia, nella prossima versione di NuGet, quindi è necessario renderla consapevole il prima possibile, in modo da poter configurare gli ambienti in modo appropriato e quindi non essere interessati quando si inizia a applicare il vincolo di consenso.

Per altri dettagli, vedere il [post di Blog del team](http://blog.nuget.org/20120518/package-restore-and-consent.html) su questa funzionalità.

### <a name="nugetexe-performance-improvements"></a>Miglioramenti delle prestazioni nuget.exe
Modificando il comando install per scaricare e installare i pacchetti in parallelo, NuGet 1,8 offre miglioramenti significativi delle prestazioni per nuget.exe e per il ripristino dei pacchetti di estensione.  Il testing di alto livello Mostra che le prestazioni per l'installazione di 6 pacchetti in un progetto migliorano di circa il 35% in NuGet 1,8.  L'aumento del numero di pacchetti a 25 Mostra un miglioramento delle prestazioni del 60%.

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1,8 include alcune correzioni di bug con particolare attenzione alla console di gestione pacchetti e al flusso di lavoro di ripristino dei pacchetti, in particolare per quanto riguarda il consenso per il ripristino dei pacchetti e l'integrazione con Windows 8 Express.
Per un elenco completo degli elementi di lavoro corretti in NuGet 1,8, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).