---
title: Note sulla versione 1.4 di NuGet
description: Note sulla versione per NuGet 1.4 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5e4c2a5f2db80b0ebc3fec7c653aecb8bcc4ab5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822058"
---
# <a name="nuget-14-release-notes"></a>Note sulla versione 1.4 di NuGet

[Note sulla versione 1.3 NuGet](../release-notes/nuget-1.3.md) | [note sulla versione 1.5 di NuGet](../release-notes/nuget-1.5.md)

NuGet 1.4 è stata rilasciata 17 giugno 2011.

## <a name="features"></a>Funzionalità

### <a name="update-package-improvements"></a>Miglioramenti di pacchetto di aggiornamento
1.4 NuGet introduce numerosi miglioramenti per il comando di pacchetto di aggiornamento, rendendo più semplice mantenere i pacchetti della stessa versione in più progetti in una soluzione. Ad esempio, quando si aggiorna un pacchetto alla versione più recente, è molto comune a tutti i progetti con tale pacchetto installato per essere aggiornati per la stessa verision.

Il `Update-Package` comando ora, è facile:

#### <a name="update-all-packages-in-a-single-project"></a>Aggiornare tutti i pacchetti in un unico progetto

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a>Aggiornare un pacchetto in tutti i progetti

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a>Aggiornare tutti i pacchetti in tutti i progetti

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a>Eseguire un aggiornamento "sicuro" per tutti i pacchetti
Il `-Safe` flag vincola gli aggiornamenti alle versioni sole con lo stesso componente di versione principale e secondaria. Se è installata la versione 1.0.0 di un pacchetto e le versioni 1.0.1, 1.0.2 e 1.1 sono disponibili nel feed, ad esempio il `-Safe` flag aggiorna il pacchetto alla versione 1.0.2. L'aggiornamento senza il `-Safe` flag necessario aggiornare il pacchetto alla versione più recente, 1.1.

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a>La gestione dei pacchetti a livello di soluzione
Prima di NuGet 1.4, installa un pacchetto in più progetti era complessa utilizzando la finestra di dialogo. È necessario avviare la finestra di dialogo una volta per ogni progetto.

1.4 NuGet aggiunge il supporto per i pacchetti di installazione o disinstallazione / l'aggiornamento in più progetti contemporaneamente. Avviare semplicemente la facendo clic con il pulsante destro la soluzione e selezionando il **Gestisci pacchetti NuGet** opzione di menu.

![Finestra di dialogo Gestisci pacchetti NuGet di livello soluzione](./media/manage-nuget-packages-solution-dialog.png)

Si noti che nella barra del titolo della finestra di dialogo, viene visualizzato il nome della soluzione, non il nome di un progetto.
Operazioni sui pacchetti forniscono ora un elenco di caselle di controllo con l'elenco dei progetti che per applicare l'operazione.

![Gestisci pacchetti NuGet la selezione dei progetti](./media/manage-nuget-packages-project-selection.png)

Per ulteriori informazioni, vedere l'argomento su [Gestione pacchetti per la soluzione](../tools/package-manager-ui.md#managing-packages-for-the-solution).

