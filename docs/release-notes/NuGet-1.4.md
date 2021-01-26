---
title: Note sulla versione di NuGet 1,4
description: Note sulla versione per NuGet 1,4, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777140"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="e79dc-103">Note sulla versione di NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="e79dc-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="e79dc-104">Note sulla versione di [NuGet 1,3](../release-notes/nuget-1.3.md)  |  [Note sulla versione di NuGet 1,5](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="e79dc-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="e79dc-105">NuGet 1,4 è stato rilasciato il 17 giugno 2011.</span><span class="sxs-lookup"><span data-stu-id="e79dc-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="e79dc-106">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="e79dc-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="e79dc-107">Miglioramenti di Update-Package</span><span class="sxs-lookup"><span data-stu-id="e79dc-107">Update-Package improvements</span></span>
<span data-ttu-id="e79dc-108">In NuGet 1,4 sono stati introdotti numerosi miglioramenti al comando Update-Package che semplificano la conservazione dei pacchetti con la stessa versione tra più progetti in una soluzione.</span><span class="sxs-lookup"><span data-stu-id="e79dc-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="e79dc-109">Ad esempio, quando si aggiorna un pacchetto alla versione più recente, è molto comune che tutti i progetti con il pacchetto installato vengano aggiornati allo stesso Verision.</span><span class="sxs-lookup"><span data-stu-id="e79dc-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="e79dc-110">Il `Update-Package` comando ora rende più semplice:</span><span class="sxs-lookup"><span data-stu-id="e79dc-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="e79dc-111">Aggiornare tutti i pacchetti in un singolo progetto</span><span class="sxs-lookup"><span data-stu-id="e79dc-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="e79dc-112">Aggiornare un pacchetto in tutti i progetti</span><span class="sxs-lookup"><span data-stu-id="e79dc-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="e79dc-113">Aggiorna tutti i pacchetti in tutti i progetti</span><span class="sxs-lookup"><span data-stu-id="e79dc-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="e79dc-114">Eseguire un aggiornamento "sicuro" su tutti i pacchetti</span><span class="sxs-lookup"><span data-stu-id="e79dc-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="e79dc-115">Il `-Safe` flag vincola gli aggiornamenti solo alle versioni con lo stesso componente della versione principale e secondaria.</span><span class="sxs-lookup"><span data-stu-id="e79dc-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="e79dc-116">Se, ad esempio, è installata la versione 1.0.0 di un pacchetto e nel feed sono disponibili le versioni 1.0.1, 1.0.2 e 1,1, il `-Safe` flag aggiorna il pacchetto alla versione 1.0.2.</span><span class="sxs-lookup"><span data-stu-id="e79dc-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="e79dc-117">Se si esegue l'aggiornamento senza il `-Safe` flag, il pacchetto verrà aggiornato alla versione più recente 1,1.</span><span class="sxs-lookup"><span data-stu-id="e79dc-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="e79dc-118">Gestione dei pacchetti a livello di soluzione</span><span class="sxs-lookup"><span data-stu-id="e79dc-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="e79dc-119">Prima di NuGet 1,4, l'installazione di un pacchetto in più progetti è stata complessa usando la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="e79dc-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="e79dc-120">È necessario avviare la finestra di dialogo una volta per ogni progetto.</span><span class="sxs-lookup"><span data-stu-id="e79dc-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="e79dc-121">NuGet 1,4 aggiunge il supporto per l'installazione/disinstallazione o l'aggiornamento di pacchetti in più progetti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="e79dc-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="e79dc-122">È sufficiente avviare il facendo clic con il pulsante destro del mouse sulla soluzione e selezionando l'opzione di menu **Gestisci pacchetti NuGet** .</span><span class="sxs-lookup"><span data-stu-id="e79dc-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Finestra di dialogo Gestisci pacchetti NuGet di livello soluzione](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="e79dc-124">Si noti che nella barra del titolo della finestra di dialogo viene visualizzato il nome della soluzione, non il nome di un progetto.</span><span class="sxs-lookup"><span data-stu-id="e79dc-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="e79dc-125">Le operazioni sui pacchetti forniscono ora un elenco di caselle di controllo con l'elenco dei progetti a cui deve essere applicata l'operazione.</span><span class="sxs-lookup"><span data-stu-id="e79dc-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Gestisci selezione progetto pacchetti NuGet](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="e79dc-127">Per ulteriori informazioni, vedere l'argomento relativo alla [gestione dei pacchetti per la soluzione](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="e79dc-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="e79dc-128">Limitazione degli aggiornamenti alle versioni consentite</span><span class="sxs-lookup"><span data-stu-id="e79dc-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="e79dc-129">Per impostazione predefinita, quando si esegue il `Update-Package` comando in un pacchetto (o si aggiorna il pacchetto utilizzando la finestra di dialogo), questo verrà aggiornato alla versione più recente nel feed.</span><span class="sxs-lookup"><span data-stu-id="e79dc-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="e79dc-130">Con il nuovo supporto per l'aggiornamento di tutti i pacchetti, in alcuni casi è possibile che si desideri bloccare un pacchetto in un intervallo di versioni specifico.</span><span class="sxs-lookup"><span data-stu-id="e79dc-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="e79dc-131">Ad esempio, è possibile che si sappia che l'applicazione funzionerà solo con la versione 2. \* di un pacchetto, ma non con 3,0 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="e79dc-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="e79dc-132">Per evitare l'aggiornamento accidentale del pacchetto a 3, NuGet 1,4 aggiunge il supporto per limitare l'intervallo di versioni in cui i pacchetti possono essere aggiornati manualmente modificando il `packages.config` file usando il nuovo `allowedVersions` attributo.</span><span class="sxs-lookup"><span data-stu-id="e79dc-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="e79dc-133">Ad esempio, nell'esempio seguente viene illustrato come bloccare il `SomePackage` pacchetto con intervallo di versione 2,0-3,0 (esclusivo).</span><span class="sxs-lookup"><span data-stu-id="e79dc-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="e79dc-134">L' `allowedVersions` attributo accetta valori usando il [formato dell'intervallo di versioni](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="e79dc-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="e79dc-135">Si noti che in 1,4, il blocco di un pacchetto in un intervallo di versioni specifico deve essere modificato manualmente.</span><span class="sxs-lookup"><span data-stu-id="e79dc-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="e79dc-136">In NuGet 1,5 si prevede di aggiungere il supporto per l'inserimento di questo intervallo tramite il `Install-Package` comando.</span><span class="sxs-lookup"><span data-stu-id="e79dc-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="e79dc-137">Visualizzatore pacchetti</span><span class="sxs-lookup"><span data-stu-id="e79dc-137">Package Visualizer</span></span>
<span data-ttu-id="e79dc-138">Il nuovo Visualizzatore di pacchetti, avviato tramite l'opzione di menu **strumenti**  ->  **libreria pacchetti di gestione pacchetti**  ->   , consente di visualizzare facilmente tutti i progetti e le relative dipendenze di pacchetto all'interno di una soluzione.</span><span class="sxs-lookup"><span data-stu-id="e79dc-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="e79dc-139">_**Nota importante:** Questa funzionalità sfrutta i vantaggi del supporto di DGML in Visual Studio. La creazione della visualizzazione è supportata solo in Visual Studio Ultimate. La visualizzazione di un diagramma DGML è supportata solo in Visual Studio Premium o versione successiva._</span><span class="sxs-lookup"><span data-stu-id="e79dc-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Visualizzatore pacchetti](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="e79dc-141">Controllo automatico degli aggiornamenti per la finestra di dialogo NuGet</span><span class="sxs-lookup"><span data-stu-id="e79dc-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="e79dc-142">Alcune versioni di NuGet introducono nuove funzionalità espresse tramite il `.nuspec` file che non sono riconosciute dalle versioni precedenti della finestra di dialogo NuGet.</span><span class="sxs-lookup"><span data-stu-id="e79dc-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="e79dc-143">Un esempio è l'introduzione in NuGet 1,4 per [specificare gli assembly del Framework](../release-notes/nuget-1.2.md#framework-assembly-refs).</span><span class="sxs-lookup"><span data-stu-id="e79dc-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="e79dc-144">Per questo motivo, è importante usare la versione più recente di NuGet per assicurarsi che sia possibile usare i pacchetti sfruttando le funzionalità più recenti.</span><span class="sxs-lookup"><span data-stu-id="e79dc-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="e79dc-145">Per rendere più visibili gli aggiornamenti a NuGet, la finestra di dialogo NuGet contiene la logica da evidenziare quando è disponibile una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="e79dc-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="e79dc-146">_**Nota**: il controllo viene eseguito solo se la scheda **online** è stata selezionata nella sessione corrente._</span><span class="sxs-lookup"><span data-stu-id="e79dc-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Finestra di dialogo Gestisci pacchetti NuGet con la nuova versione disponibile](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="e79dc-148">Per disattivare la verifica automatica degli aggiornamenti, passare alla finestra di dialogo Impostazioni NuGet e deselezionare **Controlla automaticamente la disponibilità di aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="e79dc-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Impostazioni NuGet](./media/nuget-settings.png)

<span data-ttu-id="e79dc-150">Questa funzionalità è stata effettivamente aggiunta in NuGet 1,3, ma non è naturalmente visibile fino a quando non viene reso disponibile un aggiornamento a 1,3, ad esempio NuGet 1,4.</span><span class="sxs-lookup"><span data-stu-id="e79dc-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="e79dc-151">Miglioramenti della finestra di dialogo Gestione pacchetti</span><span class="sxs-lookup"><span data-stu-id="e79dc-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="e79dc-152">**Nomi di menu migliorati**: le opzioni di menu per avviare la finestra di dialogo sono state rinominate per maggiore chiarezza.</span><span class="sxs-lookup"><span data-stu-id="e79dc-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="e79dc-153">L'opzione di menu ora **gestisce i pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e79dc-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="e79dc-154">**Riquadro dei dettagli Mostra la data di aggiornamento più recente**: la finestra di dialogo NuGet Visualizza la data dell'ultimo aggiornamento nel riquadro dei dettagli per un pacchetto quando è selezionata la scheda **online** o **aggiornamenti** .</span><span class="sxs-lookup"><span data-stu-id="e79dc-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="e79dc-155">**Elenco di tag visualizzati**: la finestra di dialogo NuGet Visualizza i tag.</span><span class="sxs-lookup"><span data-stu-id="e79dc-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="e79dc-156">Miglioramenti di PowerShell</span><span class="sxs-lookup"><span data-stu-id="e79dc-156">Powershell Improvements</span></span>
* <span data-ttu-id="e79dc-157">**Script di PowerShell firmati**: NuGet include script di PowerShell firmati che consentono l'utilizzo in ambienti più restrittivi.</span><span class="sxs-lookup"><span data-stu-id="e79dc-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="e79dc-158">**Richiesta di supporto**: la console di gestione pacchetti supporta ora la richiesta tramite `$host.ui.Prompt` i `$host.ui.PromptForChoice` comandi e.</span><span class="sxs-lookup"><span data-stu-id="e79dc-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="e79dc-159">**Nomi di origine del pacchetto**: specificare il nome di un'origine del pacchetto è supportato quando si specifica un'origine del pacchetto usando il `-Source` flag.</span><span class="sxs-lookup"><span data-stu-id="e79dc-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="e79dc-160">Miglioramenti della riga di comando nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e79dc-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="e79dc-161">**Comandi personalizzati NuGet**: nuget.exe è estendibile tramite comandi personalizzati mediante MEF.</span><span class="sxs-lookup"><span data-stu-id="e79dc-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="e79dc-162">**Più semplice è il flusso di lavoro per la creazione di pacchetti di simboli**: il `-Symbols` flag può essere applicato a una normale struttura di cartelle basata sulla convenzione creazione di un pacchetto di simboli includendo solo l'origine e i `.pdb` file all'interno della cartella.</span><span class="sxs-lookup"><span data-stu-id="e79dc-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="e79dc-163">**Specifica di più origini**: il `NuGet install` comando supporta la specifica di più origini usando i punti e virgola come delimitatore o specificando `-Source` più volte.</span><span class="sxs-lookup"><span data-stu-id="e79dc-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="e79dc-164">**Supporto per l'autenticazione proxy**: NuGet 1,4 aggiunge il supporto per la richiesta di credenziali utente quando si usa NuGet dietro un proxy che richiede l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e79dc-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="e79dc-165">**Modifica di rilievonuget.exe aggiornamento**: il `-Self` flag è ora necessario per nuget.exe aggiornare se stesso.</span><span class="sxs-lookup"><span data-stu-id="e79dc-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="e79dc-166">`nuget.exe Update` ora accetta un percorso del `packages.config` file e tenterà di aggiornare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="e79dc-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="e79dc-167">Si noti che questo aggiornamento è limitato in quanto non sarà: \* \* aggiornare, aggiungere e rimuovere contenuto nel file di progetto.</span><span class="sxs-lookup"><span data-stu-id="e79dc-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="e79dc-168">\* \* Eseguire script di PowerShell all'interno del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e79dc-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="e79dc-169">Supporto del server NuGet per il push di pacchetti con nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e79dc-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="e79dc-170">NuGet include un modo semplice per ospitare un [repository NuGet leggero basato su Web](../hosting-packages/nuget-server.md) tramite il `NuGet.Server` pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="e79dc-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="e79dc-171">Con NuGet 1,4, il server Lightweight supporta il push e l'eliminazione di pacchetti con nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="e79dc-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="e79dc-172">La versione più recente di `NuGet.Server` aggiunge un nuovo oggetto `appSetting` denominato `apiKey` .</span><span class="sxs-lookup"><span data-stu-id="e79dc-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="e79dc-173">Quando la chiave viene omessa o lascia vuota, il push dei pacchetti nel feed è disabilitato.</span><span class="sxs-lookup"><span data-stu-id="e79dc-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="e79dc-174">L'impostazione di apiKey su un valore (idealmente una password complessa) consente di eseguire il push dei pacchetti utilizzando nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="e79dc-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="e79dc-175">Supporto per Windows Phone Tools Mango Edition</span><span class="sxs-lookup"><span data-stu-id="e79dc-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="e79dc-176">NuGet è ora supportato nella versione finale candidata di Windows Phone Tools per mango.</span><span class="sxs-lookup"><span data-stu-id="e79dc-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="e79dc-177">Attualmente, Windows Phone strumenti non dispone del supporto per Gestione estensioni di Visual Studio, pertanto per installare NuGet per gli strumenti di Windows Phone, potrebbe essere necessario scaricare ed eseguire il progetto VSIX manualmente.</span><span class="sxs-lookup"><span data-stu-id="e79dc-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="e79dc-178">Per disinstallare NuGet per gli strumenti di Windows Phone, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="e79dc-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="e79dc-179">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="e79dc-179">Bug Fixes</span></span>
<span data-ttu-id="e79dc-180">NuGet 1,4 aveva un totale di 88 elementi di lavoro corretti.</span><span class="sxs-lookup"><span data-stu-id="e79dc-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="e79dc-181">71 di questi sono stati contrassegnati come bug.</span><span class="sxs-lookup"><span data-stu-id="e79dc-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="e79dc-182">Per un elenco completo degli elementi di lavoro corretti in NuGet 1,4, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e79dc-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="e79dc-183">Correzioni di bug degni di Nota:</span><span class="sxs-lookup"><span data-stu-id="e79dc-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="e79dc-184">[Problema 603](http://nuget.codeplex.com/workitem/603): le dipendenze del pacchetto tra repository diversi vengono risolte correttamente quando si specifica un'origine del pacchetto specifica.</span><span class="sxs-lookup"><span data-stu-id="e79dc-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="e79dc-185">[Problema 1036](http://nuget.codeplex.com/workitem/1036): `NuGet Pack SomeProject.csproj` l'aggiunta a un evento di post-compilazione non causa più un ciclo infinito.</span><span class="sxs-lookup"><span data-stu-id="e79dc-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="e79dc-186">[Problema 961](http://nuget.codeplex.com/workitem/961): il `-Source` flag supporta percorsi relativi.</span><span class="sxs-lookup"><span data-stu-id="e79dc-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="e79dc-187">Aggiornamento di NuGet 1,4</span><span class="sxs-lookup"><span data-stu-id="e79dc-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="e79dc-188">Poco dopo il rilascio di NuGet 1,4, sono stati rilevati alcuni problemi importanti da risolvere.</span><span class="sxs-lookup"><span data-stu-id="e79dc-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="e79dc-189">Il numero di versione specifico di questo aggiornamento 1,4 è 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="e79dc-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="e79dc-190">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="e79dc-190">Bug Fixes</span></span>
* <span data-ttu-id="e79dc-191">[Problema 1220](http://nuget.codeplex.com/workitem/1220): Update-Package non viene eseguito `install.ps1` / `uninstall.ps1` in tutti i progetti quando è presente più di un progetto</span><span class="sxs-lookup"><span data-stu-id="e79dc-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="e79dc-192">[Problema 1156](http://nuget.codeplex.com/workitem/1156): la console di gestione pacchetti è bloccata in W2K3/XP (se PowerShell 2 non è installato)</span><span class="sxs-lookup"><span data-stu-id="e79dc-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
