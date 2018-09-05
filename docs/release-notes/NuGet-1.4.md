---
title: Note sulla versione 1.4 di NuGet
description: Note sulla versione per NuGet 1.4 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550631"
---
# <a name="nuget-14-release-notes"></a>Note sulla versione 1.4 di NuGet

[Note sulla versione di NuGet 1.3](../release-notes/nuget-1.3.md) | [note sulla versione di NuGet 1.5](../release-notes/nuget-1.5.md)

NuGet 1.4 è stato rilasciato il 17 giugno 2011.

## <a name="features"></a>Funzionalità

### <a name="update-package-improvements"></a>Miglioramenti di Update-Package
NuGet 1.4 introduce numerosi miglioramenti per il comando Update-Package, rendendo più semplice mantenere i pacchetti della stessa versione in più progetti in una soluzione. Ad esempio, quando si aggiorna un pacchetto alla versione più recente, è molto comune a tutti i progetti con tale pacchetto installato per essere aggiornati il verision stesso.

Il `Update-Package` comando a questo punto, è facile:

#### <a name="update-all-packages-in-a-single-project"></a>Aggiorna tutti i pacchetti in un unico progetto

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aggiornare un pacchetto in tutti i progetti

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aggiorna tutti i pacchetti in tutti i progetti

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Eseguire un aggiornamento "sicuro" per tutti i pacchetti
Il `-Safe` flag vincola gli aggiornamenti alle versioni di solo con lo stesso componente di versione principale e secondaria. Se è installata la versione 1.0.0 di un pacchetto e le versioni 1.0.1, 1.0.2 e 1.1 sono disponibili nel feed, ad esempio il `-Safe` flag aggiorna il pacchetto alla versione 1.0.2. L'aggiornamento senza il `-Safe` flag potrebbe aggiornare il pacchetto alla versione più recente, 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>La gestione dei pacchetti a livello di soluzione
Prima di NuGet 1.4, era complesso usando la finestra di dialogo installa un pacchetto in più progetti. È necessario avviare la finestra di dialogo una sola volta per ogni progetto.

NuGet 1.4 aggiunge il supporto per i pacchetti di installazione/disinstallazione/aggiornamento in più progetti contemporaneamente. Avviare semplicemente il pulsante destro del mouse facendo clic la soluzione e selezionando il **Gestisci pacchetti NuGet** l'opzione di menu.

![Finestra di dialogo Gestisci pacchetti NuGet di livello soluzione](./media/manage-nuget-packages-solution-dialog.png)

Si noti che nella barra del titolo della finestra di dialogo, viene visualizzato il nome della soluzione, non il nome di un progetto.
Operazioni sui pacchetti forniscono ora un elenco di caselle di controllo con l'elenco dei progetti che per applicare l'operazione.

![Gestire la selezione dei progetti i pacchetti NuGet](./media/manage-nuget-packages-project-selection.png)

Per altre informazioni, vedere l'argomento sul [gestione dei pacchetti per la soluzione](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Applicazione di un vincolo viene aggiornato a consentite versioni
Per impostazione predefinita, quando si esegue il `Update-Package` comando in un pacchetto o l'aggiornamento del pacchetto mediante finestra di dialogo, verrà aggiornato alla versione più recente nel feed. Con il nuovo supporto per l'aggiornamento di tutti i pacchetti, potrebbero esserci casi in cui si desidera bloccare un intervallo di versioni specifiche di un pacchetto. Ad esempio, si potrebbe sapere in anticipo che l'applicazione funziona solo con versione 2. * di un pacchetto, ma non 3.0 e versioni successive. Per evitare accidentalmente l'aggiornamento del pacchetto su 3, NuGet 1.4 aggiunge il supporto per vincolare l'intervallo di versioni che i pacchetti possono essere aggiornati a modificando manualmente il `packages.config` file usando il nuovo `allowedVersions` attributo.

