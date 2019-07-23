---
title: Note sulla versione di NuGet 1,4
description: Note sulla versione per NuGet 1,4, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de76cf610e580a36014be9274b9c2c762b1015ac
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317169"
---
# <a name="nuget-14-release-notes"></a>Note sulla versione di NuGet 1,4

[Note sulla versione di NuGet 1,3-](../release-notes/nuget-1.3.md) | [Note sulla versione di NuGet 1,5](../release-notes/nuget-1.5.md)

NuGet 1,4 è stato rilasciato il 17 giugno 2011.

## <a name="features"></a>Funzionalità

### <a name="update-package-improvements"></a>Miglioramenti di Update-Package
In NuGet 1,4 sono stati introdotti numerosi miglioramenti al comando Update-Package che semplificano la conservazione dei pacchetti con la stessa versione tra più progetti in una soluzione. Ad esempio, quando si aggiorna un pacchetto alla versione più recente, è molto comune che tutti i progetti con il pacchetto installato vengano aggiornati allo stesso Verision.

Il `Update-Package` comando ora rende più semplice:

#### <a name="update-all-packages-in-a-single-project"></a>Aggiornare tutti i pacchetti in un singolo progetto

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aggiornare un pacchetto in tutti i progetti

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aggiorna tutti i pacchetti in tutti i progetti

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Eseguire un aggiornamento "sicuro" su tutti i pacchetti
Il `-Safe` flag vincola gli aggiornamenti solo alle versioni con lo stesso componente della versione principale e secondaria. Se, ad esempio, è installata la versione 1.0.0 di un pacchetto e nel feed sono disponibili le versioni 1.0.1, 1.0.2 e 1,1, il `-Safe` flag aggiorna il pacchetto alla versione 1.0.2. Se si esegue `-Safe` l'aggiornamento senza il flag, il pacchetto verrà aggiornato alla versione più recente 1,1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>Gestione dei pacchetti a livello di soluzione
Prima di NuGet 1,4, l'installazione di un pacchetto in più progetti è stata complessa usando la finestra di dialogo. È necessario avviare la finestra di dialogo una volta per ogni progetto.

NuGet 1,4 aggiunge il supporto per l'installazione/disinstallazione o l'aggiornamento di pacchetti in più progetti contemporaneamente. È sufficiente avviare il facendo clic con il pulsante destro del mouse sulla soluzione e selezionando l'opzione di menu **Gestisci pacchetti NuGet** .

![Finestra di dialogo Gestisci pacchetti NuGet di livello soluzione](./media/manage-nuget-packages-solution-dialog.png)

Si noti che nella barra del titolo della finestra di dialogo viene visualizzato il nome della soluzione, non il nome di un progetto.
Le operazioni sui pacchetti forniscono ora un elenco di caselle di controllo con l'elenco dei progetti a cui deve essere applicata l'operazione.

![Gestisci selezione progetto pacchetti NuGet](./media/manage-nuget-packages-project-selection.png)

Per ulteriori informazioni, vedere l'argomento relativo alla [gestione dei pacchetti per la soluzione](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Limitazione degli aggiornamenti alle versioni consentite
Per impostazione predefinita, quando si `Update-Package` esegue il comando in un pacchetto (o si aggiorna il pacchetto utilizzando la finestra di dialogo), questo verrà aggiornato alla versione più recente nel feed. Con il nuovo supporto per l'aggiornamento di tutti i pacchetti, in alcuni casi è possibile che si desideri bloccare un pacchetto in un intervallo di versioni specifico. Ad esempio, è possibile che si sappia che l'applicazione funzionerà solo con la versione 2. * di un pacchetto, ma non con 3,0 e versioni successive. Per evitare l'aggiornamento accidentale del pacchetto a 3, NuGet 1,4 aggiunge il supporto per limitare l'intervallo di versioni in cui i pacchetti possono essere aggiornati manualmente modificando il `packages.config` file usando il nuovo `allowedVersions` attributo.

