---
title: Note sulla versione 1.4 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Note sulla versione per NuGet 1.4 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
keywords: 1.4 NuGet note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 1229cd7fddb826902478b69cfdbc16a8ed192b64
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="c9255-104">Note sulla versione 1.4 di NuGet</span><span class="sxs-lookup"><span data-stu-id="c9255-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="c9255-105">[Note sulla versione 1.3 NuGet](../release-notes/nuget-1.3.md) | [note sulla versione 1.5 di NuGet](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="c9255-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="c9255-106">NuGet 1.4 è stata rilasciata 17 giugno 2011.</span><span class="sxs-lookup"><span data-stu-id="c9255-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="c9255-107">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="c9255-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="c9255-108">Miglioramenti di pacchetto di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="c9255-108">Update-Package improvements</span></span>
<span data-ttu-id="c9255-109">1.4 NuGet introduce numerosi miglioramenti per il comando di pacchetto di aggiornamento, rendendo più semplice mantenere i pacchetti della stessa versione in più progetti in una soluzione.</span><span class="sxs-lookup"><span data-stu-id="c9255-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="c9255-110">Ad esempio, quando si aggiorna un pacchetto alla versione più recente, è molto comune a tutti i progetti con tale pacchetto installato per essere aggiornati per la stessa verision.</span><span class="sxs-lookup"><span data-stu-id="c9255-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="c9255-111">Il `Update-Package` comando ora, è facile:</span><span class="sxs-lookup"><span data-stu-id="c9255-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="c9255-112">Aggiornare tutti i pacchetti in un unico progetto</span><span class="sxs-lookup"><span data-stu-id="c9255-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="c9255-113">Aggiornare un pacchetto in tutti i progetti</span><span class="sxs-lookup"><span data-stu-id="c9255-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="c9255-114">Aggiornare tutti i pacchetti in tutti i progetti</span><span class="sxs-lookup"><span data-stu-id="c9255-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="c9255-115">Eseguire un aggiornamento "sicuro" per tutti i pacchetti</span><span class="sxs-lookup"><span data-stu-id="c9255-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="c9255-116">Il `-Safe` flag vincola gli aggiornamenti alle versioni sole con lo stesso componente di versione principale e secondaria.</span><span class="sxs-lookup"><span data-stu-id="c9255-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="c9255-117">Se è installata la versione 1.0.0 di un pacchetto e le versioni 1.0.1, 1.0.2 e 1.1 sono disponibili nel feed, ad esempio il `-Safe` flag aggiorna il pacchetto alla versione 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="c9255-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="c9255-118">L'aggiornamento senza il `-Safe` flag necessario aggiornare il pacchetto alla versione più recente, 1.1.</span><span class="sxs-lookup"><span data-stu-id="c9255-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="c9255-119">La gestione dei pacchetti a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="c9255-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="c9255-120">Prima di NuGet 1.4, installa un pacchetto in più progetti era complessa utilizzando la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="c9255-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="c9255-121">È necessario avviare la finestra di dialogo una volta per ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="c9255-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="c9255-122">1.4 NuGet aggiunge il supporto per i pacchetti di installazione o disinstallazione / l'aggiornamento in più progetti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c9255-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="c9255-123">Avviare semplicemente la facendo clic con il pulsante destro la soluzione e selezionando il **Gestisci pacchetti NuGet** opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="c9255-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Finestra di dialogo Gestisci pacchetti NuGet di livello soluzione](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="c9255-125">Si noti che nella barra del titolo della finestra di dialogo, viene visualizzato il nome della soluzione, non il nome di un progetto.</span><span class="sxs-lookup"><span data-stu-id="c9255-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="c9255-126">Operazioni sui pacchetti forniscono ora un elenco di caselle di controllo con l'elenco dei progetti che per applicare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="c9255-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gestisci pacchetti NuGet la selezione dei progetti](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="c9255-128">Per ulteriori informazioni, vedere l'argomento su [Gestione pacchetti per la soluzione](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="c9255-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="c9255-129">Vincolare viene aggiornato a consentito versioni</span><span class="sxs-lookup"><span data-stu-id="c9255-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="c9255-130">Per impostazione predefinita, quando si esegue il `Update-Package` comando in un pacchetto (o l'aggiornamento del pacchetto tramite una finestra di dialogo), verrà eseguito un aggiornamento alla versione più recente nel feed.</span><span class="sxs-lookup"><span data-stu-id="c9255-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="c9255-131">Con il nuovo supporto per l'aggiornamento di tutti i pacchetti, potrebbe essere casi in cui si desidera bloccare un intervallo di versioni specifiche di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c9255-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="c9255-132">Ad esempio, si potrebbe sapere in anticipo che l'applicazione funziona solo con 2.\* versione di un pacchetto, ma non 3.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c9255-132">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="c9255-133">Per evitare accidentalmente l'aggiornamento del pacchetto su 3, 1.4 NuGet aggiunge il supporto per vincolare l'intervallo di versioni di pacchetti possono essere aggiornati a modificando manualmente il `packages.config` file utilizzando il nuovo `allowedVersions` attributo.</span><span class="sxs-lookup"><span data-stu-id="c9255-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="c9255-134">Ad esempio, nell'esempio seguente viene illustrato come bloccare il `SomePackage` pacchetto alla versione intervallo (esclusivo) 2.0, 3.0.</span><span class="sxs-lookup"><span data-stu-id="c9255-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="c9255-135">Il `allowedVersions` attributo accetta valori utilizzando il [formato intervallo versione](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="c9255-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="c9255-136">Si noti che in 1.4, il blocco di un intervallo di versioni specifiche di un pacchetto deve essere modificato manualmente.</span><span class="sxs-lookup"><span data-stu-id="c9255-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="c9255-137">1.5 NuGet si intende aggiungere il supporto per la distribuzione di questo intervallo tramite il `Install-Package` comando.</span><span class="sxs-lookup"><span data-stu-id="c9255-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="c9255-138">Visualizzatore di pacchetto</span><span class="sxs-lookup"><span data-stu-id="c9255-138">Package Visualizer</span></span>
<span data-ttu-id="c9255-139">Il nuovo visualizzatore del pacchetto, avviato tramite il **strumenti** -> **Gestione pacchetti libreria** -> **pacchetto Visualizzatore** opzione di menu, consente di Consente di visualizzare facilmente tutti i progetti e le relative dipendenze di pacchetto all'interno di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="c9255-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="c9255-140">_**Nota importante:** questa funzionalità consente di sfruttare il supporto DGML in Visual Studio. Creazione della visualizzazione è supportata solo in Visual Studio Ultimate. Visualizzazione di un diagramma DGML è supportata solo in Visual Studio Premium o superiore._</span><span class="sxs-lookup"><span data-stu-id="c9255-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualizzatore di pacchetto](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="c9255-142">Controllo di aggiornamento automatico per la finestra di dialogo NuGet</span><span class="sxs-lookup"><span data-stu-id="c9255-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="c9255-143">Alcune versioni di NuGet introducono nuove funzionalità espressa tramite il `.nuspec` file che non vengono riconosciuti da versioni precedenti della finestra di dialogo NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9255-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="c9255-144">Un esempio è l'introduzione in NuGet 1.4 per [specificano gli assembly framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="c9255-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="c9255-145">Per questo motivo, è importante utilizzare la versione più recente di NuGet per verificare che è possibile utilizzare pacchetti sfruttando le funzionalità più recenti.</span><span class="sxs-lookup"><span data-stu-id="c9255-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="c9255-146">Per rendere più visibili gli aggiornamenti a NuGet, la finestra di dialogo NuGet contiene la logica per evidenziare quando è disponibile una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="c9255-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="c9255-147">_**Nota**: il controllo viene eseguito solo se il **Online** scheda è stata selezionata nella sessione corrente._</span><span class="sxs-lookup"><span data-stu-id="c9255-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Finestra di dialogo di pacchetti NuGet con disponibile una nuova versione di gestione](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="c9255-149">Per disattivare il controllo automatico per gli aggiornamenti, passare alla finestra di dialogo Impostazioni NuGet e deselezionare **controlla automaticamente la disponibilità di aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="c9255-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Impostazioni di NuGet](./media/nuget-settings.png)

<span data-ttu-id="c9255-151">Questa funzionalità è stata effettivamente aggiunta NuGet 1.3, ma non sarà visibile, naturalmente, fino a quando un aggiornamento a 1.3, ad esempio NuGet 1.4, è stata resa disponibile.</span><span class="sxs-lookup"><span data-stu-id="c9255-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="c9255-152">Miglioramenti della finestra di dialogo Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="c9255-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="c9255-153">**I nomi dei menu migliorata**: opzioni di Menu per avviare la finestra di dialogo sono state rinominate per maggiore chiarezza.</span><span class="sxs-lookup"><span data-stu-id="c9255-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="c9255-154">L'opzione di menu è ora **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c9255-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="c9255-155">**Riquadro dei dettagli Mostra la data di aggiornamento più recente**: NuGet la finestra di dialogo viene visualizzata la data dell'ultimo aggiornamento nel riquadro dei dettagli per un pacchetto quando il **Online** o **Aggiorna** scheda viene selezionata.</span><span class="sxs-lookup"><span data-stu-id="c9255-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="c9255-156">**Elenco di tag visualizzato**: Nuget la finestra di dialogo Visualizza tag.</span><span class="sxs-lookup"><span data-stu-id="c9255-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="c9255-157">Miglioramenti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9255-157">Powershell Improvements</span></span>
* <span data-ttu-id="c9255-158">**Gli script di PowerShell firmati**: NuGet include script Powershell firmati abilitazione dell'utilizzo in ambienti più restrittivi.</span><span class="sxs-lookup"><span data-stu-id="c9255-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="c9255-159">**Richiesta di supporto**: nella Console di gestione pacchetti supporta ora la richiesta di conferma tramite il `$host.ui.Prompt` e `$host.ui.PromptForChoice` comandi.</span><span class="sxs-lookup"><span data-stu-id="c9255-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="c9255-160">**I nomi di origine del pacchetto**: specificando il nome di un'origine pacchetto è supportato quando si specifica un'origine pacchetto usando la `-Source` flag.</span><span class="sxs-lookup"><span data-stu-id="c9255-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="c9255-161">miglioramenti della riga di comando di NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="c9255-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="c9255-162">**I comandi personalizzati NuGet**: nuget.exe è estensibile tramite i comandi personalizzati tramite MEF.</span><span class="sxs-lookup"><span data-stu-id="c9255-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="c9255-163">**Più semplice il flusso di lavoro per la creazione di pacchetti di simboli**: il `-Symbols` flag può essere applicato a una struttura di cartelle basato sulle convenzioni normali creazione di un pacchetto di simboli includendo solo l'origine e `.pdb` file all'interno della cartella.</span><span class="sxs-lookup"><span data-stu-id="c9255-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="c9255-164">**Specifica di più origini**: il `NuGet install` comando supporta la specifica di più origini con punti e virgola come delimitatore o specificando `-Source` più volte.</span><span class="sxs-lookup"><span data-stu-id="c9255-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="c9255-165">**Supporta l'autenticazione proxy**: 1.4 NuGet aggiunge il supporto per richiedere le credenziali utente quando si usa NuGet dietro un proxy che richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c9255-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="c9255-166">**NuGet.exe aggiornare modifiche di rilievo**: il `-Self` flag è ora necessario per nuget.exe di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c9255-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="c9255-167">`nuget.exe Update` accetta ora in un percorso per il `packages.config` tenterà di pacchetti di aggiornamento e file.</span><span class="sxs-lookup"><span data-stu-id="c9255-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="c9255-168">Si noti che questo aggiornamento è limitato in quanto non vi: * * aggiornare, aggiungere, rimuovere il contenuto nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="c9255-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="c9255-169">* * Eseguire gli script di Powershell all'interno del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c9255-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="c9255-170">Supporto di Server NuGet per i pacchetti push utilizzando nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c9255-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="c9255-171">NuGet include un modo semplice per ospitare un [web semplice basato su repository NuGet](../hosting-packages/nuget-server.md) tramite il `NuGet.Server` pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="c9255-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="c9255-172">Con NuGet 1.4, il server lightweight supporta push e l'eliminazione dei pacchetti utilizzando nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="c9255-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="c9255-173">La versione più recente di `NuGet.Server` aggiunge un nuovo `appSetting`, denominato `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="c9255-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="c9255-174">Quando la chiave viene omesso o viene lasciata vuota, inserendo i pacchetti per il feed è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="c9255-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="c9255-175">Impostazione di apiKey su un valore (idealmente una password complessa) consente pacchetti push utilizzando nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="c9255-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="c9255-176">Supporto per Windows Phone strumenti Mango Edition</span><span class="sxs-lookup"><span data-stu-id="c9255-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="c9255-177">NuGet è ora supportato nella versione finale candidata di strumenti di Windows Phone per Mango.</span><span class="sxs-lookup"><span data-stu-id="c9255-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="c9255-178">Attualmente, gli strumenti di Windows Phone non dispone del supporto per la gestione di estensione di Visual Studio installare NuGet per strumenti di Windows Phone, è necessario scaricare ed eseguire manualmente il progetto VSIX.</span><span class="sxs-lookup"><span data-stu-id="c9255-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="c9255-179">Per disinstallare NuGet per strumenti di Windows Phone, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="c9255-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="c9255-180">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="c9255-180">Bug Fixes</span></span>
<span data-ttu-id="c9255-181">1.4 NuGet era un totale di 88 fissati di elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c9255-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="c9255-182">71 di quelli contrassegnati come bug.</span><span class="sxs-lookup"><span data-stu-id="c9255-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="c9255-183">Per un elenco completo di lavoro gli elementi corretti in NuGet 1.4,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="c9255-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="c9255-184">Correzioni di bug non degni di nota:</span><span class="sxs-lookup"><span data-stu-id="c9255-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="c9255-185">[Problema 603](http://nuget.codeplex.com/workitem/603): le dipendenze dei pacchetti in repository diversi venga risolto correttamente quando si specifica un'origine pacchetto specifico.</span><span class="sxs-lookup"><span data-stu-id="c9255-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="c9255-186">[Problema 1036](http://nuget.codeplex.com/workitem/1036): aggiunta di `NuGet Pack SomeProject.csproj` di post-evento di compilazione non è più causa un ciclo infinito.</span><span class="sxs-lookup"><span data-stu-id="c9255-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="c9255-187">[Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supporta percorsi relativi.</span><span class="sxs-lookup"><span data-stu-id="c9255-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="c9255-188">Aggiornamento di NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="c9255-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="c9255-189">Poco dopo il rilascio di NuGet 1.4, è stato rilevato un paio di problemi che sono stati importante risolvere.</span><span class="sxs-lookup"><span data-stu-id="c9255-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="c9255-190">Il numero di versione specifica di questo aggiornamento per 1.4 è 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="c9255-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="c9255-191">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="c9255-191">Bug Fixes</span></span>
* <span data-ttu-id="c9255-192">[Problema 1220](http://nuget.codeplex.com/workitem/1220): pacchetto di aggiornamento non esegue `install.ps1` / `uninstall.ps1` in tutti i progetti quando è presente più di un progetto</span><span class="sxs-lookup"><span data-stu-id="c9255-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="c9255-193">[Problema 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol bloccati in W2K3/XP (quando non è installato Powershell 2)</span><span class="sxs-lookup"><span data-stu-id="c9255-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