Ad esempio, nell'esempio seguente viene illustrato come bloccare i `SomePackage` pacchetto versione intervallo (esclusivo) 2.0, 3.0.
Il `allowedVersions` attributo accetta i valori mediante il [formato di intervallo versione](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Si noti che in 1.4, il blocco di un intervallo di versioni specifiche di un pacchetto deve essere modificato manualmente. In NuGet 1.5 si prevede di aggiungere il supporto per questo intervallo tramite l'inserimento di `Install-Package` comando.

### <a name="package-visualizer"></a>Pacchetto Visualizzatore
Il nuovo visualizzatore di pacchetto, avviato tramite il **degli strumenti** -> **Library Package Manager** -> **pacchetto Visualizzatore** opzione di menu consente di visualizzare con facilità tutti i progetti e le relative dipendenze di pacchetto all'interno di una soluzione.

_**Nota importante:** questa funzionalità sfrutta i vantaggi del supporto DGML in Visual Studio. Creare la visualizzazione è supportata solo in Visual Studio Ultimate. Visualizzazione di un diagramma DGML è supportata solo in Visual Studio Premium o superiore._

![Pacchetto Visualizzatore](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Disponibilità di aggiornamenti automatici per la finestra di dialogo di NuGet
Alcune versioni di NuGet introducono nuove funzionalità espresse tramite la `.nuspec` file che non vengono riconosciute dalle versioni precedenti della finestra di dialogo di NuGet.
Un esempio è l'introduzione in NuGet 1.4 per [specificano gli assembly di framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Per questo motivo, è importante usare la versione più recente di NuGet per assicurarsi che è possibile usare i pacchetti a sfruttare le funzionalità più recenti.
Per rendere più visibili gli aggiornamenti a NuGet, finestra di dialogo NuGet contiene la logica per evidenziare quando è disponibile una versione più recente.

_**Nota**: la verifica viene eseguita solo se il **Online** scheda è stata selezionata nella sessione corrente._

![Finestra di dialogo di pacchetti NuGet con la nuova versione disponibile Gestisci](./media/manage-nuget-packages-update-notification.png)

Per disattivare la verifica automatica degli aggiornamenti, passare alla finestra di dialogo Impostazioni NuGet e deselezionare **controlla automaticamente la disponibilità di aggiornamenti**.

![Impostazioni di NuGet](./media/nuget-settings.png)

Questa funzionalità è stata effettivamente aggiunta nella versione 1.3 di NuGet, ma non è visibile, naturalmente, fino a un aggiornamento a 1.3, ad esempio NuGet 1.4, è stato reso disponibile.

### <a name="package-manager-dialog-improvements"></a>Miglioramenti della finestra Gestione pacchetti
* **I nomi dei menu migliorato**: opzioni di Menu per avviare la finestra di dialogo sono state rinominate per maggiore chiarezza. L'opzione di menu è ora **Gestisci pacchetti NuGet**.
* **Riquadro dei dettagli Mostra data di aggiornamento più recente**: NuGet il dialogo viene visualizzata la data dell'aggiornamento più recente nel riquadro dei dettagli per un pacchetto quando il **Online** oppure **Aggiorna** la scheda selezionata.
* **Elenco di tag visualizzato**: Nuget la finestra di dialogo Visualizza tag.

### <a name="powershell-improvements"></a>Miglioramenti di PowerShell
* **Gli script PowerShell firmati**: NuGet include script di Powershell firmati abilitazione utilizzo in ambienti più restrittivi.
* **Richiesta di supporto**: Console di gestione pacchetti supporta ora la richiesta di conferma tramite il `$host.ui.Prompt` e `$host.ui.PromptForChoice` comandi.
* **Nomi di origine del pacchetto**: specificare il nome di un'origine del pacchetto è supportato quando si specifica un'origine pacchetto usando la `-Source` flag.

### <a name="nugetexe-command-line-improvements"></a>miglioramenti della riga di comando NuGet.exe
* **Comandi personalizzati NuGet**: nuget.exe è estensibile tramite i comandi personalizzati tramite MEF.
* **Più semplice il flusso di lavoro per la creazione di pacchetti di simboli**: il `-Symbols` flag può essere applicato a una struttura di cartelle basato sulle convenzioni normali creazione di un pacchetto di simboli includendo solo l'origine e `.pdb` file all'interno della cartella.
* **Specifica di più origini**: il `NuGet install` comando supporta la specifica di più origini con punti e virgola come delimitatore o specificando `-Source` più volte.
* **Supporta l'autenticazione proxy**: NuGet 1.4 aggiunge il supporto per richiedere le credenziali utente quando si usa NuGet dietro un proxy che richiede l'autenticazione.
* **NuGet.exe Update modifica di rilievo**: il `-Self` flag è ora necessario per nuget.exe aggiornarsi. `nuget.exe Update` accetta ora un percorso per il `packages.config` file e tenterà di aggiornare i pacchetti. Si noti che questo aggiornamento è limitato in quanto non vi: * * aggiornare, aggiungere, rimuovere il contenuto nel file di progetto.
* * Eseguire gli script di Powershell all'interno del pacchetto.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Supporto di Server NuGet per il push dei pacchetti usando nuget.exe
NuGet include un modo semplice per ospitare un [repository NuGet basato sul web lightweight](../hosting-packages/nuget-server.md) tramite il `NuGet.Server` pacchetto NuGet. Con NuGet 1.4, il server lightweight supporta il push ed eliminazione di pacchetti tramite nuget.exe.
La versione più recente di `NuGet.Server` aggiunge un nuovo `appSetting`, denominato `apiKey`. Quando la chiave viene omesso o lasciata vuota, il push dei pacchetti nel feed è disabilitato. Se si imposta il valore apiKey su un valore (idealmente una password complessa) consente il push dei pacchetti tramite nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Supporto per Windows Phone strumenti Mango Edition
NuGet è ora supportato nella versione finale candidata di strumenti di Windows Phone per Mango.
Attualmente, gli strumenti di Windows Phone non include il supporto per il gestore estensione di Visual Studio installare NuGet per strumenti di Windows Phone, è necessario scaricare ed eseguire manualmente il progetto VSIX.

Per disinstallare NuGet per strumenti di Windows Phone, eseguire il comando seguente.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correzioni di bug
NuGet 1.4 è basato su un totale di 88 fisso di elementi di lavoro. 71 di questi sono stati contrassegnati come bug.

Per un elenco completo di lavoro elementi di risolti in NuGet 1.4, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug la pena notare:

* [Problema 603](http://nuget.codeplex.com/workitem/603): dipendenze di pacchetto tra repository diversi venga risolto correttamente quando si specifica un'origine di pacchetto specifico.
* [Problema 1036](http://nuget.codeplex.com/workitem/1036): aggiunta di `NuGet Pack SomeProject.csproj` a evento post-compilazione non è più causa un ciclo infinito.
* [Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supporta percorsi relativi.

## <a name="nuget-14-update"></a>Aggiornamento di NuGet 1.4
Poco dopo il rilascio di NuGet 1.4, è stato rilevato un paio di problemi che sono state importante risolvere.
Il numero di versione specifica di questo aggiornamento a 1.4 è 1.4.20615.9020.

### <a name="bug-fixes"></a>Correzioni di bug
* [Problema 1220](http://nuget.codeplex.com/workitem/1220): non esegue Update-Package `install.ps1` / `uninstall.ps1` in tutti i progetti quando è presente più di un progetto
* [Problema 1156](http://nuget.codeplex.com/workitem/1156): modalità Consol Package Manager bloccati su W2K3/XP (quando non è installato Powershell 2)