Ad esempio, nell'esempio seguente viene illustrato come bloccare il `SomePackage` pacchetto con intervallo di versione 2,0-3,0 (esclusivo).
L' `allowedVersions` attributo accetta valori usando il [formato dell'intervallo di versioni](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Si noti che in 1,4, il blocco di un pacchetto in un intervallo di versioni specifico deve essere modificato manualmente. In NuGet 1,5 si prevede di aggiungere il supporto per l'inserimento di questo `Install-Package` intervallo tramite il comando.

### <a name="package-visualizer"></a>Visualizzatore pacchetti
Il nuovo Visualizzatore di pacchetti, avviato tramite l'opzione**di menu** **strumenti** -> **libreria pacchetti di gestione** -> pacchetti, consente di visualizzare facilmente tutti i progetti e le dipendenze dei pacchetti all'interno di un soluzione.

_**Nota importante:** Questa funzionalità sfrutta i vantaggi del supporto di DGML in Visual Studio. La creazione della visualizzazione è supportata solo in Visual Studio Ultimate. La visualizzazione di un diagramma DGML è supportata solo in Visual Studio Premium o versione successiva._

![Visualizzatore pacchetti](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Controllo automatico degli aggiornamenti per la finestra di dialogo NuGet
Alcune versioni di NuGet introducono nuove funzionalità espresse tramite `.nuspec` il file che non sono riconosciute dalle versioni precedenti della finestra di dialogo NuGet.
Un esempio è l'introduzione in NuGet 1,4 per [specificare gli assembly del Framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Per questo motivo, è importante usare la versione più recente di NuGet per assicurarsi che sia possibile usare i pacchetti sfruttando le funzionalità più recenti.
Per rendere più visibili gli aggiornamenti a NuGet, la finestra di dialogo NuGet contiene la logica da evidenziare quando è disponibile una versione più recente.

_**Nota**: Il controllo viene eseguito solo se la scheda **online** è stata selezionata nella sessione corrente._

![Finestra di dialogo Gestisci pacchetti NuGet con la nuova versione disponibile](./media/manage-nuget-packages-update-notification.png)

Per disattivare la verifica automatica degli aggiornamenti, passare alla finestra di dialogo Impostazioni NuGet e deselezionare **Controlla automaticamente la disponibilità di aggiornamenti**.

![Impostazioni NuGet](./media/nuget-settings.png)

Questa funzionalità è stata effettivamente aggiunta in NuGet 1,3, ma non è naturalmente visibile fino a quando non viene reso disponibile un aggiornamento a 1,3, ad esempio NuGet 1,4.

### <a name="package-manager-dialog-improvements"></a>Miglioramenti della finestra di dialogo Gestione pacchetti
* **Nomi di menu migliorati**: Le opzioni di menu per avviare la finestra di dialogo sono state rinominate per maggiore chiarezza. L'opzione di menu ora **gestisce i pacchetti NuGet**.
* **Riquadro dei dettagli Mostra la data di aggiornamento più recente**: La finestra di dialogo NuGet Visualizza la data dell'ultimo aggiornamento nel riquadro dei dettagli per un pacchetto quando è selezionata la scheda **online** o **aggiornamenti** .
* **Elenco di tag visualizzati**: Nella finestra di dialogo NuGet vengono visualizzati i tag.

### <a name="powershell-improvements"></a>Miglioramenti di PowerShell
* **Script di PowerShell firmati**: NuGet include script di PowerShell firmati che consentono l'utilizzo in ambienti più restrittivi.
* **Richiesta di supporto**: La console di gestione pacchetti supporta ora la richiesta tramite `$host.ui.Prompt` i `$host.ui.PromptForChoice` comandi e.
* **Nomi di origine del pacchetto**: Specificare il nome di un'origine del pacchetto è supportato quando si specifica un'origine del pacchetto `-Source` usando il flag.

### <a name="nugetexe-command-line-improvements"></a>miglioramenti della riga di comando di NuGet. exe
* **Comandi personalizzati NuGet**: NuGet. exe è estendibile tramite comandi personalizzati che usano MEF.
* **Più semplice è il flusso di lavoro per la creazione di pacchetti di simboli**: Il `-Symbols` flag può essere applicato a una normale struttura di cartelle basata sulla convenzione creazione di un pacchetto di simboli includendo `.pdb` solo l'origine e i file all'interno della cartella.
* **Specifica di più origini**: Il `NuGet install` comando supporta la specifica di più origini usando i punti e virgola come delimitatore o `-Source` specificando più volte.
* **Supporto per l'autenticazione proxy**: NuGet 1,4 aggiunge il supporto per la richiesta di credenziali utente quando si usa NuGet dietro un proxy che richiede l'autenticazione.
* **modifica di rilievo dell'aggiornamento di NuGet. exe**: Il `-Self` flag è ora necessario per l'aggiornamento di NuGet. exe. `nuget.exe Update`ora accetta un percorso del file e `packages.config` tenterà di aggiornare i pacchetti. Si noti che questo aggiornamento è limitato in quanto non sarà: * * aggiornare, aggiungere e rimuovere contenuto nel file di progetto.
\* * Eseguire script di PowerShell all'interno del pacchetto.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Supporto del server NuGet per il push di pacchetti con NuGet. exe
NuGet include un modo semplice per ospitare un [repository NuGet leggero basato su Web](../hosting-packages/nuget-server.md) tramite `NuGet.Server` il pacchetto NuGet. Con NuGet 1,4, il server Lightweight supporta il push e l'eliminazione di pacchetti con NuGet. exe.
La versione più recente `NuGet.Server` di aggiunge un `appSetting`nuovo oggetto `apiKey`denominato. Quando la chiave viene omessa o lascia vuota, il push dei pacchetti nel feed è disabilitato. L'impostazione di apiKey su un valore (idealmente una password complessa) consente di eseguire il push dei pacchetti con NuGet. exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Supporto per Windows Phone Tools Mango Edition
NuGet è ora supportato nella versione finale candidata di Windows Phone Tools per mango.
Attualmente, Windows Phone strumenti non dispone del supporto per Gestione estensioni di Visual Studio, pertanto per installare NuGet per gli strumenti di Windows Phone, potrebbe essere necessario scaricare ed eseguire il progetto VSIX manualmente.

Per disinstallare NuGet per gli strumenti di Windows Phone, eseguire il comando seguente.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1,4 aveva un totale di 88 elementi di lavoro corretti. 71 di questi sono stati contrassegnati come bug.

Per un elenco completo degli elementi di lavoro corretti in NuGet 1,4, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug degni di Nota:

* [Problema 603](http://nuget.codeplex.com/workitem/603): Le dipendenze dei pacchetti tra repository diversi vengono risolte correttamente quando si specifica un'origine del pacchetto specifica.
* [Problema 1036](http://nuget.codeplex.com/workitem/1036): L' `NuGet Pack SomeProject.csproj` aggiunta a un evento di post-compilazione non causa più un ciclo infinito.
* [Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` il flag supporta percorsi relativi.

## <a name="nuget-14-update"></a>Aggiornamento di NuGet 1,4
Poco dopo il rilascio di NuGet 1,4, sono stati rilevati alcuni problemi importanti da risolvere.
Il numero di versione specifico di questo aggiornamento 1,4 è 1.4.20615.9020.

### <a name="bug-fixes"></a>Correzioni di bug
* [Problema 1220](http://nuget.codeplex.com/workitem/1220): Update-Package non viene `install.ps1` eseguito / `uninstall.ps1` in tutti i progetti quando è presente più di un progetto
* [Problema 1156](http://nuget.codeplex.com/workitem/1156): Console di gestione pacchetti bloccata su W2K3/XP (se PowerShell 2 non è installato)
