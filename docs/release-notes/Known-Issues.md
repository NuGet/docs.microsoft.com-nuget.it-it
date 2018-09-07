---
title: Problemi noti
description: Problemi noti con NuGet inclusi autenticazione, installazione dei pacchetti e strumenti.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fc338ba3810a125f638a937cf14456bf519a24a8
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548474"
---
# <a name="known-issues-with-nuget"></a><span data-ttu-id="19821-103">Problemi noti con NuGet</span><span class="sxs-lookup"><span data-stu-id="19821-103">Known Issues with NuGet</span></span>

<span data-ttu-id="19821-104">Questi sono i problemi noti più comuni relativi a NuGet segnalati ripetutamente.</span><span class="sxs-lookup"><span data-stu-id="19821-104">These are the most common known issues with NuGet that are repeatedly reported.</span></span> <span data-ttu-id="19821-105">In caso di problemi con l'installazione di NuGet o la gestione dei pacchetti, esaminare questi problemi noti e le relative soluzioni.</span><span class="sxs-lookup"><span data-stu-id="19821-105">If you are having trouble installing NuGet or managing packages, please take a look through these known issues and their resolutions.</span></span>

> [!Note]
> <span data-ttu-id="19821-106">A partire da NuGet 4.0, i problemi noti fanno parte delle note sulla versione corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="19821-106">Starting with NuGet 4.0, known issues are a part of the respective release notes.</span></span>

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a><span data-ttu-id="19821-107">Problemi di autenticazione con i feed NuGet in VSTS con nuget.exe v3.4.3</span><span class="sxs-lookup"><span data-stu-id="19821-107">Authentication issues with NuGet feeds in VSTS with nuget.exe v3.4.3</span></span>

<span data-ttu-id="19821-108">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="19821-108">**Problem:**</span></span>

<span data-ttu-id="19821-109">Quando si usa il comando seguente per archiviare le credenziali, il risultato è la doppia crittografia del token di accesso personale.</span><span class="sxs-lookup"><span data-stu-id="19821-109">When we use the following command to store the credentials, we end up double encrypting the Personal Access Token.</span></span>

<span data-ttu-id="19821-110">$PAT = "token di accesso personale" $Feed = "URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span><span class="sxs-lookup"><span data-stu-id="19821-110">$PAT = "Your personal access token" $Feed = "Your url" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT</span></span>

<span data-ttu-id="19821-111">**Soluzione alternativa:**</span><span class="sxs-lookup"><span data-stu-id="19821-111">**Workaround:**</span></span>

<span data-ttu-id="19821-112">Archiviare le password in testo non crittografato usando l'opzione [-StorePasswordInClearText](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="19821-112">Store passwords in clear text using the [-StorePasswordInClearText](../tools/cli-ref-sources.md) option.</span></span>

## <a name="error-installing-packages-with-nuget-34-341"></a><span data-ttu-id="19821-113">Errore durante l'installazione di pacchetti con NuGet 3.4, 3.4.1</span><span class="sxs-lookup"><span data-stu-id="19821-113">Error installing packages with NuGet 3.4, 3.4.1</span></span>

<span data-ttu-id="19821-114">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="19821-114">**Problem:**</span></span>

<span data-ttu-id="19821-115">In NuGet 3.4 e 3.4.1, quando si usa il componente aggiuntivo di NuGet, le origini non vengono segnalate come disponibili e non è possibile aggiungere nuove origini nella finestra di configurazione.</span><span class="sxs-lookup"><span data-stu-id="19821-115">In NuGet 3.4 and 3.4.1, when using the NuGet add-in, no sources are reported as available and you are unable to add new sources in the configuration window.</span></span> <span data-ttu-id="19821-116">Il risultato è simile all'immagine riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="19821-116">The result is similar to the image below:</span></span>

![Configurazione di NuGet senza origini](./media/knownIssue-34-NoSources.PNG)