### <a name="constraining-upgrades-to-allowed-versions"></a>Vincolare viene aggiornato a consentito versioni
Per impostazione predefinita, quando si esegue il `Update-Package` comando in un pacchetto (o l'aggiornamento del pacchetto tramite una finestra di dialogo), verrà eseguito un aggiornamento alla versione più recente nel feed. Con il nuovo supporto per l'aggiornamento di tutti i pacchetti, potrebbe essere casi in cui si desidera bloccare un intervallo di versioni specifiche di un pacchetto. Ad esempio, si potrebbe sapere in anticipo che l'applicazione funziona solo con 2.* versione di un pacchetto, ma non 3.0 e versioni successive. Per evitare accidentalmente l'aggiornamento del pacchetto su 3, 1.4 NuGet aggiunge il supporto per vincolare l'intervallo di versioni di pacchetti possono essere aggiornati a modificando manualmente il `packages.config` file utilizzando il nuovo `allowedVersions` attributo.

Ad esempio, nell'esempio seguente viene illustrato come bloccare il `SomePackage` pacchetto alla versione intervallo (esclusivo) 2.0, 3.0.
Il `allowedVersions` attributo accetta valori utilizzando il [formato intervallo versione](../reference/package-versioning.md#version-ranges-and-wildcards).

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

Si noti che in 1.4, il blocco di un intervallo di versioni specifiche di un pacchetto deve essere modificato manualmente. 1.5 NuGet si intende aggiungere il supporto per la distribuzione di questo intervallo tramite il `Install-Package` comando.

### <a name="package-visualizer"></a>Visualizzatore di pacchetto
Il nuovo visualizzatore del pacchetto, avviato tramite il **strumenti** -> **Gestione pacchetti libreria** -> **pacchetto Visualizzatore** opzione di menu, consente di Consente di visualizzare facilmente tutti i progetti e le relative dipendenze di pacchetto all'interno di una soluzione.

_**Nota importante:** questa funzionalità consente di sfruttare il supporto DGML in Visual Studio. Creazione della visualizzazione è supportata solo in Visual Studio Ultimate. Visualizzazione di un diagramma DGML è supportata solo in Visual Studio Premium o superiore._

![Visualizzatore di pacchetto](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a>Controllo di aggiornamento automatico per la finestra di dialogo NuGet
Alcune versioni di NuGet introducono nuove funzionalità espressa tramite il `.nuspec` file che non vengono riconosciuti da versioni precedenti della finestra di dialogo NuGet.
Un esempio è l'introduzione in NuGet 1.4 per [specificano gli assembly framework](../release-notes/nuget-1.2.md#framework-assembly-refs).
Per questo motivo, è importante utilizzare la versione più recente di NuGet per verificare che è possibile utilizzare pacchetti sfruttando le funzionalità più recenti.
Per rendere più visibili gli aggiornamenti a NuGet, la finestra di dialogo NuGet contiene la logica per evidenziare quando è disponibile una versione più recente.

_**Nota**: il controllo viene eseguito solo se il **Online** scheda è stata selezionata nella sessione corrente._

![Finestra di dialogo di pacchetti NuGet con disponibile una nuova versione di gestione](./media/manage-nuget-packages-update-notification.png)

Per disattivare il controllo automatico per gli aggiornamenti, passare alla finestra di dialogo Impostazioni NuGet e deselezionare **controlla automaticamente la disponibilità di aggiornamenti**.

![Impostazioni di NuGet](./media/nuget-settings.png)

Questa funzionalità è stata effettivamente aggiunta NuGet 1.3, ma non sarà visibile, naturalmente, fino a quando un aggiornamento a 1.3, ad esempio NuGet 1.4, è stata resa disponibile.

### <a name="package-manager-dialog-improvements"></a>Miglioramenti della finestra di dialogo Gestione pacchetti
* **I nomi dei menu migliorata**: opzioni di Menu per avviare la finestra di dialogo sono state rinominate per maggiore chiarezza. L'opzione di menu è ora **Gestisci pacchetti NuGet**.
* **Riquadro dei dettagli Mostra la data di aggiornamento più recente**: NuGet la finestra di dialogo viene visualizzata la data dell'ultimo aggiornamento nel riquadro dei dettagli per un pacchetto quando il **Online** o **Aggiorna** scheda viene selezionata.
* **Elenco di tag visualizzato**: Nuget la finestra di dialogo Visualizza tag.

### <a name="powershell-improvements"></a>Miglioramenti di PowerShell
* **Gli script di PowerShell firmati**: NuGet include script Powershell firmati abilitazione dell'utilizzo in ambienti più restrittivi.
* **Richiesta di supporto**: nella Console di gestione pacchetti supporta ora la richiesta di conferma tramite il `$host.ui.Prompt` e `$host.ui.PromptForChoice` comandi.
* **I nomi di origine del pacchetto**: specificando il nome di un'origine pacchetto è supportato quando si specifica un'origine pacchetto usando la `-Source` flag.

### <a name="nugetexe-command-line-improvements"></a>miglioramenti della riga di comando di NuGet.exe
* **I comandi personalizzati NuGet**: nuget.exe è estensibile tramite i comandi personalizzati tramite MEF.
* **Più semplice il flusso di lavoro per la creazione di pacchetti di simboli**: il `-Symbols` flag può essere applicato a una struttura di cartelle basato sulle convenzioni normali creazione di un pacchetto di simboli includendo solo l'origine e `.pdb` file all'interno della cartella.
* **Specifica di più origini**: il `NuGet install` comando supporta la specifica di più origini con punti e virgola come delimitatore o specificando `-Source` più volte.
* **Supporta l'autenticazione proxy**: 1.4 NuGet aggiunge il supporto per richiedere le credenziali utente quando si usa NuGet dietro un proxy che richiede l'autenticazione.
* **NuGet.exe aggiornare modifiche di rilievo**: il `-Self` flag è ora necessario per nuget.exe di aggiornamento. `nuget.exe Update` accetta ora in un percorso per il `packages.config` tenterà di pacchetti di aggiornamento e file. Si noti che questo aggiornamento è limitato in quanto non vi: * * aggiornare, aggiungere, rimuovere il contenuto nel file di progetto.
* * Eseguire gli script di Powershell all'interno del pacchetto.

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a>Supporto di Server NuGet per i pacchetti push utilizzando nuget.exe
NuGet include un modo semplice per ospitare un [web semplice basato su repository NuGet](../hosting-packages/nuget-server.md) tramite il `NuGet.Server` pacchetto NuGet. Con NuGet 1.4, il server lightweight supporta push e l'eliminazione dei pacchetti utilizzando nuget.exe.
La versione più recente di `NuGet.Server` aggiunge un nuovo `appSetting`, denominato `apiKey`. Quando la chiave viene omesso o viene lasciata vuota, inserendo i pacchetti per il feed è disabilitato. Impostazione di apiKey su un valore (idealmente una password complessa) consente pacchetti push utilizzando nuget.exe.

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a>Supporto per Windows Phone strumenti Mango Edition
NuGet è ora supportato nella versione finale candidata di strumenti di Windows Phone per Mango.
Attualmente, gli strumenti di Windows Phone non dispone del supporto per la gestione di estensione di Visual Studio installare NuGet per strumenti di Windows Phone, è necessario scaricare ed eseguire manualmente il progetto VSIX.

Per disinstallare NuGet per strumenti di Windows Phone, eseguire il comando seguente.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a>Correzioni di bug
1.4 NuGet era un totale di 88 fissati di elementi di lavoro. 71 di quelli contrassegnati come bug.

Per un elenco completo di lavoro gli elementi corretti in NuGet 1.4,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Correzioni di bug non degni di nota:

* [Problema 603](http://nuget.codeplex.com/workitem/603): le dipendenze dei pacchetti in repository diversi venga risolto correttamente quando si specifica un'origine pacchetto specifico.
* [Problema 1036](http://nuget.codeplex.com/workitem/1036): aggiunta di `NuGet Pack SomeProject.csproj` di post-evento di compilazione non è più causa un ciclo infinito.
* [Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supporta percorsi relativi.

## <a name="nuget-14-update"></a>Aggiornamento di NuGet 1.4
Poco dopo il rilascio di NuGet 1.4, è stato rilevato un paio di problemi che sono stati importante risolvere.
Il numero di versione specifica di questo aggiornamento per 1.4 è 1.4.20615.9020.

### <a name="bug-fixes"></a>Correzioni di bug
* [Problema 1220](http://nuget.codeplex.com/workitem/1220): pacchetto di aggiornamento non esegue `install.ps1` / `uninstall.ps1` in tutti i progetti quando è presente più di un progetto
* [Problema 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol bloccati in W2K3/XP (quando non è installato Powershell 2)
