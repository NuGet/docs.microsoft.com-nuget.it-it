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
# <a name="nuget-14-release-notes"></a><span data-ttu-id="5f33a-103">Note sulla versione 1.4 di NuGet</span><span class="sxs-lookup"><span data-stu-id="5f33a-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="5f33a-104">[Note sulla versione di NuGet 1.3](../release-notes/nuget-1.3.md) | [note sulla versione di NuGet 1.5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="5f33a-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="5f33a-105">NuGet 1.4 è stato rilasciato il 17 giugno 2011.</span><span class="sxs-lookup"><span data-stu-id="5f33a-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="5f33a-106">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="5f33a-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="5f33a-107">Miglioramenti di Update-Package</span><span class="sxs-lookup"><span data-stu-id="5f33a-107">Update-Package improvements</span></span>
<span data-ttu-id="5f33a-108">NuGet 1.4 introduce numerosi miglioramenti per il comando Update-Package, rendendo più semplice mantenere i pacchetti della stessa versione in più progetti in una soluzione.</span><span class="sxs-lookup"><span data-stu-id="5f33a-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="5f33a-109">Ad esempio, quando si aggiorna un pacchetto alla versione più recente, è molto comune a tutti i progetti con tale pacchetto installato per essere aggiornati il verision stesso.</span><span class="sxs-lookup"><span data-stu-id="5f33a-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="5f33a-110">Il `Update-Package` comando a questo punto, è facile:</span><span class="sxs-lookup"><span data-stu-id="5f33a-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="5f33a-111">Aggiorna tutti i pacchetti in un unico progetto</span><span class="sxs-lookup"><span data-stu-id="5f33a-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="5f33a-112">Aggiornare un pacchetto in tutti i progetti</span><span class="sxs-lookup"><span data-stu-id="5f33a-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="5f33a-113">Aggiorna tutti i pacchetti in tutti i progetti</span><span class="sxs-lookup"><span data-stu-id="5f33a-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="5f33a-114">Eseguire un aggiornamento "sicuro" per tutti i pacchetti</span><span class="sxs-lookup"><span data-stu-id="5f33a-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="5f33a-115">Il `-Safe` flag vincola gli aggiornamenti alle versioni di solo con lo stesso componente di versione principale e secondaria.</span><span class="sxs-lookup"><span data-stu-id="5f33a-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="5f33a-116">Se è installata la versione 1.0.0 di un pacchetto e le versioni 1.0.1, 1.0.2 e 1.1 sono disponibili nel feed, ad esempio il `-Safe` flag aggiorna il pacchetto alla versione 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="5f33a-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="5f33a-117">L'aggiornamento senza il `-Safe` flag potrebbe aggiornare il pacchetto alla versione più recente, 1.1.</span><span class="sxs-lookup"><span data-stu-id="5f33a-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="5f33a-118">La gestione dei pacchetti a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="5f33a-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="5f33a-119">Prima di NuGet 1.4, era complesso usando la finestra di dialogo installa un pacchetto in più progetti.</span><span class="sxs-lookup"><span data-stu-id="5f33a-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="5f33a-120">È necessario avviare la finestra di dialogo una sola volta per ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="5f33a-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="5f33a-121">NuGet 1.4 aggiunge il supporto per i pacchetti di installazione/disinstallazione/aggiornamento in più progetti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="5f33a-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="5f33a-122">Avviare semplicemente il pulsante destro del mouse facendo clic la soluzione e selezionando il **Gestisci pacchetti NuGet** l'opzione di menu.</span><span class="sxs-lookup"><span data-stu-id="5f33a-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Finestra di dialogo Gestisci pacchetti NuGet di livello soluzione](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="5f33a-124">Si noti che nella barra del titolo della finestra di dialogo, viene visualizzato il nome della soluzione, non il nome di un progetto.</span><span class="sxs-lookup"><span data-stu-id="5f33a-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="5f33a-125">Operazioni sui pacchetti forniscono ora un elenco di caselle di controllo con l'elenco dei progetti che per applicare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="5f33a-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gestire la selezione dei progetti i pacchetti NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="5f33a-127">Per altre informazioni, vedere l'argomento sul [gestione dei pacchetti per la soluzione](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="5f33a-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="5f33a-128">Applicazione di un vincolo viene aggiornato a consentite versioni</span><span class="sxs-lookup"><span data-stu-id="5f33a-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="5f33a-129">Per impostazione predefinita, quando si esegue il `Update-Package` comando in un pacchetto o l'aggiornamento del pacchetto mediante finestra di dialogo, verrà aggiornato alla versione più recente nel feed.</span><span class="sxs-lookup"><span data-stu-id="5f33a-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="5f33a-130">Con il nuovo supporto per l'aggiornamento di tutti i pacchetti, potrebbero esserci casi in cui si desidera bloccare un intervallo di versioni specifiche di un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5f33a-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="5f33a-131">Ad esempio, si potrebbe sapere in anticipo che l'applicazione funziona solo con versione 2. \* di un pacchetto, ma non 3.0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="5f33a-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="5f33a-132">Per evitare accidentalmente l'aggiornamento del pacchetto su 3, NuGet 1.4 aggiunge il supporto per vincolare l'intervallo di versioni che i pacchetti possono essere aggiornati a modificando manualmente il `packages.config` file usando il nuovo `allowedVersions` attributo.</span><span class="sxs-lookup"><span data-stu-id="5f33a-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="5f33a-133">Ad esempio, nell'esempio seguente viene illustrato come bloccare i `SomePackage` pacchetto versione intervallo (esclusivo) 2.0, 3.0.</span><span class="sxs-lookup"><span data-stu-id="5f33a-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="5f33a-134">Il `allowedVersions` attributo accetta i valori mediante il [formato di intervallo versione](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="5f33a-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="5f33a-135">Si noti che in 1.4, il blocco di un intervallo di versioni specifiche di un pacchetto deve essere modificato manualmente.</span><span class="sxs-lookup"><span data-stu-id="5f33a-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="5f33a-136">In NuGet 1.5 si prevede di aggiungere il supporto per questo intervallo tramite l'inserimento di `Install-Package` comando.</span><span class="sxs-lookup"><span data-stu-id="5f33a-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="5f33a-137">Pacchetto Visualizzatore</span><span class="sxs-lookup"><span data-stu-id="5f33a-137">Package Visualizer</span></span>
<span data-ttu-id="5f33a-138">Il nuovo visualizzatore di pacchetto, avviato tramite il **degli strumenti** -> **Library Package Manager** -> **pacchetto Visualizzatore** opzione di menu consente di visualizzare con facilità tutti i progetti e le relative dipendenze di pacchetto all'interno di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="5f33a-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="5f33a-139">_**Nota importante:** questa funzionalità sfrutta i vantaggi del supporto DGML in Visual Studio. Creare la visualizzazione è supportata solo in Visual Studio Ultimate. Visualizzazione di un diagramma DGML è supportata solo in Visual Studio Premium o superiore._</span><span class="sxs-lookup"><span data-stu-id="5f33a-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Pacchetto Visualizzatore](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="5f33a-141">Disponibilità di aggiornamenti automatici per la finestra di dialogo di NuGet</span><span class="sxs-lookup"><span data-stu-id="5f33a-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="5f33a-142">Alcune versioni di NuGet introducono nuove funzionalità espresse tramite la `.nuspec` file che non vengono riconosciute dalle versioni precedenti della finestra di dialogo di NuGet.</span><span class="sxs-lookup"><span data-stu-id="5f33a-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="5f33a-143">Un esempio è l'introduzione in NuGet 1.4 per [specificano gli assembly di framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="5f33a-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="5f33a-144">Per questo motivo, è importante usare la versione più recente di NuGet per assicurarsi che è possibile usare i pacchetti a sfruttare le funzionalità più recenti.</span><span class="sxs-lookup"><span data-stu-id="5f33a-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="5f33a-145">Per rendere più visibili gli aggiornamenti a NuGet, finestra di dialogo NuGet contiene la logica per evidenziare quando è disponibile una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="5f33a-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="5f33a-146">_**Nota**: la verifica viene eseguita solo se il **Online** scheda è stata selezionata nella sessione corrente._</span><span class="sxs-lookup"><span data-stu-id="5f33a-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Finestra di dialogo di pacchetti NuGet con la nuova versione disponibile Gestisci](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="5f33a-148">Per disattivare la verifica automatica degli aggiornamenti, passare alla finestra di dialogo Impostazioni NuGet e deselezionare **controlla automaticamente la disponibilità di aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="5f33a-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Impostazioni di NuGet](./media/nuget-settings.png)

<span data-ttu-id="5f33a-150">Questa funzionalità è stata effettivamente aggiunta nella versione 1.3 di NuGet, ma non è visibile, naturalmente, fino a un aggiornamento a 1.3, ad esempio NuGet 1.4, è stato reso disponibile.</span><span class="sxs-lookup"><span data-stu-id="5f33a-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="5f33a-151">Miglioramenti della finestra Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="5f33a-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="5f33a-152">**I nomi dei menu migliorato**: opzioni di Menu per avviare la finestra di dialogo sono state rinominate per maggiore chiarezza.</span><span class="sxs-lookup"><span data-stu-id="5f33a-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="5f33a-153">L'opzione di menu è ora **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5f33a-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="5f33a-154">**Riquadro dei dettagli Mostra data di aggiornamento più recente**: NuGet il dialogo viene visualizzata la data dell'aggiornamento più recente nel riquadro dei dettagli per un pacchetto quando il **Online** oppure **Aggiorna** la scheda selezionata.</span><span class="sxs-lookup"><span data-stu-id="5f33a-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="5f33a-155">**Elenco di tag visualizzato**: Nuget la finestra di dialogo Visualizza tag.</span><span class="sxs-lookup"><span data-stu-id="5f33a-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="5f33a-156">Miglioramenti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f33a-156">Powershell Improvements</span></span>
* <span data-ttu-id="5f33a-157">**Gli script PowerShell firmati**: NuGet include script di Powershell firmati abilitazione utilizzo in ambienti più restrittivi.</span><span class="sxs-lookup"><span data-stu-id="5f33a-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="5f33a-158">**Richiesta di supporto**: Console di gestione pacchetti supporta ora la richiesta di conferma tramite il `$host.ui.Prompt` e `$host.ui.PromptForChoice` comandi.</span><span class="sxs-lookup"><span data-stu-id="5f33a-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="5f33a-159">**Nomi di origine del pacchetto**: specificare il nome di un'origine del pacchetto è supportato quando si specifica un'origine pacchetto usando la `-Source` flag.</span><span class="sxs-lookup"><span data-stu-id="5f33a-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="5f33a-160">miglioramenti della riga di comando NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="5f33a-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="5f33a-161">**Comandi personalizzati NuGet**: nuget.exe è estensibile tramite i comandi personalizzati tramite MEF.</span><span class="sxs-lookup"><span data-stu-id="5f33a-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="5f33a-162">**Più semplice il flusso di lavoro per la creazione di pacchetti di simboli**: il `-Symbols` flag può essere applicato a una struttura di cartelle basato sulle convenzioni normali creazione di un pacchetto di simboli includendo solo l'origine e `.pdb` file all'interno della cartella.</span><span class="sxs-lookup"><span data-stu-id="5f33a-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="5f33a-163">**Specifica di più origini**: il `NuGet install` comando supporta la specifica di più origini con punti e virgola come delimitatore o specificando `-Source` più volte.</span><span class="sxs-lookup"><span data-stu-id="5f33a-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="5f33a-164">**Supporta l'autenticazione proxy**: NuGet 1.4 aggiunge il supporto per richiedere le credenziali utente quando si usa NuGet dietro un proxy che richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="5f33a-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="5f33a-165">**NuGet.exe Update modifica di rilievo**: il `-Self` flag è ora necessario per nuget.exe aggiornarsi.</span><span class="sxs-lookup"><span data-stu-id="5f33a-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="5f33a-166">`nuget.exe Update` accetta ora un percorso per il `packages.config` file e tenterà di aggiornare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="5f33a-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="5f33a-167">Si noti che questo aggiornamento è limitato in quanto non vi: * * aggiornare, aggiungere, rimuovere il contenuto nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="5f33a-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="5f33a-168">* * Eseguire gli script di Powershell all'interno del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5f33a-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="5f33a-169">Supporto di Server NuGet per il push dei pacchetti usando nuget.exe</span><span class="sxs-lookup"><span data-stu-id="5f33a-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="5f33a-170">NuGet include un modo semplice per ospitare un [repository NuGet basato sul web lightweight](../hosting-packages/nuget-server.md) tramite il `NuGet.Server` pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="5f33a-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="5f33a-171">Con NuGet 1.4, il server lightweight supporta il push ed eliminazione di pacchetti tramite nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="5f33a-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="5f33a-172">La versione più recente di `NuGet.Server` aggiunge un nuovo `appSetting`, denominato `apiKey`.</span><span class="sxs-lookup"><span data-stu-id="5f33a-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="5f33a-173">Quando la chiave viene omesso o lasciata vuota, il push dei pacchetti nel feed è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="5f33a-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="5f33a-174">Se si imposta il valore apiKey su un valore (idealmente una password complessa) consente il push dei pacchetti tramite nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="5f33a-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="5f33a-175">Supporto per Windows Phone strumenti Mango Edition</span><span class="sxs-lookup"><span data-stu-id="5f33a-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="5f33a-176">NuGet è ora supportato nella versione finale candidata di strumenti di Windows Phone per Mango.</span><span class="sxs-lookup"><span data-stu-id="5f33a-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="5f33a-177">Attualmente, gli strumenti di Windows Phone non include il supporto per il gestore estensione di Visual Studio installare NuGet per strumenti di Windows Phone, è necessario scaricare ed eseguire manualmente il progetto VSIX.</span><span class="sxs-lookup"><span data-stu-id="5f33a-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="5f33a-178">Per disinstallare NuGet per strumenti di Windows Phone, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5f33a-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="5f33a-179">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="5f33a-179">Bug Fixes</span></span>
<span data-ttu-id="5f33a-180">NuGet 1.4 è basato su un totale di 88 fisso di elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="5f33a-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="5f33a-181">71 di questi sono stati contrassegnati come bug.</span><span class="sxs-lookup"><span data-stu-id="5f33a-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="5f33a-182">Per un elenco completo di lavoro elementi di risolti in NuGet 1.4, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="5f33a-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="5f33a-183">Correzioni di bug la pena notare:</span><span class="sxs-lookup"><span data-stu-id="5f33a-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="5f33a-184">[Problema 603](http://nuget.codeplex.com/workitem/603): dipendenze di pacchetto tra repository diversi venga risolto correttamente quando si specifica un'origine di pacchetto specifico.</span><span class="sxs-lookup"><span data-stu-id="5f33a-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="5f33a-185">[Problema 1036](http://nuget.codeplex.com/workitem/1036): aggiunta di `NuGet Pack SomeProject.csproj` a evento post-compilazione non è più causa un ciclo infinito.</span><span class="sxs-lookup"><span data-stu-id="5f33a-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="5f33a-186">[Problema 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supporta percorsi relativi.</span><span class="sxs-lookup"><span data-stu-id="5f33a-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="5f33a-187">Aggiornamento di NuGet 1.4</span><span class="sxs-lookup"><span data-stu-id="5f33a-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="5f33a-188">Poco dopo il rilascio di NuGet 1.4, è stato rilevato un paio di problemi che sono state importante risolvere.</span><span class="sxs-lookup"><span data-stu-id="5f33a-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="5f33a-189">Il numero di versione specifica di questo aggiornamento a 1.4 è 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="5f33a-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="5f33a-190">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="5f33a-190">Bug Fixes</span></span>
* <span data-ttu-id="5f33a-191">[Problema 1220](http://nuget.codeplex.com/workitem/1220): non esegue Update-Package `install.ps1` / `uninstall.ps1` in tutti i progetti quando è presente più di un progetto</span><span class="sxs-lookup"><span data-stu-id="5f33a-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="5f33a-192">[Problema 1156](http://nuget.codeplex.com/workitem/1156): modalità Consol Package Manager bloccati su W2K3/XP (quando non è installato Powershell 2)</span><span class="sxs-lookup"><span data-stu-id="5f33a-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
