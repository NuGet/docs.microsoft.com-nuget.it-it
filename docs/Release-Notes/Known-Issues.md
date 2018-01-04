---
title: Problemi noti di NuGet | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 42e7a619-1c69-454b-8243-16e2f9f950d0
description: Problemi noti con NuGet inclusi autenticazione, installazione dei pacchetti e strumenti.
keywords: Problemi noti di NuGet, problemi di NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ce145212da3830216e123f39257a6707712f88c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="known-issues-with-nuget"></a>Problemi noti con NuGet

Questi sono i problemi noti più comuni relativi a NuGet segnalati ripetutamente. In caso di problemi con l'installazione di NuGet o la gestione dei pacchetti, esaminare questi problemi noti e le relative soluzioni.

> [!Note]
> A partire da NuGet 4.0, i problemi noti fanno parte delle note sulla versione corrispondenti.

## <a name="authentication-issues-with-nuget-feeds-in-vsts-with-nugetexe-v343"></a>Problemi di autenticazione con i feed NuGet in VSTS con nuget.exe v3.4.3

**Problema:**

Quando si usa il comando seguente per archiviare le credenziali, il risultato è la doppia crittografia del token di accesso personale.

$PAT = "token di accesso personale" $Feed = "URL" .\nuget.exe sources add -Name Test -Source $Feed -UserName $UserName -Password $PAT

**Soluzione alternativa:**

Archiviare le password in testo non crittografato usando l'opzione [-StorePasswordInClearText](../tools/cli-ref-sources.md).

## <a name="error-installing-packages-with-nuget-34-341"></a>Errore durante l'installazione di pacchetti con NuGet 3.4, 3.4.1

**Problema:**

In NuGet 3.4 e 3.4.1, quando si usa il componente aggiuntivo di NuGet, le origini non vengono segnalate come disponibili e non è possibile aggiungere nuove origini nella finestra di configurazione. Il risultato è simile all'immagine riportata di seguito:

![Configurazione di NuGet senza origini](./media/knownIssue-34-NoSources.PNG)

