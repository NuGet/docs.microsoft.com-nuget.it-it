---
title: Come creare un pacchetto per i controlli UWP con NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: Come creare pacchetti NuGet contenenti controlli UWP, inclusi i metadati e i file di supporto necessari per le finestre di progettazione di Visual Studio e Blend.
keywords: controlli UWP NuGet, finestra di progettazione XAML di Visual Studio, finestra di progettazione di Blend, controlli personalizzati
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8756ce472c11a05370914841245295361b3f179b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Creazione di controlli UWP come pacchetti NuGet

Con Visual Studio 2017, è possibile sfruttare le funzionalità aggiunte per i controlli UWP inseriti nei pacchetti NuGet. Questa guida illustra tali funzionalità usando l'[esempio ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="pre-requisites"></a>Prerequisiti:

1.  Visual Studio 2017
1.  Familiarità con la [creazione di pacchetti UWP](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Aggiungere il supporto della casella degli strumenti e del riquadro Asset per i controlli XAML

Per visualizzare un controllo XAML nella casella degli strumenti della finestra di progettazione XAML in Visual Studio e nel riquadro Asset di Blend, creare un file `VisualStudioToolsManifest.xml` nella radice della cartella `tools` del progetto del pacchetto. Questo file non è obbligatorio se non è necessario visualizzare il controllo nella casella degli strumenti o nel riquadro Asset.

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

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

Si supponga, ad esempio, di avere impostato la proprietà TPMinV per il pacchetto dei controlli sull'edizione dell'anniversario di Windows 10 (10.0; build 14393) e di volersi quindi assicurare che il pacchetto venga utilizzato solo da progetti UWP che corrispondono a tale limite inferiore. Per consentire al pacchetto di essere utilizzato da progetti UWP basati su `project.json`, è necessario creare un pacchetto per i controlli con i nomi di cartella seguenti:

```
\lib\uap10.0\*
\ref\uap10.0\*
```

Per applicare il controllo TPMinV appropriato, creare un [file di destinazioni MSBuild](/visualstudio/msbuild/msbuild-targets) e crearne un pacchetto sotto la cartella build (sostituendo "your_assembly_name" con il nome dell'assembly specifico):

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

Ecco un esempio dell'aspetto del file di destinazioni:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Aggiungere il supporto in fase di progettazione

Per configurare dove visualizzare le proprietà del controllo nel controllo proprietà, aggiungere gli strumenti decorativi personalizzati e così via e inserire il file `design.dll` nella cartella `lib\<platform>\Design` in modo appropriato alla piattaforma di destinazione. Per assicurarsi inoltre che la funzionalità **[Modifica modello > Modifica copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** operi correttamente, è necessario includere nella cartella `<AssemblyName>\Themes` `Generic.xaml` e tutti i dizionari risorse uniti. Questo file non influisce sul comportamento di runtime di un controllo.


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> Per impostazione predefinita, le proprietà del controllo verranno visualizzate sotto la categoria Varie nel controllo proprietà.


## <a name="use-strings-and-resources"></a>Usare stringhe e risorse

È possibile incorporare nel pacchetto le risorse stringa (`.resw`) che possono essere usate dal controllo o dal progetto UWP utilizzato e impostare la proprietà **Azione di compilazione** del file `.resw` su **PRIResource**.

Per un esempio, vedere [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) nell'esempio ExtensionSDKasNuGetPackage.

## <a name="package-content-such-as-images"></a>Creare un pacchetto per contenuti come le immagini

Per creare un pacchetto per contenuti come le immagini che possono essere usate dal controllo o dal progetto UWP utilizzato, aggiungere tali file alla cartella `lib\uap10.0.14393.0`, come segue. Anche in questo caso, "your_assembly_name" deve corrispondere al controllo specifico:

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

È anche possibile creare un [file di destinazioni MSBuild](/visualstudio/msbuild/msbuild-targets) per assicurarsi che l'asset venga copiato nella cartella di output del progetto utilizzato:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Vedere anche

- [Creare pacchetti UWP](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) (Esempio ExtensionSDKasNuGetPackage)