<span data-ttu-id="19821-118">Il file `NuGet.Config` nella cartella `%AppData%\NuGet\` (Windows) o `~/.nuget/` (Mac/Linux) è stato svuotato accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="19821-118">The `NuGet.Config` file in your `%AppData%\NuGet\` (Windows) or `~/.nuget/` (Mac/Linux) folder has accidentally been emptied.</span></span> <span data-ttu-id="19821-119">Per correggere l'errore: chiudere Visual Studio (in Windows, se applicabile), eliminare il file `NuGet.Config` e ripetere l'operazione.</span><span class="sxs-lookup"><span data-stu-id="19821-119">To fix this: close Visual Studio (on Windows, if applicable), delete the `NuGet.Config` file, and try the operation again.</span></span> <span data-ttu-id="19821-120">NuGet ha generato un nuovo `NuGet.Config` e dovrebbe essere possibile procedere.</span><span class="sxs-lookup"><span data-stu-id="19821-120">NuGet generated a new `NuGet.Config` and you should be able to proceed.</span></span>

## <a name="error-installing-packages-with-nuget-27"></a><span data-ttu-id="19821-121">Errore durante l'installazione di pacchetti con NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="19821-121">Error installing packages with NuGet 2.7</span></span>

<span data-ttu-id="19821-122">**Problema:**</span><span class="sxs-lookup"><span data-stu-id="19821-122">**Problem:**</span></span>

<span data-ttu-id="19821-123">In NuGet 2.7 o versione successiva, quando si tenta di installare qualsiasi pacchetto che contiene riferimenti ad assembly, è possibile che venga visualizzato il messaggio di errore **"Formato della stringa di input non corretto."**, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="19821-123">In NuGet 2.7 or above, when you attempt to install any package which contains assembly references, you may receive the error message **"Input string was not in a correct format."**, like below:</span></span>

```ps
install-package log4net
    Installing 'log4net 2.0.0'.
    Successfully installed 'log4net 2.0.0'.
    Adding 'log4net 2.0.0' to Tyson.OperatorUpload.
    Install failed. Rolling back...
    install-package : Input string was not in a correct format.
    At line:1 char:1
        install-package log4net
        ~~~~~~~~~~~~~~~~~~~~~~~
        CategoryInfo : NotSpecified: (:) [Install-Package], FormatException
        FullyQualifiedErrorId : NuGetCmdletUnhandledException,NuGet.PowerShell.Commands.InstallPackageCommand
