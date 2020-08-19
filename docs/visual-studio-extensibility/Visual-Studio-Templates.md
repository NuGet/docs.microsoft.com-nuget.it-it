---
title: Pacchetti NuGet nei modelli di Visual Studio
description: Istruzioni per includere i pacchetti NuGet nei modelli di progetto e di elemento di Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 2dfbd793eee05169f051d9c8943bc065945b92da
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622642"
---
# <a name="packages-in-visual-studio-templates"></a>Pacchetti nei modelli di Visual Studio

I modelli di progetto e di elemento di Visual Studio spesso hanno bisogno della garanzia che determinati pacchetti siano installati quando viene creato il progetto o l'elemento. Ad esempio, il modello ASP.NET MVC 3 installa jQuery, Modernizr e altri pacchetti.

A supporto di questa funzionalità, gli autori di modelli possono indicare a NuGet di installare i pacchetti necessari, anziché singole librerie. Gli sviluppatori possono quindi aggiornare facilmente tali pacchetti in un secondo momento.

Per altre informazioni sulla creazione dei modelli, fare riferimento a [Procedura: Creare modelli di progetto](/visualstudio/ide/how-to-create-project-templates) o [Creazione di modelli di progetto e di elemento personalizzati](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Il resto di questa sezione descrive i passaggi specifici da eseguire durante la creazione di un modello per includere correttamente i pacchetti NuGet.

- [Aggiunta di pacchetti a un modello](#adding-packages-to-a-template)
- [Procedure consigliate](#best-practices)

Per un esempio, vedere l'[esempio NuGetInVsTemplates](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Aggiunta di pacchetti a un modello

Quando viene creata un'istanza di un modello, viene richiamata una [creazione guidata di modelli](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) per caricare l'elenco dei pacchetti da installare insieme alle informazioni su dove trovare tali pacchetti. I pacchetti possono essere incorporati in VSIX, incorporati nel modello o situati sul disco rigido locale, nel qual caso viene usata una chiave del Registro di sistema per fare riferimento al percorso del file. Informazioni dettagliate su questi percorsi sono disponibili più avanti in questa sezione.

I pacchetti preinstallati funzionano tramite [creazioni guidate di modelli](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Viene richiamata una speciale procedura guidata quando viene creata l'istanza del modello. La procedura guidata carica l'elenco dei pacchetti che devono essere installati e passa le informazioni alle API NuGet appropriate.

Passaggi per includere i pacchetti in un modello:

1. Nel `vstemplate` file aggiungere un riferimento alla creazione guidata modelli NuGet aggiungendo un [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) elemento:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` è un assembly che contiene solo la classe `TemplateWizard`, che è un semplice wrapper che chiama l'implementazione effettiva in `NuGet.VisualStudio.dll`. La versione dell'assembly non verrà mai modificata, pertanto i modelli di progetto/elemento continuano a funzionare con le nuove versioni di NuGet.

1. Aggiungere l'elenco dei pacchetti da installare nel progetto:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    La procedura guidata supporta più elementi `<package>` per supportare più origini dei pacchetti. Sono richiesti entrambi gli attributi `id` e `version`, il che significa che una versione specifica di un pacchetto verrà installata anche se è disponibile una versione più recente. Ciò impedisce agli aggiornamenti pacchetto di interrompere il modello, lasciando la scelta di aggiornare il pacchetto allo sviluppatore che usa il modello.

1. Specificare il repository dove NuGet può dove trovare i pacchetti come descritto nelle sezioni successive.

### <a name="vsix-package-repository"></a>Repository di pacchetti VSIX

L'approccio di distribuzione consigliato per i modelli di progetto/elemento di Visual Studio è un'[estensione VSIX](/visualstudio/extensibility/shipping-visual-studio-extensions) perché consente di inserire in un pacchetto più modelli di progetto/elemento e permette agli sviluppatori di individuare facilmente i modelli usando Gestione estensioni di Visual Studio o Visual Studio Gallery. Anche gli aggiornamenti all'estensione sono facili da distribuire tramite il [meccanismo di aggiornamento automatico di Gestione estensioni di Visual Studio](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

VSIX può fungere da origine per i pacchetti richiesta dal modello:

1. Modificare l'elemento `<packages>` nel file `.vstemplate` come indicato di seguito:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    L'attributo `repository` specifica il tipo di repository come `extension` mentre `repositoryId` è l'identificatore univoco di VSIX, ovvero il valore dell'attributo `ID` nel file `vsixmanifest` dell'estensione. Vedere [Riferimenti su VSIX Extension Schema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference).

1. Inserire i file `nupkg` in una cartella chiamata `Packages` all'interno di VSIX.

1. Aggiungere i file di pacchetto necessari come `<Asset>` nel file `vsixmanifest`. Vedere [Riferimenti su VSIX Extension Schema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Si noti che è possibile distribuire i pacchetti nello stesso VSIX dei modelli di progetto oppure è possibile inserirli in un VSIX distinto, se più opportuno per lo specifico scenario. Tuttavia, non fare riferimento ad alcun VSIX su cui non si ha controllo, perché le modifiche apportate a tale estensione potrebbero interrompere il modello.

### <a name="template-package-repository"></a>Repository di pacchetti di modello

Se si distribuisce solo un singolo modello di progetto/elemento e non è necessario inserire più modelli in un pacchetto, è possibile ricorrere a un approccio più semplice ma più limitato che include i pacchetti direttamente nel file ZIP del modello di progetto/elemento:

1. Modificare l'elemento `<packages>` nel file `.vstemplate` come indicato di seguito:

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    L'attributo `repository` ha il valore `template` e l'attributo `repositoryId` non è richiesto.

1. Inserire i pacchetti nella cartella radice del file ZIP del modello di progetto/elemento.

Si noti che l'uso di questo approccio in un VSIX che contiene più modelli comporta un aumento eccessivo non necessario quando uno o più pacchetti sono comuni per i modelli. In tali casi, usare [VSIX come repository](#vsix-package-repository) come descritto nella sezione precedente.

### <a name="registry-specified-folder-path"></a>Percorso della cartella specificato dal Registro di sistema

Gli SDK che vengono installati tramite un file MSI possono installare i pacchetti NuGet direttamente nel computer dello sviluppatore. In questo modo si rendono immediatamente disponibili quando viene usato un modello di progetto o di elemento, anziché doverli estrarre in quella fase. I modelli ASP.NET usano questo approccio.

1. Fare in modo che il file MSI installi i pacchetti nel computer. È possibile installare solo i file `.nupkg` oppure è possibile installarli insieme al contenuto espanso, che consente di risparmiare un ulteriore passaggio quando viene usato il modello. In questo caso, seguire la struttura di cartelle standard di NuGet in cui i file `.nupkg` si trovano nella cartella radice e quindi ogni pacchetto dispone di una sottocartella con la coppia ID/versione come nome della sottocartella.

1. Scrivere una chiave del Registro di sistema per identificare il percorso del pacchetto:

    - Percorso della chiave: `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` a livello di computer o, in caso di pacchetti e modelli installati per utente, usare in alternativa `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.
    - Nome della chiave: usare un nome univoco per l'utente. Ad esempio, i modelli ASP.NET MVC 4 per Visual Studio 2012 usano `AspNetMvc4VS11`.
    - Valori: percorso completo della cartella dei pacchetti.

1. Nell'elemento `<packages>` nel file `.vstemplate` aggiungere l'attributo `repository="registry"` e specificare il nome della chiave del Registro di sistema nell'attributo `keyName`.

    - Se i pacchetti sono già stati decompressi in precedenza, usare l'attributo `isPreunzipped="true"`.
    - *(NuGet 3.2+)* Se si vuole forzare una compilazione in fase di progettazione al termine dell'installazione del pacchetto, aggiungere l'attributo `forceDesignTimeBuild="true"`.
    - Come ottimizzazione, aggiungere `skipAssemblyReferences="true"` perché il modello stesso include già i riferimenti necessari.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Procedure consigliate

1. Dichiarare una dipendenza da VSIX di NuGet aggiungendo un riferimento a esso nel manifesto VSIX:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Richiedi il salvataggio dei modelli di progetto/elemento durante la creazione includendo [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) nel `.vstemplate` file.

1. I modelli non includono un file `packages.config` e non includono riferimenti o contenuto che verrebbero aggiunti al momento dell'installazione dei i pacchetti NuGet.
