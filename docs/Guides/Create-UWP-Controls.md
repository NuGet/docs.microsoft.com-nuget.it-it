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
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="4da58-104">Creazione di controlli UWP come pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="4da58-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="4da58-105">Con Visual Studio 2017, è possibile sfruttare le funzionalità aggiunte per i controlli UWP inseriti nei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="4da58-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="4da58-106">Questa guida illustra tali funzionalità usando l'[esempio ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="4da58-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="4da58-107">Prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="4da58-107">Pre-requisites:</span></span>

1.  <span data-ttu-id="4da58-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4da58-108">Visual Studio 2017</span></span>
1.  <span data-ttu-id="4da58-109">Familiarità con la [creazione di pacchetti UWP](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4da58-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="4da58-110">Aggiungere il supporto della casella degli strumenti e del riquadro Asset per i controlli XAML</span><span class="sxs-lookup"><span data-stu-id="4da58-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="4da58-111">Per visualizzare un controllo XAML nella casella degli strumenti della finestra di progettazione XAML in Visual Studio e nel riquadro Asset di Blend, creare un file `VisualStudioToolsManifest.xml` nella radice della cartella `tools` del progetto del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4da58-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="4da58-112">Questo file non è obbligatorio se non è necessario visualizzare il controllo nella casella degli strumenti o nel riquadro Asset.</span><span class="sxs-lookup"><span data-stu-id="4da58-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

<span data-ttu-id="4da58-113">La struttura del file è la seguente:</span><span class="sxs-lookup"><span data-stu-id="4da58-113">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="4da58-114">dove:</span><span class="sxs-lookup"><span data-stu-id="4da58-114">where:</span></span>

- <span data-ttu-id="4da58-115">*your_package_file*: nome del file di controllo, ad esempio `ManagedPackage.winmd`. "ManagedPackage" è un nome arbitrario usato per questo esempio e non ha altri significati.</span><span class="sxs-lookup"><span data-stu-id="4da58-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="4da58-116">*vs_category*: etichetta del gruppo in cui il controllo deve essere visualizzato nella casella degli strumenti della finestra di progettazione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4da58-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="4da58-117">`VSCategory` è necessario per visualizzare il controllo nella casella degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="4da58-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="4da58-118">*blend_category*: etichetta del gruppo in cui il controllo deve essere visualizzato nel riquadro Asset della finestra di progettazione di Blend.</span><span class="sxs-lookup"><span data-stu-id="4da58-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="4da58-119">`BlendCategory` è necessario per visualizzare il controllo in Asset.</span><span class="sxs-lookup"><span data-stu-id="4da58-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="4da58-120">*type_full_name_n*: nome completo di ogni controllo, incluso lo spazio dei nomi, ad esempio `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="4da58-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="4da58-121">Si noti che il formato punto viene usato sia per i tipi gestiti che per quelli nativi.</span><span class="sxs-lookup"><span data-stu-id="4da58-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="4da58-122">Negli scenari più avanzati è anche possibile includere più elementi `<File>` in `<FileList>` quando un singolo pacchetto contiene più assembly del controllo.</span><span class="sxs-lookup"><span data-stu-id="4da58-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="4da58-123">È anche possibile avere più nodi `<ToolboxItems>` in un singolo `<File>` se si vuole organizzare i controlli in categorie separate.</span><span class="sxs-lookup"><span data-stu-id="4da58-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="4da58-124">Nell'esempio seguente il controllo implementato in `ManagedPackage.winmd` verrà visualizzato in Visual Studio e in Blend in un gruppo denominato "Managed Package" e "MyCustomControl" verrà visualizzato in tale gruppo.</span><span class="sxs-lookup"><span data-stu-id="4da58-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="4da58-125">Tutti questi nomi sono arbitrari.</span><span class="sxs-lookup"><span data-stu-id="4da58-125">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="4da58-128">È necessario specificare in modo esplicito ogni controllo che si vuole visualizzare nella casella degli strumenti e nel riquadro Asset.</span><span class="sxs-lookup"><span data-stu-id="4da58-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="4da58-129">Assicurarsi di specificarli nel formato `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="4da58-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="4da58-130">Aggiungere icone personalizzate ai controlli</span><span class="sxs-lookup"><span data-stu-id="4da58-130">Add custom icons to your controls</span></span>

<span data-ttu-id="4da58-131">Per visualizzare un'icona personalizzata nella casella degli strumenti e nel riquadro Asset, aggiungere un'immagine al proprio progetto o al corrispondente progetto `design.dll` con il nome "Namespace.ControlName.extension" e impostare l'azione di compilazione su "Risorsa incorporata".</span><span class="sxs-lookup"><span data-stu-id="4da58-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="4da58-132">I formati supportati sono `.png`, `.jpg`, `.jpeg`, `.gif` e `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="4da58-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="4da58-133">Le dimensioni dell'immagine consigliate sono pari a 64 x 64 pixel.</span><span class="sxs-lookup"><span data-stu-id="4da58-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="4da58-134">Nell'esempio seguente il progetto contiene un file di immagine denominato "ManagedPackage.MyCustomControl.png".</span><span class="sxs-lookup"><span data-stu-id="4da58-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Impostazione di un'icona personalizzata in un progetto](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="4da58-136">Per i controlli nativi, è necessario inserire l'icona come risorsa nel progetto `design.dll`.</span><span class="sxs-lookup"><span data-stu-id="4da58-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="4da58-137">Supportare versioni specifiche della piattaforma Windows</span><span class="sxs-lookup"><span data-stu-id="4da58-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="4da58-138">I pacchetti UWP hanno una proprietà TargetPlatformVersion (TPV) e una proprietà TargetPlatformMinVersion (TPMinV) che definiscono i limiti superiore e inferiore della versione del sistema operativo in cui l'app può essere installata.</span><span class="sxs-lookup"><span data-stu-id="4da58-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="4da58-139">TPV specifica anche la versione dell'SDK in cui viene compilata l'app.</span><span class="sxs-lookup"><span data-stu-id="4da58-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="4da58-140">Tenere sempre presente queste proprietà quando si crea un pacchetto UWP: usando API non comprese nei limiti delle versioni della piattaforma definite nell'app, non sarà possibile eseguire la compilazione o l'app avrà esito negativo in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4da58-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="4da58-141">Si supponga, ad esempio, di avere impostato la proprietà TPMinV per il pacchetto dei controlli sull'edizione dell'anniversario di Windows 10 (10.0; build 14393) e di volersi quindi assicurare che il pacchetto venga utilizzato solo da progetti UWP che corrispondono a tale limite inferiore.</span><span class="sxs-lookup"><span data-stu-id="4da58-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="4da58-142">Per consentire al pacchetto di essere utilizzato da progetti UWP basati su `project.json`, è necessario creare un pacchetto per i controlli con i nomi di cartella seguenti:</span><span class="sxs-lookup"><span data-stu-id="4da58-142">To allow your package to be consumed by `project.json` based UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0\*
\ref\uap10.0\*
```

<span data-ttu-id="4da58-143">Per applicare il controllo TPMinV appropriato, creare un [file di destinazioni MSBuild](/visualstudio/msbuild/msbuild-targets) e crearne un pacchetto sotto la cartella build (sostituendo "your_assembly_name" con il nome dell'assembly specifico):</span><span class="sxs-lookup"><span data-stu-id="4da58-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

<span data-ttu-id="4da58-144">Ecco un esempio dell'aspetto del file di destinazioni:</span><span class="sxs-lookup"><span data-stu-id="4da58-144">Here is an example of what the targets file should look like:</span></span>

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

## <a name="add-design-time-support"></a><span data-ttu-id="4da58-145">Aggiungere il supporto in fase di progettazione</span><span class="sxs-lookup"><span data-stu-id="4da58-145">Add design-time support</span></span>

<span data-ttu-id="4da58-146">Per configurare dove visualizzare le proprietà del controllo nel controllo proprietà, aggiungere gli strumenti decorativi personalizzati e così via e inserire il file `design.dll` nella cartella `lib\<platform>\Design` in modo appropriato alla piattaforma di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4da58-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="4da58-147">Per assicurarsi inoltre che la funzionalità **[Modifica modello > Modifica copia](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** operi correttamente, è necessario includere nella cartella `<AssemblyName>\Themes` `Generic.xaml` e tutti i dizionari risorse uniti.</span><span class="sxs-lookup"><span data-stu-id="4da58-147">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="4da58-148">Questo file non influisce sul comportamento di runtime di un controllo.</span><span class="sxs-lookup"><span data-stu-id="4da58-148">(This file has no impact on the runtime behavior of a control.)</span></span>


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
> <span data-ttu-id="4da58-149">Per impostazione predefinita, le proprietà del controllo verranno visualizzate sotto la categoria Varie nel controllo proprietà.</span><span class="sxs-lookup"><span data-stu-id="4da58-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>


## <a name="use-strings-and-resources"></a><span data-ttu-id="4da58-150">Usare stringhe e risorse</span><span class="sxs-lookup"><span data-stu-id="4da58-150">Use strings and resources</span></span>

<span data-ttu-id="4da58-151">È possibile incorporare nel pacchetto le risorse stringa (`.resw`) che possono essere usate dal controllo o dal progetto UWP utilizzato e impostare la proprietà **Azione di compilazione** del file `.resw` su **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="4da58-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="4da58-152">Per un esempio, vedere [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) nell'esempio ExtensionSDKasNuGetPackage.</span><span class="sxs-lookup"><span data-stu-id="4da58-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="4da58-153">Creare un pacchetto per contenuti come le immagini</span><span class="sxs-lookup"><span data-stu-id="4da58-153">Package content such as images</span></span>

<span data-ttu-id="4da58-154">Per creare un pacchetto per contenuti come le immagini che possono essere usate dal controllo o dal progetto UWP utilizzato,</span><span class="sxs-lookup"><span data-stu-id="4da58-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="4da58-155">aggiungere tali file alla cartella `lib\uap10.0.14393.0`, come segue. Anche in questo caso, "your_assembly_name" deve corrispondere al controllo specifico:</span><span class="sxs-lookup"><span data-stu-id="4da58-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

<span data-ttu-id="4da58-156">È anche possibile creare un [file di destinazioni MSBuild](/visualstudio/msbuild/msbuild-targets) per assicurarsi che l'asset venga copiato nella cartella di output del progetto utilizzato:</span><span class="sxs-lookup"><span data-stu-id="4da58-156">You may also author an[MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

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

## <a name="see-also"></a><span data-ttu-id="4da58-157">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4da58-157">See also</span></span>

- [<span data-ttu-id="4da58-158">Creare pacchetti UWP</span><span class="sxs-lookup"><span data-stu-id="4da58-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- <span data-ttu-id="4da58-159">[ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage) (Esempio ExtensionSDKasNuGetPackage)</span><span class="sxs-lookup"><span data-stu-id="4da58-159">[ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)</span></span>