```

<span data-ttu-id="19821-124">La causa è l'annullamento della registrazione della libreria dei tipi per il componente COM `VSLangProj.dll` nel sistema.</span><span class="sxs-lookup"><span data-stu-id="19821-124">This is caused by the type library for the `VSLangProj.dll` COM component being unregistered on your system.</span></span> <span data-ttu-id="19821-125">Questa situazione può verificarsi, ad esempio, quando sono disponibili due versioni di Visual Studio installate side-by-side e si disinstalla la versione meno recente.</span><span class="sxs-lookup"><span data-stu-id="19821-125">This can happen, for example, when you have two versions of Visual Studio installed side-by-side and you then uninstall the older version.</span></span> <span data-ttu-id="19821-126">Ciò può causare inavvertitamente l'annullamento della registrazione della libreria COM sopra indicata.</span><span class="sxs-lookup"><span data-stu-id="19821-126">Doing so may inadvertently unregister the above COM library.</span></span>

<span data-ttu-id="19821-127">**Soluzione:**</span><span class="sxs-lookup"><span data-stu-id="19821-127">**Solution:**:</span></span>

<span data-ttu-id="19821-128">Eseguire questo comando da un **prompt dei comandi con privilegi elevati** per registrare di nuovo la libreria dei tipi per `VSLangProj.dll`.</span><span class="sxs-lookup"><span data-stu-id="19821-128">Run this command from an **elevated prompt** to re-register the type library for `VSLangProj.dll`</span></span>

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

<span data-ttu-id="19821-129">Se il comando non riesce, verificare l'esistenza del file in tale percorso.</span><span class="sxs-lookup"><span data-stu-id="19821-129">If the command fails, check to see if the file exists in that location.</span></span>

<span data-ttu-id="19821-130">Per altre informazioni su questo errore, vedere questo [elemento di lavoro](https://nuget.codeplex.com/workitem/3609 "Elemento di lavoro 3609").</span><span class="sxs-lookup"><span data-stu-id="19821-130">For more information about this error, see this [work item](https://nuget.codeplex.com/workitem/3609 "Work item 3609").</span></span>

## <a name="build-failure-after-package-update-in-vs-2012"></a><span data-ttu-id="19821-131">Errore di compilazione dopo l'aggiornamento del pacchetto in Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="19821-131">Build failure after package update in VS 2012</span></span>

<span data-ttu-id="19821-132">Il problema: si usa Visual Studio 2012 RTM.</span><span class="sxs-lookup"><span data-stu-id="19821-132">The problem: You are using VS 2012 RTM.</span></span> <span data-ttu-id="19821-133">Quando si aggiornano i pacchetti NuGet, viene visualizzato il messaggio: "Non è stato possibile disinstallare completamente uno o più pacchetti."</span><span class="sxs-lookup"><span data-stu-id="19821-133">When updating NuGet packages, you get this message: "One or more packages could not be completed uninstalled."</span></span> <span data-ttu-id="19821-134">e viene richiesto di riavviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-134">and you are prompted to restart Visual Studio.</span></span> <span data-ttu-id="19821-135">Dopo il riavvio di Visual Studio, si verificano strani errori di compilazione.</span><span class="sxs-lookup"><span data-stu-id="19821-135">After VS restart, you get weird build errors.</span></span>

<span data-ttu-id="19821-136">La causa è che alcuni file nei pacchetti precedenti sono bloccati da un processo di MSBuild in background.</span><span class="sxs-lookup"><span data-stu-id="19821-136">The cause is that certain files in the old packages are locked by a background MSBuild process.</span></span> <span data-ttu-id="19821-137">Anche dopo il riavvio di Visual Studio, il processo di MSBuild in background usa ancora i file nei pacchetti precedenti, causando gli errori di compilazione.</span><span class="sxs-lookup"><span data-stu-id="19821-137">Even after VS restart, the background MSBuild process still uses the files in the old packages, causing the build failures.</span></span>

<span data-ttu-id="19821-138">La correzione consiste nell'installare Visual Studio 2012 Update, ad esempio Visual Studio 2012 Update 2.</span><span class="sxs-lookup"><span data-stu-id="19821-138">The fix is to install VS 2012 Update, e.g. VS 2012 Update 2.</span></span>

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a><span data-ttu-id="19821-139">L'aggiornamento da una versione precedente alla versione più recente di NuGet causa un errore di verifica della firma</span><span class="sxs-lookup"><span data-stu-id="19821-139">Upgrading to latest NuGet from an older version causes a signature verification error</span></span>

<span data-ttu-id="19821-140">Se si esegue Visual Studio 2010 SP1, potrebbe essere visualizzato il messaggio di errore seguente durante il tentativo di aggiornare NuGet, se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="19821-140">If you are running VS 2010 SP1, you might run into the following error message when attempting to upgrade NuGet if you have an older version installed.</span></span>

![Programma di installazione dell'estensione di Visual Studio](./media/Visual-Studio-Extension-Installer.png)

<span data-ttu-id="19821-142">Quando si visualizzano i log, potrebbe essere menzionata una `SignatureMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="19821-142">When viewing the logs, you might see a mention of a `SignatureMismatchException`.</span></span>

