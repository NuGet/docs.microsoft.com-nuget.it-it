---
title: Come creare un pacchetto per i controlli dell'interfaccia utente con NuGet
description: Come creare pacchetti NuGet contenenti controlli UWP o WPF, inclusi i metadati e i file di supporto necessari per le finestre di progettazione di Visual Studio e Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ce5ad07209a06010150b14092aa1b15ee6f84146
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548738"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Creazione di controlli dell'interfaccia utente come pacchetti NuGet

Con Visual Studio 2017, è possibile sfruttare le funzionalità aggiunte per i controlli UWP e WPF inseriti nei pacchetti NuGet. Questa guida illustra tali funzionalità nel contesto dei controlli UWP usando l'[esempio ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). Lo stesso vale per i controlli WPF, se non diversamente indicato.

## <a name="prerequisites"></a>Prerequisiti

1. Visual Studio 2017
1. Familiarità con la [creazione di pacchetti UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generare il layout della libreria

> [!Note]
> Applicabile solo ai controlli UWP.

L'impostazione della proprietà `GenerateLibraryLayout` garantisce che l'output di compilazione del progetto venga generato in un layout che è pronto per essere incluso nel pacchetto senza la necessità di voci per singoli file in nuspec.

Dalle proprietà del progetto, passare alla scheda Build e selezionare la casella di controllo "Genera layout libreria". Verrà modificato il file di progetto e il flag `GenerateLibraryLayout` verrà impostato su true per la configurazione e la piattaforma di compilazione attualmente selezionata.

In alternativa, modificare il file di progetto per aggiungere `<GenerateLibraryLayout>true</GenerateLibraryLayout>` al primo gruppo di proprietà non condizionale. Questa modifica verrà applicata alla proprietà indipendentemente dalla configurazione o dalla piattaforma di compilazione.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Aggiungere il supporto della casella degli strumenti e del riquadro Asset per i controlli XAML

Per visualizzare un controllo XAML nella casella degli strumenti della finestra di progettazione XAML in Visual Studio e nel riquadro Asset di Blend, creare un file `VisualStudioToolsManifest.xml` nella radice della cartella `tools` del progetto del pacchetto. Questo file non è obbligatorio se non è necessario visualizzare il controllo nella casella degli strumenti o nel riquadro Asset.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

La struttura del file è la seguente:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

dove:

- *your_package_file*: nome del file di controllo, ad esempio `ManagedPackage.winmd`. "ManagedPackage" è un nome arbitrario usato per questo esempio e non ha altri significati.
- *vs_category*: etichetta del gruppo in cui il controllo deve essere visualizzato nella casella degli strumenti della finestra di progettazione di Visual Studio. `VSCategory` è necessario per visualizzare il controllo nella casella degli strumenti.
- *blend_category*: etichetta del gruppo in cui il controllo deve essere visualizzato nel riquadro Asset della finestra di progettazione di Blend. `BlendCategory` è necessario per visualizzare il controllo in Asset.
- *type_full_name_n*: nome completo di ogni controllo, incluso lo spazio dei nomi, ad esempio `ManagedPackage.MyCustomControl`. Si noti che il formato punto viene usato sia per i tipi gestiti che per quelli nativi.

Negli scenari più avanzati è anche possibile includere più elementi `<File>` in `<FileList>` quando un singolo pacchetto contiene più assembly del controllo. È anche possibile avere più nodi `<ToolboxItems>` in un singolo `<File>` se si vuole organizzare i controlli in categorie separate.

Nell'esempio seguente il controllo implementato in `ManagedPackage.winmd` verrà visualizzato in Visual Studio e in Blend in un gruppo denominato "Managed Package" e "MyCustomControl" verrà visualizzato in tale gruppo. Tutti questi nomi sono arbitrari.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Controllo di esempio visualizzato in Visual Studio](media/UWP-control-vs-toolbox.png)

![Controllo di esempio visualizzato in Blend](media/UWP-control-blend-assets.png)

> [!Note]
> È necessario specificare in modo esplicito ogni controllo che si vuole visualizzare nella casella degli strumenti e nel riquadro Asset. Assicurarsi di specificarli nel formato `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Aggiungere icone personalizzate ai controlli

Per visualizzare un'icona personalizzata nella casella degli strumenti e nel riquadro Asset, aggiungere un'immagine al proprio progetto o al corrispondente progetto `design.dll` con il nome "Namespace.ControlName.extension" e impostare l'azione di compilazione su "Risorsa incorporata". I formati supportati sono `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`. Le dimensioni dell'immagine consigliate sono pari a 64 x 64 pixel.

Nell'esempio seguente il progetto contiene un file di immagine denominato "ManagedPackage.MyCustomControl.png".

![Impostazione di un'icona personalizzata in un progetto](media/UWP-control-custom-icon.png)

> [!Note]
> Per i controlli nativi, è necessario inserire l'icona come risorsa nel progetto `design.dll`.

## <a name="support-specific-windows-platform-versions"></a>Supportare versioni specifiche della piattaforma Windows

I pacchetti UWP hanno una proprietà TargetPlatformVersion (TPV) e una proprietà TargetPlatformMinVersion (TPMinV) che definiscono i limiti superiore e inferiore della versione del sistema operativo in cui l'app può essere installata. TPV specifica anche la versione dell'SDK in cui viene compilata l'app. Tenere sempre presente queste proprietà quando si crea un pacchetto UWP: usando API non comprese nei limiti delle versioni della piattaforma definite nell'app, non sarà possibile eseguire la compilazione o l'app avrà esito negativo in fase di esecuzione.

Si supponga, ad esempio, di avere impostato la proprietà TPMinV per il pacchetto dei controlli sull'edizione dell'anniversario di Windows 10 (10.0; build 14393) e di volersi quindi assicurare che il pacchetto venga utilizzato solo da progetti UWP che corrispondono a tale limite inferiore. Per consentire al pacchetto di essere utilizzato da progetti UWP, è necessario creare un pacchetto per i controlli con i nomi di cartella seguenti:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet controllerà automaticamente la proprietà TPMinV del progetto che utilizza il pacchetto e l'installazione avrà esito negativo se il valore è inferiore a Windows 10 Anniversary Edition (10.0; build 14393)

Nel caso di WPF, si supponga di volere che il pacchetto dei controlli WPF venga utilizzato dai progetti destinati a .NET Framework v4.6.1 o versione successiva. Per imporre questo requisito, è necessario creare un pacchetto dei controlli con i nomi di cartelle seguenti:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Aggiungere il supporto in fase di progettazione

Per configurare dove visualizzare le proprietà del controllo nel controllo proprietà, aggiungere gli strumenti decorativi personalizzati e così via e inserire il file `design.dll` nella cartella `lib\uap10.0.14393\Design` in modo appropriato alla piattaforma di destinazione. Per assicurarsi inoltre che la funzionalità **[Modifica modello > Modifica copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** operi correttamente, è necessario includere nella cartella `<your_assembly_name>\Themes` `Generic.xaml` e tutti i dizionari risorse uniti, ancora una volta usando il nome di assembly effettivo. Questo file non influisce sul comportamento di runtime di un controllo. La struttura di cartelle avrà quindi l'aspetto seguente:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Nel caso di WPF, si supponga di continuare con l'esempio in cui si vuole che il pacchetto dei controlli WPF venga utilizzato dai progetti destinati a .NET Framework v4.6.1 o versione successiva:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Per impostazione predefinita, le proprietà del controllo verranno visualizzate sotto la categoria Varie nel controllo proprietà.

## <a name="use-strings-and-resources"></a>Usare stringhe e risorse

È possibile incorporare nel pacchetto le risorse stringa (`.resw`) che possono essere usate dal controllo o dal progetto UWP utilizzato e impostare la proprietà **Azione di compilazione** del file `.resw` su **PRIResource**.

Per un esempio, vedere [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) nell'esempio ExtensionSDKasNuGetPackage.

> [!Note]
> Applicabile solo ai controlli UWP.

## <a name="see-also"></a>Vedere anche

- [Creare pacchetti UWP](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) (Esempio ExtensionSDKasNuGetPackage)