Il file `NuGet.Config` nella cartella `%AppData%\NuGet\` è stato svuotato accidentalmente. Per risolvere il problema: chiudere Visual Studio 2015, eliminare il file `NuGet.Config` nella cartella `%AppData%\NuGet\` e riavviare Visual Studio.  Verrà generato un nuovo file `NuGet.Config` e sarà possibile procedere.

## <a name="error-installing-packages-with-nuget-27"></a>Errore durante l'installazione di pacchetti con NuGet 2.7

**Problema:**

In NuGet 2.7 o versione successiva, quando si tenta di installare qualsiasi pacchetto che contiene riferimenti ad assembly, è possibile che venga visualizzato il messaggio di errore **"Formato della stringa di input non corretto."**, come di seguito:

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


La causa è l'annullamento della registrazione della libreria dei tipi per il componente COM `VSLangProj.dll` nel sistema. Questa situazione può verificarsi, ad esempio, quando sono disponibili due versioni di Visual Studio installate side-by-side e si disinstalla la versione meno recente. Ciò può causare inavvertitamente l'annullamento della registrazione della libreria COM sopra indicata.

**Soluzione:**

Eseguire questo comando da un **prompt dei comandi con privilegi elevati** per registrare di nuovo la libreria dei tipi per `VSLangProj.dll`.

    regsvr32 "C:\Program Files (x86)\Common Files\microsoft shared\MSEnv\VsLangproj.olb"

Se il comando non riesce, verificare l'esistenza del file in tale percorso.

Per altre informazioni su questo errore, vedere questo [elemento di lavoro](https://nuget.codeplex.com/workitem/3609 "Elemento di lavoro 3609").

## <a name="build-failure-after-package-update-in-vs-2012"></a>Errore di compilazione dopo l'aggiornamento del pacchetto in Visual Studio 2012
Il problema: si usa Visual Studio 2012 RTM. Quando si aggiornano i pacchetti NuGet, viene visualizzato il messaggio: "Non è stato possibile disinstallare completamente uno o più pacchetti." e viene richiesto di riavviare Visual Studio. Dopo il riavvio di Visual Studio, si verificano strani errori di compilazione.

La causa è che alcuni file nei pacchetti precedenti sono bloccati da un processo di MSBuild in background.
Anche dopo il riavvio di Visual Studio, il processo di MSBuild in background usa ancora i file nei pacchetti precedenti, causando gli errori di compilazione.

La correzione consiste nell'installare Visual Studio 2012 Update, ad esempio [Visual Studio 2012 Update 2](http://www.microsoft.com/download/details.aspx?id=38188).

## <a name="upgrading-to-latest-nuget-from-an-older-version-causes-a-signature-verification-error"></a>L'aggiornamento da una versione precedente alla versione più recente di NuGet causa un errore di verifica della firma

Se si esegue Visual Studio 2010 SP1, potrebbe essere visualizzato il messaggio di errore seguente durante il tentativo di aggiornare NuGet, se è installata una versione precedente.

![Programma di installazione dell'estensione di Visual Studio](./media/Visual-Studio-Extension-Installer.png)

Quando si visualizzano i log, potrebbe essere menzionata una `SignatureMismatchException`.

Per evitare che ciò accada, è disponibile un [hotfix di Visual Studio 2010 SP1](http://bit.ly/vsixcertfix) che è possibile installare.
In alternativa, per risolvere il problema è sufficiente disinstallare NuGet (eseguendo Visual Studio come amministratore) e quindi installarlo dalla raccolta di estensioni di Visual Studio.  Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).

## <a name="package-manager-console-throws-an-exception-when-the-reflector-visual-studio-add-in-is-also-installed"></a>La console di Gestione pacchetti genera un'eccezione quando viene installato anche il componente aggiuntivo Reflector di Visual Studio.

Quando si esegue la console di Gestione pacchetti, è possibile che venga visualizzato il messaggio di eccezione seguente se è installato il componente aggiuntivo Reflector di Visual Studio.

    The following error occurred while loading the extended type data file:
    Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2950) :
    Error in type "System.Security.AccessControl.ObjectSecurity":
    Exception: Cannot convert the "Microsoft.PowerShell.Commands.SecurityDescriptorCommandsBase"
    value of type "System.String" to type "System.Type".
    System.Management.Automation.ActionPreferenceStopException:
    Command execution stopped because the preference variable "ErrorActionPreference" or common parameter
    is set to Stop: Unable to find type

oppure

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

È stato contattato l'autore del componente aggiuntivo nella speranza di trovare una soluzione.

<p class="info">Aggiornamento: è stato verificato che la versione più recente di Reflector, 6.5, non causa questa eccezione nella console.</p>

## <a name="opening-package-manager-console-fails-with-objectsecurity-exception"></a>Errore di apertura della console di Gestione pacchetti con eccezione ObjectSecurity

Si potrebbero verificare questi errori quando si tenta di aprire la console di Gestione pacchetti:

    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2977) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2984) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2991) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(2998) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The following error occurred while loading the extended type data file: Microsoft.PowerShell.Core, C:\Windows\SysWOW64\WindowsPowerShell\v1.0\types.ps1xml(3005) : Error in type "System.Security.AccessControl.ObjectSecurity": Exception: The getter method should be public, non void, static, and have one parameter of type PSObject.
    The term 'Get-ExecutionPolicy' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.

In questo caso, seguire la soluzione [descritta su StackOverflow](http://stackoverflow.com/questions/12638289/embedding-powershell-v2-0-in-net-app-on-windows-8-rtm) per correggerli.

## <a name="the-add-package-library-reference-dialog-throws-an-exception-if-the-solution-contains-installshield-limited-edition-project"></a>La finestra di dialogo per l'aggiunta di un riferimento alla libreria di pacchetti genera un'eccezione se la soluzione contiene un progetto InstallShield Limited Edition.

È stato scoperto che se la soluzione contiene uno o più progetti InstallShield Limited Edition, la finestra di dialogo per **l'aggiunta di un riferimento alla libreria di pacchetti**genera un'eccezione all'apertura. Non esiste attualmente alcuna soluzione, se non rimuovere o scaricare i progetti InstallShield.

## <a name="uninstall-button-greyed-out-nuget-requires-admin-privileges-to-installuninstall"></a>Pulsante Disinstalla disabilitato? Per l'installazione o la disinstallazione NuGet richiede privilegi di amministratore

Se si tenta di disinstallare NuGet tramite Gestione estensioni di Visual Studio, il pulsante Disinstalla potrebbe risultare disabilitato.
Per l'installazione o la disinstallazione NuGet richiede l'accesso con privilegi di amministratore. Riavviare Visual Studio come amministratore per disinstallare l'estensione.
NuGet non richiede l'accesso con privilegi di amministratore per l'uso.

## <a name="the-package-manager-console-crashes-when-i-open-it-in-windows-xp-whats-wrong"></a>Arresto anomalo della console di gestione pacchetti quando viene aperta in Windows XP. Qual è il problema?

NuGet richiede il runtime di PowerShell 2.0. Windows XP, per impostazione predefinita, non include PowerShell 2.0. È possibile scaricare il runtime di PowerShell 2.0 da [http://support.microsoft.com/kb/968929](http://support.microsoft.com/kb/968929). Dopo l'installazione, riavviare Visual Studio. Dovrebbe essere possibile aprire la console di Gestione pacchetti.

## <a name="visual-studio-2010-sp1-beta-crashes-on-exit-if-the-package-manager-console-is-open"></a>Arresto anomalo di Visual Studio 2010 SP1 Beta in uscita se la console di Gestione pacchetti è aperta.

Se è installato Visual Studio 2010 SP1 Beta, potrebbe verificarsi un arresto anomalo se si lascia aperta la console di Gestione pacchetti e si chiude Visual Studio. Si tratta di un problema noto di Visual Studio e verrà risolto nella versione SP1 RTM.
Per il momento, ignorare l'arresto anomalo o disinstallare la versione SP1 Beta, se possibile.

## <a name="the-element-metadata--has-invalid-child-element-exception-occurs"></a>Si verifica l'eccezione "L'elemento 'metadata' contiene un elemento figlio non valido"

Se si installano pacchetti compilati con una versione non definitiva di NuGet, potrebbe essere visualizzato un messaggio di errore "L'elemento 'metadata' contiene un elemento figlio non valido nello spazio dei nomi 'schemas.microsoft.com/packaging/2010/07/nuspec.xsd'" quando si esegue la versione RTM di NuGet con tale progetto. Sarà necessario disinstallare e reinstallare ogni pacchetto usando la versione RTM di NuGet.

## <a name="attempting-to-install-or-uninstall-results-in-the-error-cannot-create-a-file-when-that-file-already-existsrdquo"></a>Qualsiasi tentativo di eseguire un'installazione o una disinstallazione genera l'errore "Impossibile creare un file, se il file esiste già.&rdquo;

Per qualche motivo, le estensioni di Visual Studio possono trovarsi in uno stato strano, in cui viene disinstallata l'estensione VSIX ma rimangono alcuni file. Per risolvere questo problema:

1. Chiudi Visual Studio
2. Aprire la cartella seguente (potrebbe essere in un'unità diversa nel computer in uso)

    C:\Programmi (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions\Microsoft Corporation\NuGet Package Manager\<versione>\

3. Eliminare tutti i file con estensione *.deleteme*.
4. Riaprire Visual Studio.

Dopo aver completato questi passaggi, dovrebbe essere possibile continuare.

## <a name="in-rare-cases-compiling-with-code-analysis-turned-on-causes-error"></a>In rari casi, la compilazione con Analisi codice attivata causa un errore.

Potrebbe essere visualizzato l'errore seguente se si installa FluentNHibernate con la console di Gestione pacchetti e quindi si compila il progetto con la funzionalità "Analisi codice" attivata.

    Error 3 CA0058 : The referenced assembly
    'NHibernate, Version=3.0.0.2001, Culture=neutral, PublicKeyToken=aa95f207798dfdb4'
    could not be found. This assembly is required for analysis and was referenced by:
    C:\temp\Scratch\src\MyProject.UnitTests\bin\Debug\MyProject.UnitTests.dll.
    MyProject.UnitTests

Per impostazione predefinita, FluentNHibernate richiede NHibernate 3.0.0.2001. Tuttavia, in base alla progettazione NuGet installerà NHibernate 3.0.0.4000 nel progetto e aggiungerà i reindirizzamenti di binding appropriati per consentirne il funzionamento. Il progetto verrà compilato correttamente anche se l'analisi codice non è attivata. A differenza del compilatore, lo strumento di analisi codice non segue correttamente i reindirizzamenti di binding per usare la versione 3.0.0.4000 anziché 3.0.0.2001. È possibile risolvere il problema installando NHibernate 3.0.0.2001 oppure indicare allo strumento di analisi codice di adottare lo stesso comportamento del compilatore, seguendo questa procedura:

1. Passare a *%PROGRAMFILES%\Microsoft Visual Studio 10.0\Team Tools\Static Analysis Tools\FxCop*
1. Aprire FxCopCmd.exe.config e modificare `AssemblyReferenceResolveMode` da `StrongName` a `StrongNameIgnoringVersion`.
1. Salvare le modifiche e ricompilare il progetto.

## <a name="write-error-command-doesnt-work-inside-installps1uninstallps1initps1"></a>Il comando Write-Error non funziona all'interno di install.ps1/uninstall.ps1/init.ps1

Si tratta di un problema noto. Anziché chiamare Write-Error, provare a chiamare throw.

    throw "My error message"

## <a name="installing-nuget-with-restricted-access-on-windows-2003-can-crash-visual-studio"></a>L'installazione di NuGet con accesso limitato in Windows 2003 può causare l'arresto anomalo di Visual Studio
Quando si tenta di installare NuGet tramite Gestione estensioni di Visual Studio senza diritti di amministratore, viene visualizzata la finestra di dialogo &#8220;Esegui come&#8221; con la casella di controllo &#8220;Esegui il programma con accesso limitato&#8221; selezionata per impostazione predefinita.

![Finestra di dialogo Esegui come con restrizioni](./media/RunAsRestricted.png)

Se si fa clic su OK con tale casella di controllo selezionata si verifica un arresto anomalo di Visual Studio. Assicurarsi di deselezionare l'opzione prima di installare NuGet.

## <a name="cannot-uninstall-nuget-for-windows-phone-tools"></a>Non è possibile disinstallare NuGet per Strumenti di Windows Phone
Strumenti di Windows Phone non include il supporto per Gestione estensioni di Visual Studio. Per disinstallare NuGet, eseguire il comando seguente.

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="changing-the-capitalization-of-nuget-package-ids-breaks-package-restore"></a>La modifica della combinazione di maiuscole/minuscole degli ID di pacchetto NuGet causa errori durante il ripristino del pacchetto
Come descritto in dettaglio in [questo problema su GitHub](https://github.com/Particular/NServiceBus/issues/1271#issuecomment-20865932), la modifica della combinazione di maiuscole/minuscole dei pacchetti NuGet può essere effettuata dal supporto NuGet, ma causa complicazioni durante il ripristino del pacchetto per gli utenti con pacchetti esistenti, con diversa combinazione di maiuscole/minuscole, nella cache dei pacchetti locale. È consigliabile richiedere una modifica della combinazione di maiuscole/minuscole solo quando è possibile avvisare gli utenti esistenti del pacchetto dei problemi che potrebbero verificarsi durante il ripristino del pacchetto in fase di compilazione.

## <a name="reporting-issues"></a>Segnalazione di problemi
Per segnalare eventuali problemi per i client NuGet, visitare [questo sito](https://nuget.codeplex.com/WorkItem/Create).
Per segnalare eventuali problemi per la raccolta NuGet, visitare [questo sito](https://github.com/nuget/nugetgallery/issues).