<span data-ttu-id="19821-143">Per evitare che ciò accada, è disponibile un [hotfix di Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) che è possibile installare.</span><span class="sxs-lookup"><span data-stu-id="19821-143">To prevent this from occurring, there is a [Visual Studio 2010 SP1 hotfix](http://bit.ly/vsixcertfix) you can install.</span></span>
<span data-ttu-id="19821-144">In alternativa, per risolvere il problema è sufficiente disinstallare NuGet (eseguendo Visual Studio come amministratore) e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-144">Alternatively, the workaround is to simply uninstall NuGet (while running Visual Studio as Administrator) and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="19821-145">Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="19821-145">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a><span data-ttu-id="19821-146">La console di Gestione pacchetti genera un'eccezione quando viene installato anche il componente aggiuntivo Reflector di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-146">Package Manager Console throws an exception when the Reflector Visual Studio Add-In is also installed.</span></span>

<span data-ttu-id="19821-147">Quando si esegue la console di Gestione pacchetti, è possibile che venga visualizzato il messaggio di eccezione seguente se è installato il componente aggiuntivo Reflector di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-147">When running the Package Manager console, you may run into the following exception message if you have the Reflector VS Add-in installed.</span></span>

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

<span data-ttu-id="19821-148">oppure</span><span class="sxs-lookup"><span data-stu-id="19821-148">or</span></span>

    System.Management.Automation.CmdletInvocationException: Could not load file or assembly 'Scripts\nuget.psm1' or one of its dependencies. <br />The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) ---&gt; System.IO.FileLoadException: Could not load file or <br />assembly 'Scripts\nuget.psm1' or one of its dependencies. The parameter is incorrect. (Exception from HRESULT: 0x80070057 (E_INVALIDARG)) <br />---&gt; System.ArgumentException: Illegal characters in path.
       at System.IO.Path.CheckInvalidPathChars(String path)
       at System.IO.Path.Combine(String path1, String path2)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.<AssemblyPaths>d__1.MoveNext()
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.InnerResolveHandler(String name)
       at Microsoft.VisualStudio.Platform.VsAppDomainManager.ResolveHandler(Object sender, ResolveEventArgs args)
       at System.AppDomain.OnAssemblyResolveEvent(RuntimeAssembly assembly, String assemblyFullName)
       --- End of inner exception stack trace ---
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadBinaryModule(Boolean trySnapInName, String moduleName, String fileName, <br />Assembly assemblyToLoad, String moduleBase, SessionState ss, String prefix, Boolean loadTypes, Boolean loadFormats, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleNamedInManifest(String moduleName, String moduleBase, <br />Boolean searchModulePath, <br />String prefix, SessionState ss, Boolean loadTypesFiles, Boolean loadFormatFiles, Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModuleManifest(ExternalScriptInfo scriptInfo, ManifestProcessingFlags <br />manifestProcessingFlags, Version version)
       at Microsoft.PowerShell.Commands.ModuleCmdletBase.LoadModule(String fileName, String moduleBase, String prefix, SessionState ss, <br />Boolean&amp; found)
       at Microsoft.PowerShell.Commands.ImportModuleCommand.ProcessRecord()
       at System.Management.Automation.Cmdlet.DoProcessRecord()
       at System.Management.Automation.CommandProcessor.ProcessRecord()
       --- End of inner exception stack trace ---
       at System.Management.Automation.Runspaces.PipelineBase.Invoke(IEnumerable input)
       at System.Management.Automation.Runspaces.Pipeline.Invoke()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Invoke(String command, Object input, Boolean outputResults)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHostExtensions.ImportModule(PowerShellHost host, String modulePath)
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.LoadStartupScripts()
       at NuGetConsole.Host.PowerShell.Implementation.PowerShellHost.Initialize()
       at NuGetConsole.Implementation.Console.ConsoleDispatcher.Start()
       at NuGetConsole.Implementation.PowerConsoleToolWindow.MoveFocus(FrameworkElement consolePane)

<span data-ttu-id="19821-149">È stato contattato l'autore del componente aggiuntivo nella speranza di trovare una soluzione.</span><span class="sxs-lookup"><span data-stu-id="19821-149">We've contacted the author of the add-in in the hopes of working out a resolution.</span></span>

<p class="info"><span data-ttu-id="19821-150">Aggiornamento: è stato verificato che la versione più recente di Reflector, 6.5, non causa questa eccezione nella console.</span><span class="sxs-lookup"><span data-stu-id="19821-150">Update: We have verified that the latest version of Reflector, 6.5, no longer causes this exception in the console.</span></span></p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a><span data-ttu-id="19821-151">Errore di apertura della console di Gestione pacchetti con eccezione ObjectSecurity</span><span class="sxs-lookup"><span data-stu-id="19821-151">Opening Package Manager Console fails with ObjectSecurity exception</span></span>

<span data-ttu-id="19821-152">Si potrebbero verificare questi errori quando si tenta di aprire la console di Gestione pacchetti:</span><span class="sxs-lookup"><span data-stu-id="19821-152">You might see these errors when trying to open the Package Manager Console:</span></span>

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

<span data-ttu-id="19821-153">In questo caso, seguire la soluzione [descritta su StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) per correggerli.</span><span class="sxs-lookup"><span data-stu-id="19821-153">If so, follow the solution [discussed on StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) to fix them.</span></span>

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a><span data-ttu-id="19821-154">La finestra di dialogo per l'aggiunta di un riferimento alla libreria di pacchetti genera un'eccezione se la soluzione contiene un progetto InstallShield Limited Edition.</span><span class="sxs-lookup"><span data-stu-id="19821-154">The Add Package Library Reference dialog throws an exception if the solution contains InstallShield Limited Edition Project</span></span>

<span data-ttu-id="19821-155">È stato scoperto che se la soluzione contiene uno o più progetti InstallShield Limited Edition, la finestra di dialogo per **l'aggiunta di un riferimento alla libreria di pacchetti**genera un'eccezione all'apertura.</span><span class="sxs-lookup"><span data-stu-id="19821-155">We have identified that if your solution contains one or more InstallShield Limited Edition project, the **Add Package Library Reference** dialog will throw an exception when opened.</span></span> <span data-ttu-id="19821-156">Non esiste attualmente alcuna soluzione, se non rimuovere o scaricare i progetti InstallShield.</span><span class="sxs-lookup"><span data-stu-id="19821-156">There is currently no workaround yet except either removing InstallShield projects or unloading them.</span></span>

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a><span data-ttu-id="19821-157">Pulsante Disinstalla disabilitato?</span><span class="sxs-lookup"><span data-stu-id="19821-157">Uninstall Button Greyed out?</span></span> <span data-ttu-id="19821-158">Per l'installazione o la disinstallazione NuGet richiede privilegi di amministratore</span><span class="sxs-lookup"><span data-stu-id="19821-158">NuGet Requires Admin Privileges to Install/Uninstall</span></span>

<span data-ttu-id="19821-159">Se si tenta di disinstallare NuGet tramite Gestione estensioni di Visual Studio, il pulsante Disinstalla potrebbe risultare disabilitato.</span><span class="sxs-lookup"><span data-stu-id="19821-159">If you try to uninstall NuGet via the Visual Studio Extension Manager, you may notice that the Uninstall button is disabled.</span></span> <span data-ttu-id="19821-160">Per l'installazione o la disinstallazione NuGet richiede l'accesso con privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="19821-160">NuGet requires admin access to install and uninstall.</span></span> <span data-ttu-id="19821-161">Riavviare Visual Studio come amministratore per disinstallare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="19821-161">Relaunch Visual Studio as an administrator to uninstall the extension.</span></span> <span data-ttu-id="19821-162">NuGet non richiede l'accesso con privilegi di amministratore per l'uso.</span><span class="sxs-lookup"><span data-stu-id="19821-162">NuGet does not require admin access to use it.</span></span>

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a><span data-ttu-id="19821-163">Arresto anomalo della console di gestione pacchetti quando viene aperta in Windows XP.</span><span class="sxs-lookup"><span data-stu-id="19821-163">The Package Manager Console crashes when I open it in Windows XP.</span></span> <span data-ttu-id="19821-164">Qual è il problema?</span><span class="sxs-lookup"><span data-stu-id="19821-164">What's wrong?</span></span>

<span data-ttu-id="19821-165">NuGet richiede il runtime di PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="19821-165">NuGet requires Powershell 2.0 runtime.</span></span> <span data-ttu-id="19821-166">Windows XP, per impostazione predefinita, non include PowerShell 2.0.</span><span class="sxs-lookup"><span data-stu-id="19821-166">Windows XP, by default, doesn't have Powershell 2.0.</span></span> <span data-ttu-id="19821-167">È possibile scaricare il runtime di PowerShell 2.0 da [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span><span class="sxs-lookup"><span data-stu-id="19821-167">You can download the Powershell 2.0 runtime from [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929).</span></span> <span data-ttu-id="19821-168">Dopo l'installazione, riavviare Visual Studio. Dovrebbe essere possibile aprire la console di Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="19821-168">After you install it, restart Visual Studio and you should be able to open Package Manager Console.</span></span>

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a><span data-ttu-id="19821-169">Arresto anomalo di Visual Studio 2010 SP1 Beta in uscita se la console di Gestione pacchetti è aperta.</span><span class="sxs-lookup"><span data-stu-id="19821-169">Visual Studio 2010 SP1 Beta crashes on exit if the Package Manager Console is open.</span></span>

<span data-ttu-id="19821-170">Se è installato Visual Studio 2010 SP1 Beta, potrebbe verificarsi un arresto anomalo se si lascia aperta la console di Gestione pacchetti e si chiude Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-170">If you have installed Visual Studio 2010 SP1 Beta, you may notice that if you leave the Package Manager Console open and close Visual Studio, it will crash.</span></span> <span data-ttu-id="19821-171">Si tratta di un problema noto di Visual Studio e verrà risolto nella versione SP1 RTM.</span><span class="sxs-lookup"><span data-stu-id="19821-171">This is a known issue of Visual Studio and will be fixed in SP1 RTM release.</span></span> <span data-ttu-id="19821-172">Per il momento, ignorare l'arresto anomalo o disinstallare la versione SP1 Beta, se possibile.</span><span class="sxs-lookup"><span data-stu-id="19821-172">For now, just ignore the crash or uninstall SP1 Beta if you can.</span></span>

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a><span data-ttu-id="19821-173">Si verifica l'eccezione "L'elemento 'metadata' contiene un elemento figlio non valido"</span><span class="sxs-lookup"><span data-stu-id="19821-173">The element 'metadata' ... has invalid child element exception occurs</span></span>

<span data-ttu-id="19821-174">Se si installano pacchetti compilati con una versione non definitiva di NuGet, potrebbe essere visualizzato un messaggio di errore "L'elemento 'metadata' contiene un elemento figlio non valido nello spazio dei nomi 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd'" quando si esegue la versione RTM di NuGet con tale progetto.</span><span class="sxs-lookup"><span data-stu-id="19821-174">If you installed packages built with a pre-release version of NuGet, you might encounter an error message stating "The element 'metadata' in namespace 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd' has invalid child element" when running the RTM version of NuGet with that project.</span></span> <span data-ttu-id="19821-175">È necessario disinstallare e reinstallare ogni pacchetto usando la versione RTM di NuGet.</span><span class="sxs-lookup"><span data-stu-id="19821-175">You need to uninstall and then re-install each package using the RTM version of NuGet.</span></span>

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-exists"></a><span data-ttu-id="19821-176">Qualsiasi tentativo di eseguire un'installazione o una disinstallazione genera l'errore "Impossibile creare un file, se il file esiste già."</span><span class="sxs-lookup"><span data-stu-id="19821-176">Attempting to install or uninstall results in the error "Cannot create a file when that file already exists."</span></span>

<span data-ttu-id="19821-177">Per qualche motivo, le estensioni di Visual Studio possono trovarsi in uno stato strano, in cui viene disinstallata l'estensione VSIX ma rimangono alcuni file.</span><span class="sxs-lookup"><span data-stu-id="19821-177">For some reason, Visual Studio extensions can get in a weird state where you've uninstalled the VSIX extension, but some files were left behind.</span></span> <span data-ttu-id="19821-178">Per risolvere questo problema:</span><span class="sxs-lookup"><span data-stu-id="19821-178">To work around this issue:</span></span>

1. <span data-ttu-id="19821-179">Chiudi Visual Studio</span><span class="sxs-lookup"><span data-stu-id="19821-179">Exit Visual Studio</span></span>
1. <span data-ttu-id="19821-180">Aprire la cartella seguente (potrebbe essere in un'unità diversa nel computer in uso)</span><span class="sxs-lookup"><span data-stu-id="19821-180">Open the following folder (it might be on a different drive on your machine)</span></span>

    <span data-ttu-id="19821-181">C:\Programmi (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<versione>\\</span><span class="sxs-lookup"><span data-stu-id="19821-181">C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<version>\\</span></span>

1. <span data-ttu-id="19821-182">Eliminare tutti i file con estensione *.deleteme*.</span><span class="sxs-lookup"><span data-stu-id="19821-182">Delete all the files with the *.deleteme* extensions.</span></span>
1. <span data-ttu-id="19821-183">Riaprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-183">Re-open Visual Studio</span></span>

<span data-ttu-id="19821-184">Dopo aver completato questi passaggi, dovrebbe essere possibile continuare.</span><span class="sxs-lookup"><span data-stu-id="19821-184">After following these steps, you should be able to continue.</span></span>

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a><span data-ttu-id="19821-185">In rari casi, la compilazione con Analisi codice attivata causa un errore.</span><span class="sxs-lookup"><span data-stu-id="19821-185">In rare cases, compiling with Code Analysis turned on causes error.</span></span>

<span data-ttu-id="19821-186">Potrebbe essere visualizzato l'errore seguente se si installa FluentNHibernate con la console di Gestione pacchetti e quindi si compila il progetto con la funzionalità "Analisi codice" attivata.</span><span class="sxs-lookup"><span data-stu-id="19821-186">You might get the following error if you installs FluentNHibernate with the Package Manager console and then compile your project with "Code Analysis" turned on.</span></span>

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

<span data-ttu-id="19821-187">Per impostazione predefinita, FluentNHibernate richiede NHibernate 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="19821-187">By default, FluentNHibernate requires NHibernate 3.0.0.2001.</span></span> <span data-ttu-id="19821-188">Tuttavia, in base alla progettazione NuGet installerà NHibernate 3.0.0.4000 nel progetto e aggiungerà i reindirizzamenti di binding appropriati per consentirne il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="19821-188">However, by design NuGet will install NHibernate 3.0.0.4000 in your project and add the appropriate binding redirects so that it will work.</span></span> <span data-ttu-id="19821-189">Il progetto verrà compilato correttamente anche se l'analisi codice non è attivata.</span><span class="sxs-lookup"><span data-stu-id="19821-189">You project will compile just fine if code analysis is not turned on.</span></span> <span data-ttu-id="19821-190">A differenza del compilatore, lo strumento di analisi codice non segue correttamente i reindirizzamenti di binding per usare la versione 3.0.0.4000 anziché 3.0.0.2001.</span><span class="sxs-lookup"><span data-stu-id="19821-190">In contrast to the compiler, code analysis tool doesn't properly follow the binding redirects to use 3.0.0.4000 instead of 3.0.0.2001.</span></span> <span data-ttu-id="19821-191">È possibile risolvere il problema installando NHibernate 3.0.0.2001 oppure indicare allo strumento di analisi codice di adottare lo stesso comportamento del compilatore, seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="19821-191">You can work around the issue by either installing NHibernate 3.0.0.2001 or tell the code analysis tool to behave the same as the compiler by doing the following:</span></span>

1. <span data-ttu-id="19821-192">Passare a *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span><span class="sxs-lookup"><span data-stu-id="19821-192">Go to *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*</span></span>
1. <span data-ttu-id="19821-193">Aprire FxCopCmd.exe.config e modificare `AssemblyReferenceResolveMode` da `StrongName` a `StrongNameIgnoringVersion`.</span><span class="sxs-lookup"><span data-stu-id="19821-193">Open FxCopCmd.exe.config and change `AssemblyReferenceResolveMode` from `StrongName` to `StrongNameIgnoringVersion`.</span></span>
1. <span data-ttu-id="19821-194">Salvare le modifiche e ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="19821-194">Save the change and rebuild your project.</span></span>

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a><span data-ttu-id="19821-195">Il comando Write-Error non funziona all'interno di install.ps1/uninstall.ps1/init.ps1</span><span class="sxs-lookup"><span data-stu-id="19821-195">Write-Error command doesn't work inside install.ps1/uninstall.ps1/init.ps1</span></span>

<span data-ttu-id="19821-196">Si tratta di un problema noto.</span><span class="sxs-lookup"><span data-stu-id="19821-196">This is a known issue.</span></span> <span data-ttu-id="19821-197">Anziché chiamare Write-Error, provare a chiamare throw.</span><span class="sxs-lookup"><span data-stu-id="19821-197">Instead of calling Write-Error, try calling throw.</span></span>

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a><span data-ttu-id="19821-198">L'installazione di NuGet con accesso limitato in Windows 2003 può causare l'arresto anomalo di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="19821-198">Installing NuGet with restricted access on Windows 2003 can crash Visual Studio</span></span>

<span data-ttu-id="19821-199">Quando si tenta di installare NuGet tramite Gestione estensioni di Visual Studio senza diritti di amministratore, viene visualizzata la finestra di dialogo &#8220;Esegui come&#8221; con la casella di controllo &#8220;Esegui il programma con accesso limitato&#8221; selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="19821-199">When attempting to install NuGet using the Visual Studio Extension Manager and not running as an administrator, the &#8220;Run As&#8221; dialog is displayed with the checkbox labeled &#8220;Run this program with restricted access&#8221; checked by default.</span></span>

![Finestra di dialogo Esegui come con restrizioni](./media/RunAsRestricted.png)

<span data-ttu-id="19821-201">Se si fa clic su OK con tale casella di controllo selezionata si verifica un arresto anomalo di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-201">Clicking OK with that checked crashes Visual Studio.</span></span> <span data-ttu-id="19821-202">Assicurarsi di deselezionare l'opzione prima di installare NuGet.</span><span class="sxs-lookup"><span data-stu-id="19821-202">Make sure to uncheck that option before installing NuGet.</span></span>

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a><span data-ttu-id="19821-203">Non è possibile disinstallare NuGet per Strumenti di Windows Phone</span><span class="sxs-lookup"><span data-stu-id="19821-203">Cannot uninstall NuGet for Windows Phone Tools</span></span>

<span data-ttu-id="19821-204">Strumenti di Windows Phone non include il supporto per Gestione estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="19821-204">Windows Phone Tools does not have support for the Visual Studio Extension Manager.</span></span> <span data-ttu-id="19821-205">Per disinstallare NuGet, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="19821-205">In order to uninstall NuGet, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a><span data-ttu-id="19821-206">La modifica della combinazione di maiuscole/minuscole degli ID di pacchetto NuGet causa errori durante il ripristino del pacchetto</span><span class="sxs-lookup"><span data-stu-id="19821-206">Changing the capitalization of NuGet package IDs breaks package restore</span></span>

<span data-ttu-id="19821-207">Come descritto in dettaglio in [questo problema su GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), la modifica della combinazione di maiuscole/minuscole dei pacchetti NuGet può essere effettuata dal supporto NuGet, ma causa complicazioni durante il ripristino del pacchetto per gli utenti con pacchetti esistenti, con diversa combinazione di maiuscole/minuscole, nella cartella *global-packages*.</span><span class="sxs-lookup"><span data-stu-id="19821-207">As discussed at length on [this GitHub issue](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), changing the capitalization of NuGet packages can be done by NuGet support, but causes complications during package restore for users who have existing, differently-cased, packages in their *global-packages* folder.</span></span> <span data-ttu-id="19821-208">È consigliabile richiedere una modifica della combinazione di maiuscole/minuscole solo quando è possibile avvisare gli utenti esistenti del pacchetto dei problemi che potrebbero verificarsi durante il ripristino del pacchetto in fase di compilazione.</span><span class="sxs-lookup"><span data-stu-id="19821-208">We recommend only requesting a case change when you have a way to communicate with existing users of your package about the break that may occur to their build-time package restore.</span></span>

## <a name="reporting-issues"></a><span data-ttu-id="19821-209">Segnalazione di problemi</span><span class="sxs-lookup"><span data-stu-id="19821-209">Reporting issues</span></span>

<span data-ttu-id="19821-210">Per segnalare problemi NuGet, visitare [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="19821-210">To report NuGet issues, visit [https://github.com/nuget/home/issues](https://github.com/nuget/home/issues).</span></span>
